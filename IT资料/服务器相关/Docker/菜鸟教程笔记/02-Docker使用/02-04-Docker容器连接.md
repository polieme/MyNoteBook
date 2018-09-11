# Docker容器连接
前面我们实现了通过网络端口来访问运行在Docker容器内的服务。下面我们实现通过端口连接到一个Docker容器
## 网络端口映射
我们创建一个python的应用服务器
```
C:\Users\zp>docker run -d -P training/webapp python app.py
f1d0b735bfb01eb517bab75a696e36766c5fb153694937cef0e99facc0cda0e4

C:\Users\zp>
```
另外我们可以指定容器绑定网络地址，比如：127.0.0.1  
我们使用-P参数创建容器，使用<code>docker ps</code>查看端口5000绑定主机端口32768
```
C:\Users\zp>docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
f1d0b735bfb0        training/webapp     "python app.py"     5 minutes ago       Up 5 minutes        0.0.0.0:32768->5000/tcp   vigorous_saha

C:\Users\zp>

```
我们可以使用-p标识来指定容器端口绑定到主机的特定端口  
> 两种方式的区别：
> - -P : 容器内部端口<font color='red'><b>随机</b></font>映射到主机的高端口
> - -p ：容器内部端口绑定到<font color='red'><b>指定</b></font>的主机端口  

```
C:\Users\zp>docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
366388b2b14e        training/webapp     "python app.py"     4 seconds ago       Up 3 seconds        0.0.0.0:5000->5000/tcp    optimistic_elbakyan
f1d0b735bfb0        training/webapp     "python app.py"     9 minutes ago       Up 9 minutes        0.0.0.0:32768->5000/tcp   vigorous_saha
```

另外我们可以指定容器绑定网络地址，比如绑定127.0.0.1,这样我们就可以通过访问127.0.0.1:5001来访问容器的5000端口。
```
C:\Users\zp>docker run -d -p 127.0.0.1:5001:5000 training/webapp python app.py
74da427e9a224b39b7a2d55c3433dcb5ecef03767ef209bc8ee163d76b8acaed

C:\Users\zp>docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                      NAMES
74da427e9a22        training/webapp     "python app.py"     8 seconds ago       Up 7 seconds        127.0.0.1:5001->5000/tcp   practical_chatterjee
366388b2b14e        training/webapp     "python app.py"     11 minutes ago      Up 11 minutes       0.0.0.0:5000->5000/tcp     optimistic_elbakyan
f1d0b735bfb0        training/webapp     "python app.py"     21 minutes ago      Up 21 minutes       0.0.0.0:32768->5000/tcp    vigorous_saha

C:\Users\zp>
```
### 绑定udp端口
上面的列子是绑定的tcp的端口，如果想绑定udp的端口，可以在服务端口后面增加/udp
```
C:\Users\zp>docker run -d -p 127.0.0.1:5000:5000/udp training/webapp python app.py
489d40b3417996153f1e5a74caa66002db64f1187ed29eeeef5006e5fade8536

C:\Users\zp>docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                                NAMES
489d40b34179        training/webapp     "python app.py"     5 seconds ago       Up 3 seconds        5000/tcp, 127.0.0.1:5000->5000/udp   nifty_booth
74da427e9a22        training/webapp     "python app.py"     2 minutes ago       Up 2 minutes        127.0.0.1:5001->5000/tcp             practical_chatterjee
366388b2b14e        training/webapp     "python app.py"     14 minutes ago      Up 14 minutes       0.0.0.0:5000->5000/tcp               optimistic_elbakyan
f1d0b735bfb0        training/webapp     "python app.py"     24 minutes ago      Up 24 minutes       0.0.0.0:32768->5000/tcp              vigorous_saha

C:\Users\zp>
```
### docker port使用方法

```
C:\Users\zp>docker port 489d40b34179
5000/udp -> 127.0.0.1:5000
```

## Docker 容器的连接
端口映射并不是唯一把Docker连接到另一个容器的方法  
docker有一个连接系统允许将多个容器连接在一起，共享连接信息  
docker连接会创建一个父子关系，其中父容器能看到子容器的信息

### 容器命名
当我们创建一个容器的时候，docker会自动对他们进行命名。另外，我们可以使用<code>--name</code>标识来命名容器
```
C:\Users\zp>docker run -d -P  --name runoob training/webapp python app.py
f1ff2cbc0e1c1c30360abfbd2c5081368994a6f9b2e397f22ad0ade73a1bd038

C:\Users\zp>docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                                NAMES
f1ff2cbc0e1c        training/webapp     "python app.py"     7 seconds ago       Up 5 seconds        0.0.0.0:32769->5000/tcp              runoob
489d40b34179        training/webapp     "python app.py"     7 minutes ago       Up 7 minutes        5000/tcp, 127.0.0.1:5000->5000/udp   nifty_booth
74da427e9a22        training/webapp     "python app.py"     10 minutes ago      Up 10 minutes       127.0.0.1:5001->5000/tcp             practical_chatterjee
366388b2b14e        training/webapp     "python app.py"     22 minutes ago      Up 22 minutes       0.0.0.0:5000->5000/tcp               optimistic_elbakyan
f1d0b735bfb0        training/webapp     "python app.py"     31 minutes ago      Up 31 minutes       0.0.0.0:32768->5000/tcp              vigorous_saha
```