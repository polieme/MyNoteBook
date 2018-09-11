1. tomcat 需要增加一个pid文件 

在tomca/bin 目录下面，增加 setenv.sh 配置，catalina.sh启动的时候会调用，同时配置java内存参数。 

\#add tomcat pid CATALINA_PID="$CATALINA_BASE/tomcat.pid" #add java opts JAVA_OPTS="-server -XX:PermSize=256M -XX:MaxPermSize=1024m -Xms512M -Xmx1024M -XX:MaxNewSize=256m"

2. 增加tomcat.service

[Unit] Description=tomcat After=syslog.target network.target remote-fs.target nss-lookup.target [Service] Type=forking PIDFile=/usr/local/tomcat/apache-tomcat-8.5.8/tomcat.pid ExecStart=/usr/local/tomcat/apache-tomcat-8.5.8/bin/startup.sh ExecStop=/bin/kill -s QUIT $MAINPID ExecReload=/bin/kill -s HUP $MAINPID PrivateTmp=true [Install] WantedBy=multi-user.targe

3. 使用tomcat.service

​    配置开机启动 

​    systemctl enable tomcat 

　 启动tomcat 

    systemctl start tomcat 

    停止tomcat 

    systemctl stop tomcat 

    重启tomcat 

    systemctl restart tomcat 



　注：因为配置pid，在启动的时候会再tomcat根目录生成tomcat.pid文件，停止之后删除。



     同时tomcat在启动时候，执行start不会启动两个tomcat，保证始终只有一个tomcat服务在运行。 

　　多个tomcat可以配置在多个目录下，互不影响。



