# Nacos 搭建手册

## 1. Docker 搭建单机版 Nacos

```shell
# 1. 下载 nacos
docker pull nacos/nacos-server:v2.2.3

# 2. 建立 custom.properties ；具体文件内容看官网版本包；其实这里运行需要看一下 docker 的官网制作的 docker 文件；例如以 v2.2.3 版本为例；使用的 workdir : /home/nacos ；使用配置文件：conf/application.properties

# 3. nacos 导入数据库脚本 【官网下载版本的包，里面有数据库脚本】

# 4. 执行
docker  run \
--name nacos -d \
-p 8848:8848 \
--privileged=true \
--restart=always \
-e JVM_XMS=256m \
-e JVM_XMX=512m \
-e MODE=standalone \
-e PREFER_HOST_MODE=hostname \
-e NACOS_AUTH_ENABLE=true \
-v /app/nacos/logs:/home/nacos/logs \
-v /app/nacos/conf/application.properties:/home/nacos/conf/application.properties \
nacos/nacos-server:v2.2.3
```

