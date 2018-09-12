1. 第一步是先看下自己服务器对应的正在使用的网卡地址，左面对应的是网络配置文件中配置的名字，后面会讲到

[daniel@localhost ~]$ ifconfig 

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9B%B8%E5%85%B3/clipboard.png?raw=true)

2.找到对应的网络配置文件

\# vim /etc/sysconfig/network-scripts/ifcfg-+上面那个第一红方框中的文件名

3.主要修改的内容如下

BOOTPROTO="static" #dhcp改为static   

ONBOOT="yes" #开机启用本配置  

IPADDR=192.168.7.106 #静态IP  

GATEWAY=192.168.7.1 #默认网关  

NETMASK=255.255.255.0 #子网掩码  

DNS1=192.168.7.1 #DNS 配置

4.修改后的效果

![img](E:/%E6%9D%82%E4%B8%83%E6%9D%82%E5%85%AB/Youdao/polieme@126.com/de93d089ba06436aa7ff439d096677b5/clipboard.png)

5.重启网络服务

\#service network restart

6.查看改动后的效果，Centois 7 不再使用 ifconfig 而是用 ip 命令查看网络信息。

![img](E:/%E6%9D%82%E4%B8%83%E6%9D%82%E5%85%AB/Youdao/polieme@126.com/ff345edc6c504759a7b65258dd945a16/clipboard.png)