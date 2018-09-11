Windows添加开机启动，很简单，但是Linux呢，这两天学习了一下，通过添加/etc/rc.local文件启动，但是据说这个方法很快就要被废掉了，因此又研究了一下添加系统服务，做成开机启动，这种启动方式是可以在开机之后不登录，就能启动服务的，好用！！

1. 编辑service文件（文件存储在/lib/systemd/system/xxxx.service）

vim /lib/systemd/system/nginx.service

2.将一下内容拷贝进nginx.service文件中

[Unit]  Description=nginx  After=network.target 

 [Service]  Type=forking  ExecStart=/usr/local/nginx/sbin/nginx  ExecReload=/usr/local/nginx/sbin/nginx -s reload  ExecStop=/usr/local/nginx/sbin/nginx -s quit PrivateTmp=true   [Install]  WantedBy=multi-user.target



相关说明：

[Unit]: 服务的说明

Description:描述服务

After:描述服务类别

[Service]服务运行参数的设置

Type=forking是后台运行的形式

ExecStart为服务的具体运行命令

ExecReload为重启命令

ExecStop为停止命令

PrivateTmp=True表示给服务分配独立的临时空间

注意：[Service]的启动、重启、停止命令全部要求使用绝对路径

[Install]运行级别下服务安装的相关设置，可设置为多用户，即系统运行级别为3

保存退出。



3.设置开机启动

systemctl enable nginx.service

4.其他启动指令

启动nginx服务：systemctl start nginx.service

设置开机自启动：systemctl enable nginx.service

停止开机自启动：systemctl disable nginx.service

查看服务当前状态：systemctl status nginx.service

重新启动服务：systemctl restart nginx.service

查看所有已启动的服务：systemctl list-units --type=service