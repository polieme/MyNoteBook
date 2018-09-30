> **部署方式**

- 直接在eclipse中添加一个server，添加过程中指明tomcat的路径即可

- 在tomcat服务器的conf\Catalina\localhost目录下创建一个xml文件

(路径找不到就自己创建)，内容如下：

```xml
<Context path="/TestPro" docBase="D:\javaProject\TestPro\WebContent" debug="0" privileged="true">
</Context>
```

其中path是指项目的发布路径，也就是访问路径，假如像上边那样填写，就要这样访问：http://localhost:8080/ TestPro /index.jsp；docBase是指项目的WebContent(eclipse)或WebRoot(myeclipse)目录，很好理解，你的项目最终发布，就是发布的这个目录，通过配置，直接让tomcat指向这个目录，这样就可以运行项目啦。

`注意：xml的文件名一定要和发布路径一致！在本例中xml文件名必须为：TestPro</font>`

- 在eclipse中启动tomcat，项目即可启动。

上边是比较常见的用法，但很多时候，我们希望把项目发布到tomcat根目录，这样就不用输入冗长的发布路径，直接输入域名就可以访问了。

　　用这种方法把项目发布tomcat根目录，注意事项如下

1.为了保险起见，删掉tomcat服务器中的webapps目录下的ROOT文件夹。

2.将xml中的path设成空(path="")。

3.将xml文件名改为ROOT(ROOT.xml)。