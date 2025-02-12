# Redis 事务

## 1. 理论简介

### 1.1. 是什么

-   一次性执行多个命令，本质是一组命令的集合；一个事务中的所有命令都会序列化，按照顺序串行化执行而不会被其他命令插入，不允许加塞；
-   官网：https://redis.io/docs/interact/transactions/

## 2. 相关命令及使用

### 2.1. 常用命令

-   `MULTI`：开启事务，redis 会将后续的命令逐个放入到队列之中，再用 `EXEC` 命令来原子化执行这个命令队列；
-   `EXEC`：执行事务中的所有操作命令；
-   `DISCARD`：取消事务，放弃执行事务块中的所有命令；
-   `WATCH`：监视一个或多个 `key`，如果事务在执行前，这个 `key` 被其他命令所改动，则事务被打断；
-   `UNWATCH`：取消监视所有的键；如果调用 `EXEC` 或 `DISCARD` 则无需手动调用 `UNWATCH`；

### 2.2. 实操

#### 2.2.1. 正常执行

```shell
127.0.0.1:6379> multi
OK
127.0.0.1:6379(TX)> set k1 100
QUEUED
127.0.0.1:6379(TX)> expire k1 1000
QUEUED
127.0.0.1:6379(TX)> exec
1) OK
2) (integer) 1
```

#### 2.2.2. 放弃事务执行

```shell
127.0.0.1:6379> multi
OK
127.0.0.1:6379(TX)> set k1 200
QUEUED
127.0.0.1:6379(TX)> set k2 100
QUEUED
127.0.0.1:6379(TX)> discard
OK
```

#### 2.2.3. 全体连坐

-   如果在排队进去的时候，命令有语法错误，例如参数数量不对，命令名称不对，关键字不对，内存不足等，则全局失败;

    ```shell
    127.0.0.1:6379> multi
    OK
    127.0.0.1:6379(TX)> set k1 k1k1k1k
    QUEUED
    127.0.0.1:6379(TX)> set k
    (error) ERR wrong number of arguments for 'set' command
    127.0.0.1:6379(TX)> exec
    (error) EXECABORT Transaction discarded because of previous errors.
    127.0.0.1:6379> get k1
    "100"
    ```

#### 2.2.4. 冤有头，债有主

-   如果说，`exec` 调用之后出错，则仅调用的命令失败，其他命令正常执行；

```shell
127.0.0.1:6379> clear
127.0.0.1:6379> multi
OK
127.0.0.1:6379(TX)> set k1 123123q
QUEUED
127.0.0.1:6379(TX)> incr k1
QUEUED
127.0.0.1:6379(TX)> set k2 123123
QUEUED
127.0.0.1:6379(TX)> exec
1) OK
2) (error) ERR value is not an integer or out of range
3) OK
```

#### 2.2.5. watch 监控

-   Redis 使用 `watch` 来进行乐观锁锁定，类似于 `CAS` 操作；
-   只要数据被修改，无论修改成啥样，均失败；
-   可以在 `multi` 执行前使用 `unwatch` 取消监控；
-   执行 `exec` 或者 `discard` 或者客户端连接丢失，退出；所有监控都会失效；
-   切记，在 6.0.9 版本之前，过期键不会导致事务中止；具体见链接：[github issue](https://github.com/redis/redis/pull/7920)

## 3. 细节详述

### 3.1. CAS 操作实现乐观锁

>   `WATCH` 命令可以为 Redis 事务提供 `check-and-set` 行为；

-   被 `WATCH` 监视的 `key`，会发现是否被改动，如果有至少一个键在被监视的时候被修改，则整个事务都会被取消，`EXEC` 会返回 `nil` 表示事务失败；

-   例如对 Redis 的一个自增操作，不采用 `incr` 命令；

    ```shell
    # 经典的自增事务问题；多个客户端一定出问题；
    get k1
    k1 = k1 + 1
    set k1 val
    ```

-   用 `WATCH` 监视

    ```shell
    WATCH k1
    get k1
    k1 = k1 + 1
    MULTI
    set k1 val
    EXEC
    
    # 在 WATCH 执行之后，EXEC 执行之前，如果有其他客户端修改了 k1 值，则当前事务失败；
    # 故 客户端 只需要不断重试这个操作即可；
    ```

### 3.2. WATCH 如何实现监控

-   Redis 使用 `WATCH` 命令来决定事务是继续执行还是回滚，那么就需要在 `MULTI` 开启事务之前使用 `WATCH` 来监控某些键值对；
-   当执行 `EXEC` 命令时，首先就会比对所有 `WATCH` 监控的键值对，如果没有发生变化，执行事务队列命令，提交事务；如果发生变化，则不会执行任何命令，且该事务废弃回滚；当然无论是否废弃事务，Redis 都会取消执行事务前面的 `WATCH` 命令；

### 3.3. 为什么 Redis 不支持回滚

1.   Redis 命令只会因为错误语法而失败；这种是编程的逻辑性导致的，不应该在生产环境中出现，而应该在开发测试过程中被发现；
2.   不支持回滚，那么 Redis 内部可以保持简单和高效；
3.   Redis 单线程架构，数据结构和命令非常高效，旨在尽可能简单和快速，将命令排队，执行时一次性提交；简化核心设计，避免复杂回滚机制，避免额外开销；同时，也因为 Redis 事务不像传统关系型事务的一样，未实现类似“日志”机制跟踪等；

### 3.4. Redis 与事务 ACID？

1.   原子性：很多文章认为：Redis 事务是不保证原子性的，因为他不能保证所有指令同时成功或失败，只有决定开始执行全部指令的能力，没有失败一条回滚能力，但是 Redis 官方认为遵循 Redis，因为 Redis 的 事务是原子性的，所有命令要么全部执行，要么全部不执行，而不是完全成功；
2.   一致性：可以保证，Redis 在命令提交时按照顺序执行，除非 Redis 宕机；
3.   隔离性：得益于 Redis 单进程单线程模式（6.0之前），可以保证命令执行过程不被打断；
4.   持久性：Redis 持久性很弱，取决于 Redis 本身的配置等；即便开启，也不能一定保证持久化到硬盘；

## 4. 参考链接

1.   [Redis 官方事务文档](https://redis.io/docs/latest/develop/interact/transactions/)

2.   [Redis 关于 WATCH 命令对过期键更改](https://github.com/redis/redis/pull/7920)
3.   [Java pdai.tech Redis 进阶-事务](https://pdai.tech/md/db/nosql-redis/db-redis-x-trans.html#cas%E6%93%8D%E4%BD%9C%E5%AE%9E%E7%8E%B0%E4%B9%90%E8%A7%82%E9%94%81)