# SFTP 部署手册

## 1. SFTP 搭建手册

### 1.1. 查看 SSH 服务

```ssh
root@test:/home/test# systemctl status sshd
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since Sun 2024-12-08 15:30:18 UTC; 1min 45s ago
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 1378 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 1379 (sshd)
      Tasks: 1 (limit: 4563)
     Memory: 5.2M
        CPU: 25ms
     CGroup: /system.slice/ssh.service
             └─1379 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

Dec 08 15:30:18 test systemd[1]: Starting OpenBSD Secure Shell server...
Dec 08 15:30:18 test sshd[1379]: Server listening on 0.0.0.0 port 22.
Dec 08 15:30:18 test sshd[1379]: Server listening on :: port 22.
Dec 08 15:30:18 test systemd[1]: Started OpenBSD Secure Shell server.
Dec 08 15:31:32 test sshd[1711]: Accepted password for test from 192.168.5.11 port 55939 ssh2
Dec 08 15:31:32 test sshd[1711]: pam_unix(sshd:session): session opened for user test(uid=1000) by (uid=0)
```

### 1.2. 创建

```shell
# 1. 创建相关用户组
root@test:/home/test# groupadd sftpuser
# 2. 创建目录
root@test:/home/test# mkdir /sftp
# 3. 千万注意：目录根必须要为 root 和 root 用户组
root@test:/# chown -R root:root /sftp
# 4. 添加用户目录及用户
root@test:/# cd /sftp/ && mkdir testuser
root@test:/sftp# useradd -g sftpuser -d /sftp/testuser/ -M -s /sbin/nologin testuser
root@test:/sftp# passwd testuser
# 5. 目录赋权；
root@test:/sftp# chown -R testuser:sftpuser ./testuser/
root@test:/sftp# chmod -R 755 /sftp/testuser/

# 6. 修改 sshd_config 文件
root@test:/sftp# vim /etc/ssh/sshd_config
# 注释这行
# Subsystem       sftp    /usr/lib/openssh/sftp-server
# 文件尾部追加追加
Subsystem sftp internal-sftp # 使用内部的 sftp 
Match User testuser # 匹配 testuser 用户；如果为 Group 则代表组匹配；
    ChrootDirectory /sftp/%u # 根目录；%u 匹配用户
    ForceCommand internal-sftp # 指定 ftp 命令
    AllowTcpForwarding no 
    X11Forwarding no
# 7. 重启
root@test:/sftp# systemctl restart sshd
```

### 1.3. 注意点

1.   `sftp` 的上级目录必须要是 `root` 用户的；在此处示例：`/sftp` 则就需要为 `root` 的；如果是 `/data/sftp` 那么，则相关联的上级目录，都必须要为 `root` ；且权限设置最大只可以为`755` ；
2.   `chown -R testuser:sftpuser ./testuser/` 如果没有这行命令，那么 `testuser` 只会有只读权限，从而无法创建；
3.   如果想要只读，不给写权限，你可以创建 `testuserr` 用户，设置 `/sftp/testuserr` 为 `ChrootDirectory` ，这样在 `755` 情况下，只会读，不会写；
4.   `%u` 可以进行匹配；`sftp` 目录不可以设置 `777` ；超过 `755` 就会出错；
5.   `sftp` 中用户名密码无法登录：`/etc/ssh/sshd_config` 密码配置为 `yes` ；

## 2. SFTP 和 SSH 分离端口

### 2.1. 原因

&emsp;&emsp;在日常使用，可能要求，`ssh` 是一个端口，但是 `sftp` 是别地端口，且 `sftp` 端口不给 `ssh` 登录，以保证安全；

### 2.2. 设置步奏

```shell
# 在 centos 7.9.2009 版本设置
# 拷贝 sshd 服务做 sftpd
cp /usr/lib/systemd/system/sshd.service  /etc/systemd/system/sftpd.service
# 拷贝 pam 配置文件
cp /etc/pam.d/sshd  /etc/pam.d/sftpd
# 拷贝 sshd config 配置
cp /etc/ssh/sshd_config  /etc/ssh/sftpd_config
# 进行软链接
ln -sf  /usr/sbin/service  /usr/sbin/rcsftpd
ln -sf  /usr/sbin/sshd  /usr/sbin/sftpd

# 复制相关文件
cp /etc/sysconfig/sshd  /etc/sysconfig/sftp
cp /var/run/sshd.pid  /var/run/sftpd.pid
# 编辑 service 文件
vim /etc/systemd/system/sftpd.service
# 修改 [unit]
Description=sftpd server daemon
# 修改 [service]
Type=notify
EnvironmentFile=/etc/sysconfig/sftp
ExecStart=/usr/sbin/sftpd -f /etc/ssh/sftpd_config

# 配置 sftp 的文件；修改端口等...基本；后续配置 sftp 用户和目录也在这个目录里面；
vim /etc/ssh/sftpd_config
	Port : 修改端口
	PermitRootLogin : true : 禁止 root 登录
	PidFile: /var/run/sftpd.pid 修改复制出来的 pid 文件


```

### 2.3. 后续

&emsp;&emsp;后面就是配置 sftp 即可了；

### 2.4. 注意：

-   白名单：配置：`AllowUsers: xxx` 
-   黑名单：配置：`DenyUsers: xxx`

## 3. 参考链接

[转向：Centos7 创建 sftp 用户](https://www.snycloud.com/archives/centos7%E5%88%9B%E5%BB%BAsftp%E7%94%A8%E6%88%B7%E5%B9%B6%E6%8C%87%E5%AE%9A%E8%AE%BF%E9%97%AE%E7%89%B9%E5%AE%9A%E7%9B%AE%E5%BD%95md)

[转向：Linux 7.5 SSH 与 SFTP 分离](https://www.cnblogs.com/qinyl/p/12194105.html)
