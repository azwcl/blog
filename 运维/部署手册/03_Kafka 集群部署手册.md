# Kafka 集群部署手册

>   为了快速搭建公司开发环境，快速部署 Kafka 集群环境手册说明

## 1. 规划

| server1         | server2         | server3         |
| --------------- | --------------- | --------------- |
| 192.168.146.130 | 192.168.146.131 | 192.168.146.132 |
| zk + kafka      | zk + kafka      | zk + kafka      |

## 2. 部署 zk

1.  官网下载 kafka ，kafka 内自带 zk
2.  解压到 /data/kafka 目录中
3.  进入 kafka 解压目录：/data/kafka/kafka_2.13-3.0.0/ 下

```shell
# 创建需要的目录
mkdir data && mkdir logs && mkdir kafka-logs

# 配置 config/zookeeper.properties 配置文件
修改该配置文件的 dataDir 配置参数为 /data/kafka/kafka_2.13-3.0.0/data/
增加配置项： dataLogDir 参数，值为：/data/kafka/kafka_2.13-3.0.0/logs/
增加配置项： server.1 = 服务器A ip:2881:3881
            server.2 = 服务器B ip:2881:3881
            server.3 = 服务器C ip:2881:3881
增加配置项：initLimit=10 
           syncLimit=5

# 三台服务器都是该配置
# 且在每台服务器下创建 myid 文件，里面写着服务器序号 1,2,3；对应上面的 server.id 的
echo 1 >> /data/kafka/kafka_2.13-3.0.0/data/myid

# 启动
```

## 3. 部署 kafka 

```shell
# 三台均需修改配置：config/server.properties:
  broker.id=1 # 对应服务器的 id 号码 A服务器是1,B是2,C是3
  listeners=PLAINTEXT://服务器 IP:9092 #注意：这是当前 IP 和当前端口
  log.dirs=/data/kafka/kafka_2.13-3.0.0/kafka-logs/
  zookeeper.connect=192.168.146.130:2181,192.168.146.131:2181,192.168.146.132:2181 # 这是zookeeper 连接

# 三台服务器均启动kafka
  ./bin/kafka-server-start.sh -daemon ./config/server.properties
```

## 4. 结束

>   这里演示，只是搭建，具体配置参数优化，根据实际情况考虑；