# 在容器中安装新的程序
> 在ubuntu中执行安装命令的时候一定要注意，<code>apt-get install -y ping</code>中的y参数，因为apt-get命令会进入交互模式，需要用户输入命令来进行确认，但是在docker环境中是无法响应这种交互的

```
C:\Users\zp>docker run learn/tutorial apt-get install -y ping
Unable to find image 'learn/tutorial:latest' locally
latest: Pulling from learn/tutorial
271134aeb542: Pull complete
Digest: sha256:2933b82e7c2a72ad8ea89d58af5d1472e35dacd5b7233577483f58ff8f9338bd
Status: Downloaded newer image for learn/tutorial:latest
Reading package lists...
Building dependency tree...
The following NEW packages will be installed:
  iputils-ping
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 56.1 kB of archives.
After this operation, 143 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu/ precise/main iputils-ping amd64 3:20101006-1ubuntu1 [56.1 kB]
debconf: delaying package configuration, since apt-utils is not installed
Fetched 56.1 kB in 1s (38.6 kB/s)
Selecting previously unselected package iputils-ping.
(Reading database ... 7545 files and directories currently installed.)
Unpacking iputils-ping (from .../iputils-ping_3%3a20101006-1ubuntu1_amd64.deb) ...
Setting up iputils-ping (3:20101006-1ubuntu1) ...
```

## 发布自己的docker镜像
1. 首先commit镜像，将修改的内容在自己仓库中生成一个新的版本
```
C:\Users\zp>docker commit -a='zhangpeng' -m="张鹏的" d9bf4d5262ec donkeyzp/centos:v1.0
sha256:bb4b994d4ef9e376def4bee158221b538df35ec6792ce5653046294c88e258c6
```

2. 使用<code>docker images</code>查看自己提交的西版本
```
C:\Users\zp>docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
donkeyzp/centos     v1.0                e032b6fb8250        4 seconds ago       200MB
donkeyzp/centos     latest              bb4b994d4ef9        6 minutes ago       200MB
learn/ping          v1                  a37373d0a4f9        About an hour ago   140MB
runoob/ubuntu       dev                 a1656da3f20b        5 hours ago         137MB
runoob/ubuntu       v2                  a1656da3f20b        5 hours ago         137MB
runoob/ubuntuv2     latest              82ddd0cd24d7        5 hours ago         137MB
centos              latest              5182e96772bf        11 days ago         200MB
httpd               latest              11426a19f1a2        2 weeks ago         178MB
ubuntu              latest              735f80812f90        3 weeks ago         83.5MB
nginx               latest              c82521676580        3 weeks ago         109MB
ubuntu              14.04               971bb384a50a        4 weeks ago         188MB
ubuntu              15.10               9b9cb95443b5        2 years ago         137MB
training/webapp     latest              6fae60ef3446        3 years ago         349MB
ubuntu              13.10               7f020f7bf345        4 years ago         185MB
learn/tutorial      latest              a7876479f1aa        5 years ago         128MB
```

3. push到Docker Hub服务器上,推送完成后，即可在Docker Hub官网的Repository中查看自己提交的镜像
```
C:\Users\zp>docker push donkeyzp/centos:v1.0
The push refers to repository [docker.io/donkeyzp/centos]
1d31b5806ba4: Layer already exists
v1.0: digest: sha256:5b912595079d089e40fc3c83cc25176ed1b4eae0bb3cb556882bcfeb1b4affca size: 529
```