### 配置Maven

软件配置一次即可，所有Maven项目共享

![配置Maven](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-001.jpeg?raw=true)

1. 如上图标注3选择自己的仓库

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-002.jpeg?raw=true)

> 1. 如上图标注 2 所示，Import Maven projects automatically 表示 IntelliJ IDEA 会实时监控项目的 pom.xml 文件，进行项目变动设置
>
> 2. 如上图标注3 所示，在 Maven 导入依赖包的时候是否自动下载源码和文档。默认是没有勾选的，也不建议勾选，原因是这样可以加快项目从外网导入依赖包的速度，如果我们需要源码和文档的时 候我们到时候再针对某个依赖包进行联网下载即可。IntelliJ IDEA 支持直接从公网下载源码和文档的
> 3. 上图标注 3 所示，可以设置导入的 VM 参数。一般这个都不需要主动改，除非项目真的导入太慢了我们再增大此参数

3. Maven骨架创建JavaWeb项目

> 1. File->New->Project
>
> 2. 如下图

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-003.jpeg?raw=true)

> 3. 如下图

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-004.jpeg?raw=true)

> 4. 如下图

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-005.jpeg?raw=true)

> 5. 如下图

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-006.jpeg?raw=true)

> 6. 点Finish之后，Maven会根据刚才的配置创建一个基于Maven的Web App \- 创建结束，其Log如下

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-007.jpeg?raw=true)

> 创建结束，其代码结构如下

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-008.jpeg?raw=true)

>     recources文件夹：一般用来存放一些资源文件
>
>     webapp文件夹：用来存放web配置文件以及jsp页面等，这已经组成了一个原始的web应用

4. 启动JavaWeb项目

> 1. 打开Project Structure

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-009.jpeg?raw=true)

> 2. 配置Facets

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-010.jpeg?raw=true)

> 3. 配置“Artifacts”

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-011.jpeg?raw=true)

> 4. 启动“Edit Configuration”

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-012.jpeg?raw=true)

> 5. Add New 'Tomcat Server' 配置

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-013.jpeg?raw=true)


> 6. 配置Deplyment

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-014.jpeg?raw=true)

> 7. 配置Server

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-015.jpeg?raw=true)

> 8. 结果如下

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-016.jpeg?raw=true)

5. 启动WebServer

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%90%8E%E7%AB%AF/2018-9-12-017.jpeg?raw=true)

现在就可以访问WebServer了















