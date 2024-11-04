# Docker 搭建 frp 内网穿透

## 1. 目标
- 内网之中有一台服务器需要暴露在公网，但是没有 公网 地址；需要通过一台外网服务器做中转暴露到公网服务器；

## 2. 准备
- 一台家用服务器 (已经装好 `docker`)
- 一台云服务器（已经装好 `docker` ）

## 3. 搭建

### 3.1. frp server 搭建
1. 创建配置文件，即 frps.toml 文件

    ```shell
    mkdir -p /data/frps
    cd /data/frps
    vim frps.toml
    ```

2. frps.toml 内容
    ```properties
    [common]
    # 监听端口
    bind_port = 7000
    # 面板端口
    dashboard_port = web ui 的暴露端口
    # 登录面板账号设置
    # 用户名
    dashboard_user = 登录用户名
    # 密码
    dashboard_pwd = 登录用户密码
    # 设置http及https协议下代理端口（非重要）
    vhost_http_port = 7080
    vhost_https_port = 7081
    
    # 身份验证 token ; 客户端需要
    token = 随机字符串 客户需要这里的 token
    ```

4. 创建 frps 容器
    ```shell
    # 先拉取镜像
    docker pull snowdreamtech/frps
    # 运行 -v 参数：这里 -v 挂载，是你的配置文件所在位置
    docker run \
    --restart=always \
    --network host -d \
    -v /app/frps/frps.toml:/etc/frp/frps.toml \
    --name frps snowdreamtech/frps
    # 检查是否正常运行
    docker ps -a 
    ```

### 3.2. frp client 搭建

1. 同理，frpc.toml 编写
    ```properties
    [common]
    # server_addr为FRPS服务器IP地址
    server_addr = frp server ip
    # server_port为服务端监听端口，bind_port，与frps.ini中保存一致
    server_port = 7000
    # 身份验证，与frps.toml中保存一致
    token = 上面服务器端的 token
    
    [ssh]
    type = tcp
    local_ip = 127.0.0.1
    local_port = 22
    remote_port = 2288
    
    # [ssh] 为服务名称，下方此处设置为，访问frp服务段的2288端口时，等同于通过中转服务器访问127.0.0.1的22端口。
    # type 为连接的类型，此处为tcp
    # local_ip 为中转客户端实际访问的IP 
    # local_port 为目标端口
    # remote_port 为远程端口
    ```

2. 创建容器
    ```shell
    # 拉取镜像
    docker pull snowdreamtech/frpc
    
    # -v 参数挂载修改
    docker run --restart=always \
    --network host -d \
    -v /data/frpc/frpc.toml:/etc/frp/frpc.toml \
    --name frpc snowdreamtech/frpc
    
    # 检查运行
    docker ps -a
    ```
