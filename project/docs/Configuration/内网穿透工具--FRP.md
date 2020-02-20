## 内网穿透工具--FRP

#### 1.安装

~~~shell
 # github地址 https://github.com/fatedier/frp/releases
 
 wget https://github.com/fatedier/frp/releases/download/v0.15.1/frp_0.15.1_linux_amd64.tar.gz
 tar xzvf frp_0.15.1_linux_amd64.tar.gz
 mv frp_0.15.1_linux_amd64 frp
~~~

#### 2.FRP 服务端配置

​	修改服务端简版配置文件 frps.ini

~~~shell
# 配置如下
[common]
# 服务端监听端口,默认为7000,可根据实际情况修改
bind_port = 7000
# HTTP访问端口,根据自己实际情况定义(可选)
vhost_http_port = 8080
# HTTPS访问端口，根据自己实际情况定义(可选)
vhost_gttps_port = 8080
~~~

​	服务端启动指令

~~~shell
# 在安装目录下执行
./frps -c ./frps.ini
~~~

#### 3.FRP客户端配置

​	修改客户端简版配置文件frpc.ini

~~~shell
# 配置如下
[common]
# server_addr 为 FRP 服务端的公网 IP
server_addr = x.x.x.x
# server_port 为 FRP 服务端监听的端口
server_port = 7000

# ssh 配置
[ssh]
# 类型
type = tcp
# 本地ip
local_ip = 127.0.0.1
# 本地转发端口
local_port = 22
# 远端端口
remote_port = 6000

# 通过域名访问内网Web服务
[web]
# 通过http协议转发
type = http
# 本地web服务对应的端口
local_port = 80
# 自定义域名(需要此域名绑定远端服务器)
custom_domains = **.**.com

# 设置认证的用户名
http_user = ***
# 设置认证的密码
http_pwd = ***
~~~

​	客户端启动命令

~~~shell
# 在安装目录下
./frpc -c ./frpc.ini
~~~

​	ssh连接内网服务器

~~~shell
ssh -oPort=6000 mike@4.3.2.1
# 6000     在frp上注册的映射端口
# mike     内网服务器用户名
# 4.3.2.1  公网IP
~~~



#### 3.通过systemctl控制启动

创建`sudo  vim /lib/systemd/system/frps.service` frps.service 文件

在frps.service里写入以下内容

~~~shell
[Unit]
Description=fraps service
After=network.target syslog.target
Wants=network.target

[Service]
Type=simple
#启动服务的命令（此处写你的frps的实际安装目录）
ExecStart=/your/path/frps -c /your/path/frps.ini

[Install]
WantedBy=multi-user.target
~~~

然后就启动frps 
`sudo systemctl start frps` 
再打开自启动 
`sudo systemctl enable frps`

如果要重启应用，可以这样，`sudo systemctl restart frps`
如果要停止应用，可以输入，`sudo systemctl stop frps`
如果要查看应用的日志，可以输入，`sudo systemctl status frps`
