1、登录Linux系统，打开终端，输入以下命令：

vi /etc/ssh/sshd_config

2、在打开的文件中，拉动鼠标到最后一行，可能会出现以下2种情况:

1)UsePAM yes UseDNS yes

2)UsePAM yes

此时将UseDNS yes修改为UseDNS no，没有的则加上这一行，便可。