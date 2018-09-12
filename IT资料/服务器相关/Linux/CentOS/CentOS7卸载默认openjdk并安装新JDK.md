1. 首先第一步是查询是否安装了openjdk

```powershell
java -version
rpm -qa | grep java或者rpm -qa | grep jdk
```

![img](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9B%B8%E5%85%B3/2018-9-12-004.png?raw=true)

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

![img](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9B%B8%E5%85%B3/2018-9-12-005.png?raw=true)

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

![img](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9B%B8%E5%85%B3/2018-9-12-006.png?raw=true)

6. 执行编译，使配置文件立即生效

```powershell
. /etc/profile
或者
切换到etc文件夹下面执行
./profile
```

