## 首先是下载  
- 打开mysql的官网  
  [mysql下载地址](https://www.mysql.com/)  
- 找到顶部的DOWNLOADS ，如果地址没换的话，应该是下面这个地址  
  [下载地址](https://www.mysql.com/downloads/)  
- 选择社区版本（Community），然后选择左侧的菜单中的MySQL Community Server
- 滑动滚轮，向下，一直到选择系统和下载版本
- 选择完之后选择列表中展示的（ZIP Archive）版本的进行下载，我下载的版本是5.7.20，下载完成成解压
------
## 添加环境变量  
- 首先是添加MYSQL_HOME，设置的VALUE值是MYSQL的解压目录，我是解压在了D:\Program Files\mysql，所以对应的MYSQL_HOME就是这个值  
- 设置PATH  
  在PATH的最后添加%MYSQL_HOME%\bin;
------

## 配置文件  
- 在mysql文件夹下，新建一个my.ini的文件**此处需要注意：保存文件的编码集一定是ANSI，这个地方不要用记事本编辑，记事本默认是UTF-8，因为他是个坑，用专业的Notepad++ 或者UE进行编辑**，具体my.ini的内容如下,内容解释下面的文件中都已经有了，就不再废话了，另外这个地方先开启skip-grant-tables是为了给root修改密码
```properties
[mysqld]
basedir=D:\Program Files\mysql
datadir=D:\Program Files\mysql\data\
port=3306
skip-grant-tables
#basedir表示mysql安装路径
#datadir表示mysql数据文件存储路径
#port表示mysql端口
#skip-grant-tables表示忽略密码
```
------
## 安装
- 然后以管理员的权限进入cmd窗口界面，管理员权限进入方式：搜索cmd，右键在对应程序上，以管理员的权限启动
- 切换到mysql/bin文件夹下，也就是你解压的出来的文件夹的bin目录下，怎么切换我就不讲了 各种cd，然后执行命令，命令如下，执行完成后会显示“Service successfully installed”
```shell
mysqld --install
```
- 生成data数据。不要着急于启动，先生成mysql的data数据，上面的my.cnf中设置了datadir=D:\Program Files\mysql\data\，因此我们需要先手动在mysql文件夹下面新建一个data文件夹，否则接下来的步骤会报错
```shell
mysqld --initialize-insecure --user=mysql;
```
- 然后看下data目录下会生成一堆文件夹和文件
------
## 启动
- 在刚刚的cmd窗口中直接输入 net start mysql，然后会提示启动成功
```
net start mysql
```
------
## 登录
- 输入命令mysql -u root -p，这个时候是没有密码的，所以输入完之后直接回车，就可以进入mysql中了
```shell
mysql -u root -p
```
------

## 更新密码
- 输入以下命令修改密码，当然密码需要修改成你自己想要修改的内容,再就是刷新下quanxian
```sql
update mysql.user set authentication_string=password('123456789') where user='root' and Host = 'localhost';
```
```
flush privileges;
```
---
## 恢复my.ini配置文件
- 现在修改完密码了，需要删除或注释my.ini文件中的skip-grant-tables选项，**一定注意不要用记事本，那是个坑**
---
## 停止和启动mysql服务
```shell
net start mysql
net stop mysql
```
---
## 常规错误提示及可能遇到的问题
- 出现这个问题的原因一般是my.ini文件的编码格式出现问题了，保存的时候一定要记得是ANSI
> mysqld: [ERROR] Found option without preceding group in config file D:\Program Files\mysql\my.ini at line 1!  
> mysqld: [ERROR] Fatal error in defaults handling. Program aborted!  

- 如果你电脑的性能没啥问题的话，一般4-5S就能启动，像这种一直冒点的情况，可以在“计算机管理”界面查看Windows应用程序日志，翻一翻，MySQL相关错误
> D:\Program Files\mysql\bin>net start mysql  
> MySQL 服务正在启动 ................

- sc delete mysql 服务的时候回提示服务正在启动，不能删除，或者已经标记为删除的情况，但是服务就是删不掉的情况，这种情况下，第一确认你的服务是否已经停止（有时候 net stop mysql 不好使，可以直接在任务管理器里面，把mysql的进程结束掉） 第二、关闭你的services.msc界面  然后再执行sc 命令进行服务删除操作