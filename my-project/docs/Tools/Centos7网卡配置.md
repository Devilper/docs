## 								Centos7网卡配置

一、 自动获取动态IP地址

二、配置静态IP地址

三、修改网卡注意事项

四、基础知识

以下实例全部基于VM虚拟机操作

一、 自动获取动态IP地址
1.输入命令"ip addr"，查看IP地址，右下图可以发现只有一张名为ens33的网卡

2.输入“cd /etc/sysconfig/network-scripts/”按回车键确定，继续输入“ls”按回车键查看文件，需要配置的文件为 ifcfg-网卡名（ 注：ifcfg-lo为网络回环文件）

3.输入“vi ifcfg-ens33”或“vi /etc/sysconfig/network-scripts/ifcfg-ens33”编辑网卡文件（网卡名称不确定时可以输入“/etc/sysconfig/network-scripts/ifcfg-”双击Tab键进行命令提示）

4.查看最后一项（蓝色框内），发现为“ONBOOT=no”。

5.按“i”键进入编辑状态，将最后一行“no”修改为“yes”，然后按“ESC”键退出编辑状态，并输入“:x”保存退出。

6.输入“service network restart”或“systemctl restart netwrok”重启网络服务。

7.再次输入“ip addr”查看，现已可自动获取IP地址。


二、配置静态IP地址
1.同样以“ifcfg-ens33”网卡为例，配置“ifcfg-ens33”文件
2.按“i”进入编辑状态，设置为“BOOTPROTO=‘static’”（如设置为none则禁用网卡，static则启用静态IP地址，设置为dhcp则为开启DHCP服务），并修改其他选项。
本例中
IPADDR=192.168.1.200
GATEWAY=192.168.1.1
PREFIX=24
注：NM_CONTROLLED=no和ONBOOT=yes可根据您的需求进行设置。
NM_CONTROLLED是network manger的参数，实时生效，修改后无需要重启网卡立即生效。
ONBOOT=yes 开机自启动网卡。

3.确认无误后按“ESC”退出编辑状态，并输入“:x”保存退出，输入“service network restart”重启服务后输入“ip addr”查看网络配置。

4.如需DNS解析服务，则可以在配置网卡文件时加入DNS1、DNS2等等，或修改 “/etc/resolv.conf”文件。
假设这是外网IP

~~~
IPADDR=192.168.1.200
GATEWAY=192.168.1.1
PREFIX=24
DNS1=114.114.114.114
或

vi /etc/resolv.conf

nameserver 114.114.114.114
~~~


三、修改网卡注意事项
配置动态IP地址时，只需修改“BOOTPROTO=、ONBOOT=”选项
配置静态IP地址时，只需修改“BOOTPROTO=、ONBOOT=”选项，
并添加“IPADDR=、GATEWAY=、PREFIX=”选项
其他选项若没需求最好不要改，不然容易造成重启网卡失败
同时，重启网卡失败时注意检查/etc/sysconfig/network-scripts/目录下有自己误保存的文件

四、基础知识
/etc/host.conf	配置域名服务客户端的控制文件
/etc/hosts	完成主机名映射为IP地址的功能
/etc/resolv.conf	域名服务客户端的配置文件,用于指定域名服务器的位置
/etc/sysconfig/network	包含了主机最基本的网络信息,用于系统启动
/etc/sysconfig/network-script/	系统启动时初始化网络的一些信息以及网卡的配置文件
/etc/xinetd.conf	定义了由超级进程xinetd启动的网络服务
/etc/networks	完成域名与网络地址的映射
/etc/protocols	设定了主机使用的协议以及各个协议的协议号
/etc/services	设定主机的不同端口的网络服务


TYPE=Ethernet	类型
BOOTPROTO=none	设置为none禁止DHCP，设置为static启用静态IP地址，设置为dhcp开启DHCP服务
NETMASK=255.255.255.0	子网掩码
PREFIX = 24	子网掩码
PEERDNS	是否允许DHCP获得的DNS覆盖本地的DNS
PEERROUTES	是否从DHCP服务器获取用于定义接口的默认网关的信息的路由表条目
UUID	唯一标识
GATEWAY=	设置网关
IPV6INIT=no	禁止IPV6
IPV4_FAILURE_FATAL=yes	如果ipv4配置失败禁用设备
IPV6_FAILURE_FATAL=yes	如果ipv6配置失败禁用设备
NAME=“eth 或 ens”	定义设备名称
BROADCAST=“address”	address表示广播地址
MACADDR=“MAC-address”	MAC-address表示指定一个MAC地址
USERCTL=yes/no	是否允许非root用户控制该设备
ONBOOT=	是否开机自启
可以自己添加的选项：

DNS1=	DNS解析服务
IPADDR=	静态IP地址
GATEWAY=	网关

