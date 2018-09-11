1. 首先第一步是查询是否安装了openjdk

```powershell
java -version
rpm -qa | grep java或者rpm -qa | grep jdk
```

![img](E:/%E6%9D%82%E4%B8%83%E6%9D%82%E5%85%AB/Youdao/polieme@126.com/e180a24abc514df993c7a811972ee2bc/clipboard.png)

2. 执行卸载命令

```powershell
yum -y remove java 红色框中的内容
或者
rpm -e --nodeps 红色框中的内容
```

3. 安装jdk

   wget下载地址

   从jdk官网下载jdk，[对应的版本](http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jdk-8u111-linux-x64.tar.gz?AuthParam=1484402679_fcd52afad2d006c2f4d31c50b4e7b6b8)

4. 下载完成后进行解压

```powershell
tar -zxvf 下载下来的tar.gz 的安装包
```

![img](E:/%E6%9D%82%E4%B8%83%E6%9D%82%E5%85%AB/Youdao/polieme@126.com/b5c37c9fc6c44cf3bea3131ba4ebebfd/clipboard.png)

移动到对应的目录下面，习惯将软件安装在/usr/local下面，因此执行命令

mv jdk1.8.0_111/ /usr/local/

5. 配置环境变量

编辑/etc/profile文件，在最后添加如下内容,然后保存

```powershell
vim /etc/profile
export JAVA_HOME=/usr/local/jdk1.8.0_111
export JRE_HOME=/usr/local/jdk1.8.0_111/jre
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=$CLASSPATH:.:$JAVA_HOME/lib:$JRE_HOME/lib
```

![img](E:/%E6%9D%82%E4%B8%83%E6%9D%82%E5%85%AB/Youdao/polieme@126.com/f2d1864f140141a396f2b4f1ab2cbd88/clipboard.png)

6. 执行编译，使配置文件立即生效

```powershell
. /etc/profile
或者
切换到etc文件夹下面执行
./profile
```

