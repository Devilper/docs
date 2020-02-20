## 《Linux就该这么学》—学习笔记

1.Yum仓库的配置文件都以.repo结尾并存放在/etc/yum/repos.d/的目录中

~~~shell
[rhel-media]: yum源的名称，可自定义
baseurl=file：///media/cdrom: 提供方式包括FTP(ftp://..)、HTTP（http://.）、本地(file:///...)
enalbed=1：设置此源是否可用，1为可用,0为禁用。
gpgcheck=1:设置此源是否校验文件，1为校验，0为不校验。
gpgkey=file:///media/cdrom/RPM-GPG-KEY-redhat-release：若为校验请指定公钥文件地址。
~~~

2.Yum仓库指令

| 命令                      | 作用                         |
| ------------------------- | ---------------------------- |
| yum repolist all          | 列出所有仓库                 |
| yum list all              | 列出仓库所有软件包           |
| yum info 软件包名称       | 查看软件包信息               |
| yum install 软件包名称    | 安装软件包                   |
| yum reinsyall 软件包名称  | 重新安装软件包               |
| yum update 软件包名称     | 升级软件包                   |
| yum remove 软件包         | 移除软件包                   |
| yum clean all             | 清除所有仓库缓存             |
| yum check-update          | 检查可更新的软件包           |
| yum grouplist             | 查看系统中已经安装的软件包组 |
| yum groupinstall 软件包组 | 安装指定的软件包组           |
| yum groupremove 软件包组  | 移除指定的软件包组           |
| yum groupinfo 软件包组    | 查询指定的软件包组信息       |

### 二、新手必须掌握的Linux命令

#### 1.echo

~~~shell
devilper@devilper_pc:~$ echo Linux
Linux
devilper@devilper-pc:~$ echo $HOSTNAME
devilper-pc

~~~

#### 2.date

参数

| 参数 | 作用           |
| ---- | -------------- |
| %t   | [TAB键]        |
| %H   | 小时(24制)     |
| %I   | 小时(12制)     |
| %M   | 分钟           |
| %S   | 秒             |
| %X   | 相当于%H:%M:%S |
| %Z   | 显示时区       |
| %p   | 显示本地AM或PM |
| %A   | 星期几         |
| %a   | 星期几         |
| %B   | 完整月份       |
| %b   | 缩写月份       |
| %d   | 日             |
| %j   | 一年中的第几天 |
| %m   | 月份           |
| %Y   | 完整的年份     |

~~~shell
# 查看当前的系统时间
devilper@devilper-PC:~$ date
2019年 09月 17日 星期二 21:15:31 CST
# 按照格式显示时间
devilper@devilper-PC:~$ date "+%Y-%m-%d %H:%M:%S"
2019-09-17 21:36:20
# 设置系统时间
devilper@devilper-PC:~$ sudo date -s "20200101 8:30:00"
2020年 01月 01日 星期三 08:30:00 CST
# 查看本地系统时区
devilper@devilper-PC:~$ date "+%Z"
CST
# 查看星期几
devilper@devilper-PC:~$ date "+%A"
星期二
# 查看上午还是下午
devilper@devilper-PC:~$ date "+%p"
下午
# 判断今天是一年中的第几天
devilper@devilper-PC:~$ date "+%j"
260
~~~

#### 3.wget

| 参数 | 作用                                 |
| ---- | ------------------------------------ |
| -b   | 后台下载模式                         |
| -O   | 下载到指定目录                       |
| -t   | 最大尝试次数                         |
| -c   | 断点续传                             |
| -p   | 下载页面内所有资源，包括图片、视频等 |
| -r   | 递归下载                             |

#### 4.uptime(查看系统负载情况)

~~~shel
[root@c6d479852832 /]# uptime
 14:10:49 up 3 days,  9:42,  0 users,  load average: 4.28, 4.19, 3.28
~~~

#### 5.free(显示当前系统中内存使用情况)

~~~shell
[root@c6d479852832 /]# free -m
              total        used        free      shared  buff/cache   available
Mem:           7867        2538         710        2222        4618        2678
Swap:         11263         672       10591

~~~

#### 6.who(查看当前登入主机的用户情况)

~~~shell
devilper@devilper-PC:~$ who
devilper tty1         2019-09-14 12:33 (:0)
~~~

#### 7.last(查看所有系统的登入记录)

~~~shell
devilper@devilper-PC:~$ last
devilper tty1         :0               Sat Sep 14 12:33   still logged in
reboot   system boot  4.15.0-30deepin- Sat Sep 14 12:28   still running
devilper tty1         :0               Thu Sep 12 23:16 - 12:27 (1+13:11)
reboot   system boot  4.15.0-30deepin- Thu Sep 12 23:15 - 12:27 (1+13:12)
devilper tty1         :0               Thu Sep 12 22:50 - 23:15  (00:24)
reboot   system boot  4.15.0-30deepin- Thu Sep 12 22:48 - 23:15  (00:26)
devilper tty1         :0               Thu Sep 12 22:47 - 22:48  (00:00)
reboot   system boot  4.15.0-30deepin- Thu Sep 12 22:47 - 22:48  (00:00)
devilper tty1         :0               Thu Sep 12 06:53 - down   (00:54)
reboot   system boot  4.15.0-30deepin- Thu Sep 12 06:53 - 07:48  (00:54)
devilper tty1         :0               Wed Sep 11 23:24 - 23:32  (00:08)
reboot   system boot  4.15.0-30deepin- Wed Sep 11 23:23 - 23:32  (00:08)
devilper tty1         :0               Wed Sep 11 23:19 - 23:23  (00:04)
reboot   system boot  4.15.0-30deepin- Wed Sep 11 23:19 - 23:23  (00:04)
devilper tty1         :0               Wed Sep 11 23:11 - 23:18  (00:06)
reboot   system boot  4.15.0-30deepin- Wed Sep 11 23:10 - 23:18  (00:08)

wtmp begins Wed Sep 11 23:10:20 2019

~~~

#### 8.od(查看特殊格式的文件，格式为：“od[选项]\[文件]”)

| 参数 | 作用      |
| ---- | --------- |
| -t a | 默认字符  |
| -t c | ASCII字符 |
| -t o | 八进制    |
| -t d | 十进制    |
| -t x | 十六进制  |
| -t f | 浮点数    |

#### 9.tr(用于转换文本文件中的字符,格式为:"tr[原是字符]\[目标字符]")

~~~shell
[root@c6d479852832 opt]# cat tr.txt | tr[a-z] [A-Z]
~~~

#### 10.wc(用于统计指定文本的行数、字数、字节数,格式为“wc[参数]文本”)

| 参数 | 作用         |
| ---- | ------------ |
| -l   | 只显示行数   |
| -w   | 只显示单词数 |
| -c   | 只显示字节数 |

#### 11.cut(通过列来提取文本字符，格式为:"cut[参数] 文本")

| 参数      | 作用                  |
| --------- | --------------------- |
| -d 分隔符 | 指定分隔符，默认为Tab |
| -f        | 指定显示的列数        |
| -c        | 单位改为字符          |

~~~shell
# 获取root用户的默认SHELL解释器
[root@c6d479852832 opt]# grep ^root /etc/passwd | cut -d: -f7
/bin/bash
~~~

#### 12.diff(比较多个文件的差异,格式为: "diff[参数] 文件")

| 参数         | 作用               |
| ------------ | ------------------ |
| -b           | 忽略空格引起的差异 |
| -B           | 忽略空行引起的差异 |
| --brief 或-q | 仅报告是否存在差异 |
| -c           | 使用上下文输出格式 |

#### 12.touch(创建空白文件与修改文件时间，格式为:"touch [选项]\[文件]")

| 参数 | 作用                       |
| ---- | -------------------------- |
| -a   | 近修改"访问时间"(atime)    |
| -m   | 近修改"更改时间"(mtime)    |
| -d   | 同事修改atime和mtime       |
| -t   | 要修改成的时间[YYMMDDhhmm] |

#### 13.mkdir(创建空白的文件夹，格式为:"mkdir[选项]目录")

| 参数    | 作用                                   |
| ------- | -------------------------------------- |
| -m=MODE | 默认的文件目录权限，如“-m 755”         |
| -p      | 连续创建多层目录(若文件夹已存在则忽略) |
| -v      | 显示创建的过程                         |

#### 14.cp(复制文件或目录，格式为:"cp[选项] 源文件 目标文件")

| 参数 | 作用                                         |
| ---- | -------------------------------------------- |
| -p   | 保留原始文件的属性                           |
| -d   | 若对象为“链接文件”，则保留该“链接文件”的属性 |
| -r   | 递归持续复制(用于目录)                       |
| -a   | 相当于-pdr                                   |

#### 15.dd(指定大小的拷贝的文件或指定转换文件，格式为:"dd[参数]")

| 参数       | 作用                   |
| ---------- | ---------------------- |
| if         | 输入的文件名称         |
| of         | 输出的文件名称         |
| bs         | 设置每个“块”的大小     |
| count      | 设置要拷贝"块"的个数   |
| conv=ucase | 将字母从小写转换为大写 |
| conv=lcase | 将字母从大写转换为小写 |

~~~SHELL
# 将硬盘的MBR信息拷贝出来
[root@c6d479852832 ~]# dd if=/dev/sda of=sda_image count=1 bs=512k
~~~

#### 16.useradd(创建新用户，格式为："useradd[选项] 用户名")

| 参数 | 作用                                   |
| ---- | -------------------------------------- |
| -d   | 指定用户的家目录(默认为/home/username) |
| -D   | 展示默认值                             |
| -e   | 账号有效截止日期，格式：YYYY-MM-DD     |
| -g   | 指定一个初始用户组(必须已存在)         |
| -G   | 指定一个或多个扩展用户组               |
| -N   | 不创建与用户同名的用户组               |
| -s   | 指定默认的Shell                        |
| -u   | 指定用户的UID                          |

~~~SHELL
# 创建名为linuxprobe的用户，并定义家目录路径、UID以及登录解释器(不允许登录)
[root@linxprobe~]# useradd -d /home/linux -u 8888 -s /sbin/nologin linuxprobe
~~~

#### 17.passwd(修改用户的密码，格式为:passwd[选项]\[用户名])

| 参数    | 作用                                                         |
| ------- | ------------------------------------------------------------ |
| -l      | 锁定用户禁止其登录                                           |
| -u      | 解除锁定，允许用户登录                                       |
| --stdin | 允许从标准输入修改用户密码，如(echo "NewPassWord"\|passwd -stdin Username) |
| -d      | 使账号无密码                                                 |
| -e      | 强制用户下次登录时修改密码                                   |
| -S      | 显示用户的密码状态                                           |

#### 18.userdel(删除用户所有表格，格式为:"userdel[选项]用户名")

| 参数 | 作用                             |
| ---- | -------------------------------- |
| -f   | 强制删除用户，家目录与其相关文件 |
| -r   | 同时删除用户，家目录与其相关文件 |

#### 19.usermod(修改用户的属性，格式为"usermod[选项]用户名")

| 参数  | 作用                                                         |
| ----- | ------------------------------------------------------------ |
| -c    | 填写账号的备注信息                                           |
| -d -m | -m 与-d 连用，可重新指定用户的家目录并自动将旧的数据转移过去 |
| -e    | 账户到期时间，格式“YYYY-MM-DD”                               |
| -g    | 变更所属用户组                                               |
| -G    | 变更扩展用户组                                               |
| -L    | 锁定用户禁止其登录系统                                       |
| -U    | 解锁用户，允许其登录系统                                     |
| -s    | 变更默认终端                                                 |
| -u    | 修改用户的UID                                                |

#### 20.groupadd(创建群组，格式为："groupadd[选项]群组名")

~~~shell
# 创建名称为linuxprobe的用户群组
[root@linuxprobe~]# groupadd linuxprobe
~~~

#### 21.tar(文件打包压缩或解压，格式为:"tar[选项]\[文件]")

| 参数 | 作用                   |      |
| ---- | ---------------------- | ---- |
| -c   | 创建压缩文件           |      |
| -x   | 解开压缩文件           |      |
| -t   | 查看压缩包内有那些文件 |      |
| -z   | 用Gzip压缩或解压       |      |
| -j   | 用bzip2压缩或解压      |      |
| -v   | 显示压缩或解压的过程   |      |
| -f   | 目标文件名             |      |
| -p   | 保留原始的权限与属性   |      |
| -P   | 使用绝对路径来压缩     |      |
| -C   | 指定解压到的目录       |      |

#### 22.grep(文本进行搜索，格式为:"grep[选项]\[文件]")

| 参数 | 作用                                         |
| ---- | -------------------------------------------- |
| -b   | 将可执行文件(binary)当做文本文件(text)来搜索 |
| -c   | 仅显示找到的次数                             |
| -i   | 忽略大小写                                   |
| -n   | 显示行号                                     |
| -v   | 反向选择——仅列出没有"关键词"的行             |

~~~shell
# 搜索在/etc/passwd 中“/sbin/nologin”出现的行，找出系统中不允许登录的用户
[root@linuxprobe~]# grep /sbin/nologin /etc/passwd
~~~

#### 23.find(查找文件，格式为:"find[查找路径]寻找条件 操作")

| 参数               | 作用                                                         |
| ------------------ | ------------------------------------------------------------ |
| -name              | 匹配名称                                                     |
| -perm              | 匹配权限(mode为完全匹配，-model为包含匹配)                   |
| -user              | 匹配所有者                                                   |
| -group             | 匹配所有组                                                   |
| -mtime -n +n       | 匹配修改内容的时间(-n 指n天以内，+n指n天以前)                |
| -atime -n +n       | 匹配访问文件的时间(-n 指n天以内，+n指n天以前)                |
| -ctime -n +n       | 匹配修改权限的时间(-n 指n天以内，+n指n天以前)                |
| -nouser            | 匹配无所有者的文件                                           |
| -nogroup           | 匹配无所有组的文件                                           |
| -newer f1 !f2      | 匹配比文件f1新却比f2旧的文件                                 |
| --type b/d/c/p/l/f | 匹配文件类型(块设备、目录、字符设备、管道、链接文件、文件文件) |
| -size              | 匹配文件的大小(+50k查找超过50k的文件，而-50k则代表查找小于50K的文件) |
| -prune             | 忽略某个文件                                                 |
| --exec{}\;         | 后面可接对搜索到结果进一步处理的命令                         |

~~~shell
#搜索在/etc/中所有以host开头的文件
[root@linuxprobe~]# find /etc -name "host*" -print
~~~

### 三、管道符、重定向域环境变量

#### 1.管道符

~~~shell
# 统计所有不允许登录系统的用户个数
[root@linuxprobe~]# grep "/sbin/nologin" /etc.passwd | wc-l
~~~

