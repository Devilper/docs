deepin安装Postman



1、官网下载Linux软件包:

https://www.getpostman.com/apps

2、将安装包移到想要安装的目录下

~~~shell
mv .Postman-linux-x64-6.4.4.tar.gz /opt/
~~~

3、解压安装

```
`sudo` `tar` `-xzvf Postman-linux-x64-6.4.4.``tar``.gz`
```

3、进入解压后的 Postman文件夹打开终端，启动 Postman

```
`.``/Postman/Postman`
```

4、建立软链接，创建解压后的 Postman 文件中的 Postman 到 /usr/bin/ 目录下

```
`sudo` `ln` `-s ``/alidata/server/Postman/Postman` `/usr/bin/`
```