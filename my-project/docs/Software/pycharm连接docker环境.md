## pycharm 使用docker 环境

1.创建或拉取docker镜像

2.设置docker端口,需要在service 文件中设置

~~~shell
# 通过命令查看docker开放的端口，一般docker不自动开放
devilper@devilper-PC:~$ sudo netstat -tulnp | grep docker
devilper@devilper-PC:~$ 
# 没有查到docker开放的端口
~~~

![](/home/devilper/Desktop/net_docker.png)

~~~shell
# 通过命令查看docker.service文件的位置
● docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: active (running) since Sat 2019-09-14 10:59:25 CST; 9min ago
     Docs: https://docs.docker.com
 Main PID: 8137 (dockerd)
    Tasks: 13
   Memory: 147.2M
      CPU: 550ms
   CGroup: /system.slice/docker.service
           └─8137 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

~~~

![](/home/devilper/Desktop/systemctl status.png)

~~~shell
# 通过编辑器打开docker.service文件
# 在第14行 ExecStart=/usr/bin/dockerd -H fd:// --contarinerd=/rin/containerd/containerd.sock进行修改
# 在/usr/bin/dockerd 后面加上 -H tcp：//0.0.0.0:2375(端口自定义)
# ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:2375 -H fd:// --contarinerd=/rin/containerd/containerd.sock
# 保存退出
~~~

![](/home/devilper/Desktop/modify.png)

3. systemctl daemon-reload      #重载service文件

4. systemctl restart docker     #重启docker service

5. 再次查询监听端口 sudo netstat -tulnp | grep docker

   ~~~shell
   devilper@devilper-PC:~$ sudo netstat -tulnp | grep docker
   tcp6       0      0 :::2375                 :::*                    LISTEN      10777/dockerd       
   devilper@devilper-PC:~$ 
   # 已经在监听2375端口了
   ~~~

6. pycharm 连接docker

   ~~~shell
   File——>Settings——>Build,Execution,Deployment——>Docker
   点击`+`号，选择`TCP socket` 在`Engine API URL`中填入docker宿主机的ip和端口号
   显示`Connection successful`就完成了
   ~~~

7. 在Project Interpreter 中选择 docker镜像

8. 设置 Edit Configurations

   ~~~shell
   `host`一栏填写 0.0.0.0
   `python interpreter` 一栏填写 docker镜像环境
   ~~~

   

错误

~~~
Job for docker.service failed because the control process exited with error code.
See "systemctl status docker.service" and "journalctl -xe" for details.
~~~

