# Docker镜像使用
当运行容器时，使用的镜像如果在本地中不存在，docker就会自动从docker镜像仓库中下载，默认是从Docker Hub公共镜像源下载。
> 下面我们来学习：
> 1. 管理和使用本地的Docker主机镜像
> 2. 创建镜像
## 列出镜像列表
我们可以使用<code>docker images</code>来列出本地主机上的镜像

```
C:\Users\zp>docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              latest              735f80812f90        3 weeks ago         83.5MB
ubuntu              15.10               9b9cb95443b5        2 years ago         137MB
training/webapp     latest              6fae60ef3446        3 years ago         349MB

C:\Users\zp>
```

> 各个选项说明：
> - REPOSITORY ：表示镜像的仓库员
> - TAG ：镜像的标签
> - IMAGE ID ：镜像ID
> - CREATED ：镜像创建时间
> - SIZE ：镜像大小

同一仓库源可以使用多个TAG，代表这个仓库员的不同版本，如：ubuntu仓库源里，有15.04、14.04等多个不同的版本，我们使用REPOSITORY:TAG来定义不同的镜像  
所以，我们如果要使用版本15.10的Ubuntu系统镜像来运行容器时，命令如下：

```
C:\Users\zp>docker run -i -t ubuntu:15.10 /bin/bash
root@63dfd0232254:/#
```

如果要使用14.04的Ubuntu系统镜像来运行容器时，命令如下：
```
C:\Users\zp>docker run -i -t ubuntu:14.04 /bin/bash
Unable to find image 'ubuntu:14.04' locally
14.04: Pulling from library/ubuntu
8284e13a281d: Downloading [======>                                            ]  9.092MB/67.13MB
26e1916a9297: Download complete
4102fc66d4ab: Download complete
1cf2b01777b2: Download complete
7f7a2d5e04ed: Download complete

```
> <font color='red'>如果你不指定一个镜像版本标签，例如你只是用ubuntu，docker将默认使用ubuntu:lastest镜像</font>


## 获取一个新的镜像
当我们在本机上使用一个不存在的镜像时Docker就会自动下载这个镜像。  
如果我们想预先下载这个镜像，我们可以使用<code>docker pull</code>命令来下载它
```
C:\Users\zp>docker pull ubuntu:13.10
13.10: Pulling from library/ubuntu
a3ed95caeb02: Pull complete
0d8710fc57fd: Downloading [=>                                                 ]  817.9kB/40.19MB
5037c5cd623d: Download complete
83b53423b49f: Download complete
e9e8bd3b94ab: Downloading [==>                                                ]  785.1kB/18.79MB
7db00e6b6e5e: Downloading [======================>                            ]  670.5kB/1.471MB
```
下载完成后，我们可以直接使用这个进行来运行容器

## 查找镜像
我们可以从Docker Hub网站来搜索镜像，Docker Hub网址：https://hub.docker.com  
我们也可以使用docker search命令来搜索镜像，比如我们需要一个httpd 的镜像来作为我们的web服务，我么可以通过<code>docker search</code> 命令搜索httpd来寻找适合我们的镜像
```
C:\Users\zp>docker search centos
NAME                               DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
centos                             The official build of CentOS.                   4585                [OK]
ansible/centos7-ansible            Ansible on Centos7                              115                                     [OK]
jdeathe/centos-ssh                 CentOS-6 6.10 x86_64 / CentOS-7 7.5.1804 x86…   99                                      [OK]
consol/centos-xfce-vnc             Centos container with "headless" VNC session…   60                                      [OK]
imagine10255/centos6-lnmp-php56    centos6-lnmp-php56                              44                                      [OK]
tutum/centos                       Simple CentOS docker image with SSH access      43
centos/mysql-57-centos7            MySQL 5.7 SQL database server                   38
gluster/gluster-centos             Official GlusterFS Image [ CentOS-7 +  Glust…   32                                      [OK]
openshift/base-centos7             A Centos7 derived base image for Source-To-I…   31
centos/python-35-centos7           Platform for building and running Python 3.5…   28
centos/postgresql-96-centos7       PostgreSQL is an advanced Object-Relational …   26
kinogmt/centos-ssh                 CentOS with SSH                                 22                                      [OK]
openshift/jenkins-2-centos7        A Centos7 based Jenkins v2.x image for use w…   14
pivotaldata/centos-gpdb-dev        CentOS image for GPDB development. Tag names…   7
openshift/mysql-55-centos7         DEPRECATED: A Centos7 based MySQL v5.5 image…   6
openshift/wildfly-101-centos7      A Centos7 based WildFly v10.1 image for use …   4
openshift/jenkins-1-centos7        DEPRECATED: A Centos7 based Jenkins v1.x ima…   4
darksheer/centos                   Base Centos Image -- Updated hourly             3                                       [OK]
pivotaldata/centos-mingw           Using the mingw toolchain to cross-compile t…   2
pivotaldata/centos                 Base centos, freshened up a little with a Do…   2
blacklabelops/centos               CentOS Base Image! Built and Updates Daily!     1                                       [OK]
jameseckersall/sonarr-centos       Sonarr on CentOS 7                              0                                       [OK]
pivotaldata/centos-gcc-toolchain   CentOS with a toolchain, but unaffiliated wi…   0
smartentry/centos                  centos with smartentry                          0                                       [OK]
pivotaldata/centos7-build          CentosOS 7 image for GPDB compilation           0

```
> 参数解析：
> - NAME : 镜像仓库源的名字
> - DESCRIPTION : 镜像描述
> - OFFICIAL ： 是否docker官方发布

## 拉取镜像
我们决定使用上图中的http官方版本镜像，使用命令<code>docker pull</code> 来下载镜像
```
C:\Users\zp>docker pull httpd
Using default tag: latest
latest: Pulling from library/httpd
d660b1f15b9b: Downloading [=>                                                 ]  2.153MB/54.25MB
aa1c79a2fa37: Download complete
f5f6514c0aff: Download complete
676d3dd26040: Download complete
4fdddf845a1b: Waiting
520c4b04fe88: Waiting
5387b1b7893c: Waiting
```
下载完成后，我们就可以使用这个镜像了。
```
C:\Users\zp>docker run -t -t httpd /bin/bash
root@04f6b1941403:/usr/local/apache2#
```
## 创建镜像
当我们从docker镜像仓库中下载的镜像不能满足我们的需求时，我们可以通过以下两种方式对镜像进行更改 
> - 从已经创建的容器中更新镜像，并且提交这个镜像
> - 使用Dockerfile指令来创建一个新的镜像

## 更新镜像
1. 更新镜像之前我们需要使用镜像创建一个容器
2. 在运行的容器内使用<code>apt-get update </code>命令进行更新
3. 使用<code>exit</code>或者CTRL+D退出容器
4. 通过容器的ID和<code>docker commit</code>提交升级后的容器副本
```
C:\Users\zp>docker run -i -t ubuntu:15.10 /bin/bash
root@7ff922f6b920:/# apt-get update # 更新系统
C:\Users\zp>docker commit -m="执行了apt-get update命令" -a="zhangpeng"  7ff922f6b920 runoob/ubuntu:v2
sha256:82ddd0cd24d7a38517d37b3f5f1f22f3b62e1b4bed2a308464ff9302bd038f60
```
> 参数解析
> - -m : 提交的描述信息
> - -a : 指定镜像坐着
> - 7ff922f6b920 : 镜像的ID
> - runoob/ubuntuv2 : 指定要创建的目标镜像名

我们可以使用<code>docker images</code> 查看我们的新镜像runoob/ubuntuv2
```
C:\Users\zp>docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
runoob/ubuntu       v2               82ddd0cd24d7        2 minutes ago       137MB
httpd               latest              11426a19f1a2        2 weeks ago         178MB
ubuntu              latest              735f80812f90        3 weeks ago         83.5MB
ubuntu              14.04               971bb384a50a        4 weeks ago         188MB
ubuntu              15.10               9b9cb95443b5        2 years ago         137MB
training/webapp     latest              6fae60ef3446        3 years ago         349MB
ubuntu              13.10               7f020f7bf345        4 years ago         185MB
```
使用我们的新景祥runoob/ubuntu来启动一个容器
```
C:\Users\zp>docker run -i -t runoob/ubuntu:v2 /bin/bash
root@9b0f6c646613:/#
```
## 构建镜像
我们使用命令<code>docker build</code>，从零开始创建一个新的镜像。为此我们需要创建一个Dockerfile文件，其中包含一组命令来告诉Docker如何构建我们的镜像
1. 首先创建一个文件名为Dockerfile的文件，没有后缀
```
# Dockerfile的文件文件内容（不包含这条，这条只是注释）
FROM    centos:6.7
MAINTAINER      Fisher "fisher@sudops.com"

RUN     /bin/echo 'root:123456' |chpasswd
RUN     useradd runoob
RUN     /bin/echo 'runoob:123456' |chpasswd
RUN     /bin/echo -e "LANG=\"en_US.UTF-8\"" >/etc/default/local
EXPOSE  22
EXPOSE  80
CMD     /usr/sbin/sshd -D
```
> 文件解析:
> - 每一个指令都会在镜像上创建一个新的层，每一个指令的前缀都必须是<font color='red'><b>大写</b></font>
> - 第一条FROM，指定使用哪个镜像源
> - RUN ：告诉Docker在镜像内执行的命令，安装什么

2. 使用Dockerfile文件，通过<code>docker build</code> 命令来创建一个镜像
```
C:\Users\zp>docker build -t runoob/centos:6.7 .
Sending build context to Docker daemon 17.92 kB
Step 1 : FROM centos:6.7
 ---&gt; d95b5ca17cc3
Step 2 : MAINTAINER Fisher "fisher@sudops.com"
 ---&gt; Using cache
 ---&gt; 0c92299c6f03
Step 3 : RUN /bin/echo 'root:123456' |chpasswd
 ---&gt; Using cache
 ---&gt; 0397ce2fbd0a
Step 4 : RUN useradd runoob
......
```
> 参数说明：
> - -t:指定要创建的目标镜像名
> - . Dockerfile所在的文件目录，可以指定Dockerfile的绝对路径

使用docker file查看自己创建的镜像已经自列表当中了

## 设置镜像标签
我们可以使用<code>docker tag</code>命令，为镜像添加一个新的标签，可以看到IMAGE_ID没有发生变化，并增加了一个TAG<code>dev</code>
```
C:\Users\zp>docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
runoob/ubuntu       v2                  a1656da3f20b        40 minutes ago      137MB
runoob/ubuntuv2     latest              82ddd0cd24d7        44 minutes ago      137MB
httpd               latest              11426a19f1a2        2 weeks ago         178MB
ubuntu              latest              735f80812f90        3 weeks ago         83.5MB
ubuntu              14.04               971bb384a50a        4 weeks ago         188MB
ubuntu              15.10               9b9cb95443b5        2 years ago         137MB
training/webapp     latest              6fae60ef3446        3 years ago         349MB
ubuntu              13.10               7f020f7bf345        4 years ago         185MB

C:\Users\zp>docker tag a1656da3f20b runoob/ubuntu:dev

C:\Users\zp>docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
runoob/ubuntu       dev                 a1656da3f20b        41 minutes ago      137MB
runoob/ubuntu       v2                  a1656da3f20b        41 minutes ago      137MB
runoob/ubuntuv2     latest              82ddd0cd24d7        44 minutes ago      137MB
httpd               latest              11426a19f1a2        2 weeks ago         178MB
ubuntu              latest              735f80812f90        3 weeks ago         83.5MB
ubuntu              14.04               971bb384a50a        4 weeks ago         188MB
ubuntu              15.10               9b9cb95443b5        2 years ago         137MB
training/webapp     latest              6fae60ef3446        3 years ago         349MB
ubuntu              13.10               7f020f7bf345        4 years ago         185MB
```