> 1. 下载Tomcat就不多说了

[下载地址](http://tomcat.apache.org/download-70.cgi)

> 2. 新建文件夹 `mkdir /usr/local/tomcat1`（用作双Tomcat部署）

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E4%B8%AD%E9%97%B4%E4%BB%B6/3559162F2A9148E7B0447E090521124B.jpg?raw=true)

> 3. 将下载的Tomcat包mv到tomcat1下面进行解压缩

```shell
mv apache-tomcat-7.0.73.tar.gz /usr/local/tomcat1      //移动压缩文件到tomcat1
tar -zxvf  apache-tomcat-7.0.73.tar.gz    //进行解压操作
```

> 4. 修改Tomcat端口号,将server.xml里面的`<Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" />`里面的8080为你想要的端口号

```shell
vim /usr/local/tomcat1/server.xml
```

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E4%B8%AD%E9%97%B4%E4%BB%B6/clipboard.png?raw=true)

> 5. 如果一台服务器想要部署多个Tomcat，那就继续吧，在`/usr/local`下创建另外一个tomcat文件夹
>
>    `mkdir /usr/local/tomcat2`，将压缩文件解压在tomcat2中，修改server.xml文件，主要修改两个`Connector port`

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E4%B8%AD%E9%97%B4%E4%BB%B6/clipboard1.png?raw=true)

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E4%B8%AD%E9%97%B4%E4%BB%B6/clipboard2.png?raw=true)

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E4%B8%AD%E9%97%B4%E4%BB%B6/clipboard3.png?raw=true)

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E4%B8%AD%E9%97%B4%E4%BB%B6/clipboard4.png?raw=true)

注：附上CentOS7的端口号开放的方法

```shell
firewall-cmd --add-port=8080/tcp --permant --zone=public

firewall-cmd --reload
```



