# Docker Hello World
Docker允许你在容器中运行应用程序，使用<code>docker run</code>来运行一个应用程序
```shell
C:\Users\zp>docker run ubuntu:15.10 /bin/echo "Hello world"
Hello world
```
> 参数解析
> - docker：Docker的二进制执行文件
> - run：与当前的docker组合来运行的一个容器
> - ubuntu15.10：指定要运行的镜像，Docker首先从本地主机上查找镜像是否存在，如果不存在，Docker就会从镜像仓库Docker Hub下载公共镜像。
> - /bin/echo "Hello World" : 在启动的容器中执行的命令


# 运行交互式的容器
我们通过docker的两个参数<code>-i -t</code>，让docker运行的容器实现“对话”的能力

```shell
C:\Users\zp>docker run -i -t ubuntu:15.10
root@df6d73f6d23d:/#
```
> 参数解析
> - -t : 在新容器内指定一个伪终端或终端
> - -i : 允许你对容器内的标准输入进行交互  

此时，我们已经进入了一个ubuntu15.10系统的容器
我们尝试在容易中运行命令 <code>cat /proc/version</code> 和<code>ls</code>分别查看当前系统的版本信息和当前目录下的文件列表
```shell
C:\Users\zp>docker run -i -t ubuntu:15.10
root@2a956069d157:/# cat /proc/version
Linux version 4.9.93-linuxkit-aufs (root@856d34d1168e) (gcc version 6.4.0 (Alpine 6.4.0) ) #1 SMP Wed Jun 6 16:55:56 UTC 2018
root@2a956069d157:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@2a956069d157:/#
```
我们可以通过exit命令或者CTRL+D来退出容器

# 启动容器（后台模式）
使用以下命令创建一个以进程方式运行的容器

```shell
C:\Users\zp>docker run -d ubuntu:15.10 /bin/sh -c "while true;do echo hello world;sleep 1;done"
009f6076905ae2bf178959a8533e74e2d5025ab91f03626ebe65e18a98f97f19

C:\Users\zp>
```

在输出中，我们没有看到期望的hello world，而是一长串字符串，这个字符串叫做容器id，对每个容器来说都是唯一的，我们可以通过容器id来查看对应的容器发生了什么

首先我们需要确认容器有在运行，可以通过<code>pdocker ps</code>来查看

```shell
C:\Users\zp>docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
009f6076905a        ubuntu:15.10        "/bin/sh -c 'while t…"   2 minutes ago       Up 2 minutes                            nostalgic_proskuriakova

C:\Users\zp>
```

> 输出解析
> - CONTAINER ID : 容器ID
> - NAMES ：自动分配的容器名称
> - IMAGE : 镜像的系统名称和版本号
> - CREATED : 创建时间

在容器内使用<code>docker logs 容器id/容器name</code>命令，查看容器内的标准输出，是一致在输出hello world的

```powershell
C:\Users\zp>docker logs 009f6076905a
hello world
hello world
hello world
hello world
hello world
hello world
hello world
hello world
hello world
.....
```

# 停止容器
我们使用<code>docker stop 容器ID/容器name</code>命令来停止容器
```shell
C:\Users\zp>docker ps -all
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
009f6076905a        ubuntu:15.10        "/bin/sh -c 'while t…"   8 minutes ago       Up 8 minutes                            nostalgic_proskuriakova

C:\Users\zp>docker stop 009f6076905a
009f6076905a

C:\Users\zp>
```