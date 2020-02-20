## rdesktop使用准则

~~~shell
rdesktop ip // 打开一个8彩色位的
~~~

~~~shell
rdesktop -a 16 ip //打开16彩色位的
~~~

~~~shell
rdesktop -u `用户名` -p `密码` -a 16 ip //直接登入 
~~~

~~~shell
rdesktop -u `用户名` -p `密码` -a 16 -f ip // 全屏
~~~

~~~shell
rdesktop -u `用户名` -p `密码` -a 16 -f -r sound:local ip // 包含声音
~~~

~~~shell
rdesktop -u `用户名` -p `密码` -a 16 -f -r disk:floppy=/mnt/floppy ip //远程共享磁盘 
~~~

