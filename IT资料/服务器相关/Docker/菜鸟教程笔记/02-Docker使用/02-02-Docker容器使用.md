# Docker 客户端
docker客户端非常简单，我们可以直接输入<code>docker</code>命令来查看Docker客户端的所有命令选项
```
C:\Users\zp>docker

Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Options:
      --config string      Location of client config files (default
                           "C:\\Users\\zp\\.docker")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level
                           ("debug"|"info"|"warn"|"error"|"fatal")
                           (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default
                           "C:\\Users\\zp\\.docker\\ca.pem")
      --tlscert string     Path to TLS certificate file (default
                           "C:\\Users\\zp\\.docker\\cert.pem")
      --tlskey string      Path to TLS key file (default
                           "C:\\Users\\zp\\.docker\\key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

Management Commands:
  config      Manage Docker configs
  container   Manage containers
  image       Manage images
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

Run 'docker COMMAND --help' for more information on a command.
```

可以通过命令<code>docker command --help</code>更深入的了解指定的Docker命令使用方法。
例如我们要查看stats指令的具体使用方法
```
C:\Users\zp>docker stats --help

Usage:  docker stats [OPTIONS] [CONTAINER...]

Display a live stream of container(s) resource usage statistics

Options:
  -a, --all             Show all containers (default shows just running)
      --format string   Pretty-print images using a Go template
      --no-stream       Disable streaming stats and only pull the first result
      --no-trunc        Do not truncate output

C:\Users\zp>
```

# 运行一个web应用
前面我们运行的容器并没有一些什么特别的用处。
接下来我们尝试使用docker勾践一个web应用程序。
我们将在docker容器中运行一个Python Flask应用来运行一个web应用
```
C:\Users\zp>docker pull training/webapp #载入镜像
Using default tag: latest
latest: Pulling from training/webapp
e190868d63f8: Already exists
909cd34c6fd7: Already exists
0b9bfabab7c1: Already exists
a3ed95caeb02: Already exists
10bbbc0fc0ff: Already exists
fca59b508e9f: Already exists
e7ae2541b15b: Already exists
9dd97ef58ce9: Already exists
a4c1b0cb7af7: Already exists
Digest: sha256:06e9c1983bd6d5db5fba376ccd63bfa529e8d02f23d5079b8f74a616308fb11d
Status: Image is up to date for training/webapp:latest

C:\Users\zp>docker run -d -P training/webapp python app.py # 启动镜像和应用
9d5c0bfcc43b6fcb4b2759007d0d99291cc920ac06e8e03bb78b3eb202ab0964

C:\Users\zp>
```

> 参数说明：
> - -d : 让容器在后台运行
> - -P : 将容器内部使用的网络端口映射到我们使用的主机上

# 查看WEB应用容器
使用<code>docker ps</code>来查看我们正在运行的容器
```
C:\Users\zp>docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
9d5c0bfcc43b        training/webapp     "python app.py"     6 minutes ago       Up 6 minutes        0.0.0.0:32769->5000/tcp   gracious_bohr
```
这里显示了对应服务的端口
```
0.0.0.0:32769->5000/tcp
```

Docker 开放了5000端口（默认Python Flask端口）映射到主机端口32769上
这时候我们就可以通过浏览器访问WEB应用
```
http://localhost:32769/
```

我们也可以通过-p参数来设定不一样的端口：
```
C:\Users\zp>docker run -d -p 5000:5000 training/webapp python app.py
d6a34ff63dc3e38a0c00b8dc9b10fb094fb857a8bee7648e52ac65003f63cabf

C:\Users\zp>
```
查看启动的实例，可以发现容器内部的5000端口映射到我们本地主机的5000端口上
```
C:\Users\zp>docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
d6a34ff63dc3        training/webapp     "python app.py"     25 seconds ago      Up 23 seconds       0.0.0.0:5000->5000/tcp    pedantic_agnesi
9d5c0bfcc43b        training/webapp     "python app.py"     11 minutes ago      Up 11 minutes       0.0.0.0:32769->5000/tcp   gracious_bohr
```

# 网络端口的快捷方式
通过<code>docker ps</code>命令查看到容器的端口映射，docker还提供了另一个快捷方式：<code>docker port</code>，使用<code>docker port</code>可以查看指定（ID或者名字）容器的某个确定端口映射到宿主机的端口
上面我们创建的web应用容器ID为：d6a34ff63dc3 名字为pedantic_agnesi  
我们可以使用对应的id查看端口的映射情况，代码如下
```
C:\Users\zp>docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
d6a34ff63dc3        training/webapp     "python app.py"     6 minutes ago       Up 6 minutes        0.0.0.0:5000->5000/tcp    pedantic_agnesi
9d5c0bfcc43b        training/webapp     "python app.py"     18 minutes ago      Up 18 minutes       0.0.0.0:32769->5000/tcp   gracious_bohr

C:\Users\zp>docker ps -all
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                    NAMES
d6a34ff63dc3        training/webapp     "python app.py"     7 minutes ago       Up 7 minutes        0.0.0.0:5000->5000/tcp   pedantic_agnesi

C:\Users\zp>docker port d6a34ff63dc3
5000/tcp -> 0.0.0.0:5000

C:\Users\zp>docker port 9d5c0bfcc43b
5000/tcp -> 0.0.0.0:32769

```

# 查看web应用程序日志
<code>docker logs[ID 或者名字]</code>可以查看容器内部的标准输出
```
C:\Users\zp>docker logs -f 9d5c0bfcc43b
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
172.17.0.1 - - [17/Aug/2018 08:12:49] "GET / HTTP/1.1" 200 -
172.17.0.1 - - [17/Aug/2018 08:12:49] "GET /favicon.ico HTTP/1.1" 404 -
```
> 参数解析：
> - -f : 让<code>docker logs</code> 像tail -f 一样来输出容器内部的标准输出。
>   从上面，我们可以看到应用程序使用的是5000端口，并且能够查看到应用程序的访问日志

# 查看WEB应用程序容器的进程
我们还可以使用<code>docker top 容器ID/容器NAME</code>来查看容器内部运行的进程
```
C:\Users\zp>docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
d6a34ff63dc3        training/webapp     "python app.py"     13 minutes ago      Up 13 minutes       0.0.0.0:5000->5000/tcp    pedantic_agnesi
9d5c0bfcc43b        training/webapp     "python app.py"     24 minutes ago      Up 24 minutes       0.0.0.0:32769->5000/tcp   gracious_bohr

C:\Users\zp>docker top d6a34ff63dc3 # 查看对应容器中的运行的程序
PID                 USER                TIME                COMMAND
4735                root                0:00                python app.py
```

# 检查WEB应用程序
## <code>docker inspect</code>使用方法
使用<code>docker inspect 容器ID/容器NAME</code>来查看Docker的底层信息，他会放回一个JSON文件记录的Docker容器的配置和状态信息

```
C:\Users\zp>docker inspect  d6a34ff63dc3
[
    {
        "Id": "d6a34ff63dc3e38a0c00b8dc9b10fb094fb857a8bee7648e52ac65003f63cabf",
        "Created": "2018-08-17T08:14:58.9619605Z",
        "Path": "python",
        "Args": [
            "app.py"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 4735,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2018-08-17T08:15:00.803567Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:6fae60ef344644649a39240b94d73b8ba9c67f898ede85cf8e947a887b3e6557",
        "ResolvConfPath": "/var/lib/docker/containers/d6a34ff63dc3e38a0c00b8dc9b10fb094fb857a8bee7648e52ac65003f63cabf/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/d6a34ff63dc3e38a0c00b8dc9b10fb094fb857a8bee7648e52ac65003f63cabf/hostname",
        "HostsPath": "/var/lib/docker/containers/d6a34ff63dc3e38a0c00b8dc9b10fb094fb857a8bee7648e52ac65003f63cabf/hosts",
        "LogPath": "/var/lib/docker/containers/d6a34ff63dc3e38a0c00b8dc9b10fb094fb857a8bee7648e52ac65003f63cabf/d6a34ff63dc3e38a0c00b8dc9b10fb094fb857a8bee7648e52ac65003f63cabf-json.log",
        "Name": "/pedantic_agnesi",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        ......
```
# 停止WEB应用容器
## <code>docker stop</code>使用方法
使用命令<code>docker stop 容器ID/容器NAME</code> 可以停止对应的应用容器
```
C:\Users\zp>docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
d6a34ff63dc3        training/webapp     "python app.py"     17 minutes ago      Up 16 minutes       0.0.0.0:5000->5000/tcp    pedantic_agnesi
9d5c0bfcc43b        training/webapp     "python app.py"     28 minutes ago      Up 28 minutes       0.0.0.0:32769->5000/tcp   gracious_bohr

C:\Users\zp>docker stop d6a34ff63dc3 9d5c0bfcc43b
d6a34ff63dc3
9d5c0bfcc43b

C:\Users\zp>
```

# 重启WEB应用容器
## <code>docker start</code>使用方法
已经停止的容器，我们可以使用命令<code>docker start 容器ID/容器NAME</code>来启动

```
C:\Users\zp>docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
d6a34ff63dc3        training/webapp     "python app.py"     17 minutes ago      Up 16 minutes       0.0.0.0:5000->5000/tcp    pedantic_agnesi
9d5c0bfcc43b        training/webapp     "python app.py"     28 minutes ago      Up 28 minutes       0.0.0.0:32769->5000/tcp   gracious_bohr

C:\Users\zp>docker stop d6a34ff63dc3 9d5c0bfcc43b
d6a34ff63dc3
9d5c0bfcc43b

C:\Users\zp>docker ps -all
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                            PORTS               NAMES
d6a34ff63dc3        training/webapp     "python app.py"     19 minutes ago      Exited (137) About a minute ago                       pedantic_agnesi

C:\Users\zp>docker start d6a34ff63dc3
d6a34ff63dc3


C:\Users\zp>docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                    NAMES
d6a34ff63dc3        training/webapp     "python app.py"     20 minutes ago      Up 57 seconds       0.0.0.0:5000->5000/tcp   pedantic_agnesi

C:\Users\zp>
```
## <code>docker ps -l</code>使用方法
使用<code>docker ps -l</code>查看最后一次创建的容器
```
C:\Users\zp>docker ps -l
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                    NAMES
d6a34ff63dc3        training/webapp     "python app.py"     21 minutes ago      Up 2 minutes        0.0.0.0:5000->5000/tcp   pedantic_agnesi

C:\Users\zp>
```

## <code>docker restart</code> 使用方法
正在运行的容器我们可以使用<code>docker restart 容器ID/容器NAME</code>命令来重启

# 移除WEB应用容器
## <code>docker rm</code>命令使用
我们可以使用<code>docker rm 容器ID/容器NAME</code>来删除不需要的容器  
<font color='red'>删除容器时，容器必须是停止状态，否则会报如下错误</font>
```
C:\Users\zp> docker rm determined_swanson
Error response from daemon: You cannot remove a running container 7a38a1ad55c6914b360b565819604733db751d86afd2575236a70a2519527361. Stop the container before attempting removal or use -f
```