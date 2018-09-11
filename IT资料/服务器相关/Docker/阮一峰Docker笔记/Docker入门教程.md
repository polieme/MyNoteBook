> 本文引自[Docker 入门教程](http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html)

# Docker解决的问题
## 环境配置难题
> 软件开发最大的麻烦事之一，就是环境配置，无法确认用户的计算机是否能够和软件环境想匹配，从而保证能够正常运行

1. 用户必须要做到两件事：操作系统设置，各种库和组件的安装，只有相同，才能保证软件的正常运行  
2. 环境配置麻烦，换一台机子，就要重来一次，旷日费时

## 虚拟机

虚拟机目前是一种解决方案，但虚拟机存在几个缺点：
1. 资源占用多：虚拟机会独占一部分内存和硬盘控件，其他程序运行时就不能使用这些资源了，哪怕虚拟机里面的程序只使用了1MB内存，虚拟机依然需要几百MB的内存才能运行。
2. 冗余步骤多：虚拟机是一个完全的操作系统，一些系统级别的操作步骤是没法跳过的
3. 启动慢：启动操作系统需要时间长

# Docker是什么？

> Docker属于Linux容器的一种封装，提供简单易用的容器使用接口，他是目前最流行的Linux容器解决方案

Docker将应用程序与该程序的依赖，打包在一个文件里面。运行这个文件，就会生成一个虚拟容器。程序在这个虚拟容器里面运行，就好像在真是物理机上运行一样。有了Docker，就不用担心环境的问题了。

总体来说，Docker的接口相当简单，用户可以方便的创建和使用容器，把自己的应用放入容器。容器还可以进行版本管理、复制、分享、修改，就像是管理普通代码一样。

# Docker用途

Docker的主要用途：
- <b>提供一次性的环境。</b>比如，本地测试他人的软件、持续集成的时候提供单元测试和构建的环境
- <b>提供弹性的云服务。</b>因为Docker容器可以随时开关，很适合动态的扩容和缩容
- <b>组件微服务架构。</b>通过多个容器，一台机器可以跑很多服务，因此在本机就可以模拟出微服务架构

# Docker安装
Docker 是一个开源的商业产品，有两个版本：社区版（Community Edition，缩写CE版）和企业版（Enterprise Edtion，缩写为EE），企业版包含一些收费服务，个人开发者一般用不到，下面的介绍针对社区版。  
<b>Docker CE参考官方文档：</b>
> - [Ubuntu:https://docs.docker.com/install/linux/docker-ce/ubuntu/#set-up-the-repository](https://docs.docker.com/install/linux/docker-ce/ubuntu/#set-up-the-repository)
> - [CentOS:https://docs.docker.com/install/linux/docker-ce/centos/](https://docs.docker.com/install/linux/docker-ce/centos/)


安装完成后，运行下面的命令，验证是否安装成功。
```powershell
$ docker version
# 或者
$ docker info
```

Docker需要用户具有sudo权限，为了避免每次输入sudo，可把用户加入Docker用户组
```powershell
$ sudo usermode -aG docker $USER
```

Docker 是服务器-客户端架构。命令行运行Docker命令的时候，需要本机有Docker服务，如果这项服务没有启动，可以用下面的命令启动
```powershell
# service命令启动方式
$ sudo service docker start

# systemctl 命令启动方式
$ sudo systemctl start docker
```

# image 文件
<b>Docker把应用程序及其相关依赖，打包在image文件里面。</b>，只有通过这个文件，才能生成Docker容器。image文件可以看做是容器的模板。Docker根据image文件生成容器的实例。同一个image文件，可以生成多个同时运行的容器实例。

image 是二级制文件。实际开发中，一个image文件往往通过继承另一个image文件，加上一些个性化设置生成，距离来说，你可以在Ubuntu的image基础上，往里面加入Apache服务器，形成你的image
```powershell
# 列出本机上的所有image文件
$ docker images
#或者
$ docker image ls

# 删除image文件
$ docker image rm [imageName或imageId]
```

image文件是通用的，一台机器的image文件拷贝到另一台电脑，照样可以使用。一般来说为了节省时间，我们应该尽量使用别人制作好的image文件，而不是自己制作。即使要定制，也应该基于别人的image文件进行加工，而不是从零开始。

为了方便共享，image文件制作完成后，可以上传到网上的仓库。Docker的官方仓库[Docker Hub](https://hub.docker.com/)是最重要、最常用的image仓库

# 实例：hello world
下面，我们通过最简单的image文件“Hello world”，感受一下Docker
### 下载image（docker pull的使用）
> 该命令不是必须的命令，可以在docker run的时候检索本地image，如果本地没有对应的image，会自动执行docker pull去服务端进行拉取，因此不是必须的

1. 首先运行下面的命令，将image文件从仓库抓取到本地
```powershell
$ docker pull library/hello-world
或者
$ docker image pull library/hello-world
或者
$ docker pull hello-world
```
上面的代码中，<code>docker image pull</code>或者<code>docker pull</code>是抓取image命令。<code>library/hello-world</code>是image文件所在仓库里面的位置，其中<code>library</code>是image文件所在的组，<code>hello-image</code>是image文件的名字。  
由于Docker官方提供的image文件，都是在<code>library</code>组里面，所以他是默认组，可以省略。

### 运行image文件
现在就可以直接运行刚刚下载的image了
```powershell
$ docker container run hello-world
# 或者
$ docker run hello-world
# 或者
$ docker run [container-id]
```
<code>docker container run</code>命令会从image文件，生成一个正在运行的容器实例

<b><font color='red'>注意：</font></b>
> <code>docker container run</code>命令具有自动住区image文件的功能。如果发现本地没有指定的image文件，就会从仓库自动抓取。因此，前面的<code>docker image pull</code>命令并不是必须的步骤。

如果运行成功，会输出以下内容：
```powershell
$ docker run -i -t 2cb0d9787c4d

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/
```
输出这段提示内容以后，<code>hello world</code>就会自动停止运行，容器自动终止。  
有些容器不会自动终止，因为提供的是服务，比如：Ubuntu的image，就可以在命令行体验Ubuntu系统。
```powershell
$ docker container run -it ubuntu bash
```
运行完上面的命令之后就会出现下面的界面，同时你会进入到Ubuntu的命令行模式
```powershell
docker run -it ubuntu bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
124c757242f8: Pull complete
2ebc019eb4e2: Pull complete
dac0825f7ffb: Pull complete
82b0bb65d1bf: Pull complete
ef3b655c7f88: Pull complete
Digest: sha256:72f832c6184b55569be1cd9043e4a80055d55873417ea792d989441f207dd2c7
Status: Downloaded newer image for ubuntu:latest
root@fdab40f4c6b7:/#
```