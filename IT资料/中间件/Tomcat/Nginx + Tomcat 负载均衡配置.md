# 1. Nginx安装

---

## 1.1 依赖库安装

首先由于nginx的一些模块依赖一些lib库，所以在安装nginx之前，必须先安装这些lib库，这些依赖库主要有g++、gcc、openssl-devel、pcre-devel和zlib-devel 所以执行如下命令安装

```shell
$   yum install gcc-c++  
$   yum install pcre pcre-devel  
$   yum install zlib zlib-devel  
$   yum install openssl openssl--devel  
```

## 1.2 安装步骤

### 1.2.1 验证是否安装过Nginx

如果已经安装过，需要进行卸载 yum remove nginx

```shell
$   find -name nginx  
```

### 1.2.2 下载Ngnix

```shell
$   wget http://nginx.org/download/nginx-1.7.4.tar.gz
```

### 1.2.3 解压压缩包

```shell
$   tar -zxvf nginx-1.7.4.tar.gz
```

### 1.2.4 安装

进入解压的文件夹，接下来安装，使用--prefix参数指定nginx安装的目录,make、make install安装

```shell
$   ./configure  $默认安装在/usr/local/nginx   
$   make  
$   make install
```

### 1.2.5 查看安装位置

```shell
$   whereis nginx
```

# 2. 负载均衡配置

## 2.1 修改nginx的配置文件

修改`/usr/local/nginx/conf`文件夹下面的`nginx.conf`文件

```shell
cd /usr/local/nginx/conf
vim nginx.conf
```

定义一个mysite，然后定义这个mysite对应需要负载均衡的服务器

```properties
upstream mysite{

server 192.168.1.148:8080;

server 192.168.1.148:8081;

ip_hash;

}
```

ip_hash 是为了保证访问的时候只对一个服务器，使`session`能够保持住

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E4%B8%AD%E9%97%B4%E4%BB%B6/lip_image001.png?raw=true)

## 2.2 启动、停止nginx

进入nginx的安装文件夹下

```shell
cd /usr/local/nginx/sbin
./nginx //启动
./nginx -s stop //停止
./nginx -s reload  //重新加载
./nginx -s quit:此方式停止步骤是待nginx进程处理任务完毕进行停止。
./nginx -s stop:此方式相当于先查出nginx进程id再使用kill命令强制杀掉进程。
```

