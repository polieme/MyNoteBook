没有安装JDK 或者JDK配置出现错误

配置JDK的时候注意环境变量的配置方法

1、新建JAVA_HOME 他的值为JDK的安装绝对路径  例如：C:\Program Files\Java\jdk1.5.0_18\

2、新建Classpath（如果已经有的话，直接点击编辑，用分号隔开），他的值为   .;%JAVA_HOME%\lib

3、新建Path，如果已经有了，可以直接加分号隔开他的值为：%JAVA_HOME%\bin