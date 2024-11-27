# PostgreSQL 数据库 in 查询限制

在 `PostgreSQL` 数据库中 `in` 查询 本身是没有硬性限制的；但是在 `jdbc` 驱动中，对其进行限制了；

## 1. jdbc 4.20.0 版本之前

```java
/*
代码位置：
org.postgresql.core.PGStream#sendInteger2
*/

/**
 * Sends a 2-byte integer (short) to the back end.
 *
 * @param val the integer to be sent
 * @throws IOException if an I/O error occurs or {@code val} cannot be encoded in 2 bytes
 */
public void sendInteger2(int val) throws IOException {
    if (val < Short.MIN_VALUE || val > Short.MAX_VALUE) {
        throw new IOException("Tried to send an out-of-range integer as a 2-byte value: " + val);
    }
    int2Buf[0] = (byte) (val >>> 8);
    int2Buf[1] = (byte) val;
    pgOutput.write(int2Buf);
}

```

其中 `Short.MAX_VALUE` 为 `32767`个；故 `in` 查询 限制为 `32767` 个；

## 2. jdbc 4.20.0 及以前版本

```java
/*
代码位置：
org.postgresql.core.PGStream#sendInteger2
*/

/**
 * Sends a 2-byte integer (short) to the back end.
 *
 * @param val the integer to be sent
 * @throws IOException if an I/O error occurs or {@code val} cannot be encoded in 2 bytes
 */
public void sendInteger2(int val) throws IOException {
    if (val < 0 || val > 65535) {
        throw new IllegalArgumentException("Tried to send an out-of-range integer as a 2-byte unsigned int value: " + val);
    }
    int2Buf[0] = (byte) (val >>> 8);
    int2Buf[1] = (byte) val;
    pgOutput.write(int2Buf);
}
```

作者修复这个缺陷，将限制调整为无符号 `Short` 最大长度；

# 3. 参考链接

转向：

-   [PostgreSQL 官方更新记录](https://jdbc.postgresql.org/changelogs/2022-06-09-42.4.0-release/)
-   [对应问题 issue](https://github.com/pgjdbc/pgjdbc/issues/1311)
-   [对应 PR](https://github.com/pgjdbc/pgjdbc/pull/2525)

