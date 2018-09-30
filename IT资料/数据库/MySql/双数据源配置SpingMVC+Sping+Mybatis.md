> 1. 首当其冲第一步就是修改数据库配置文件，我这里叫dbconfig.properties，修改的时候，只需要把原来的数据库的配置文件复制一套，然后在前面加上对应数据库的标识就行

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E6%95%B0%E6%8D%AE%E5%BA%93/clipboard1.png?raw=true)

> 2. 修改Sping的配置文件“ApplicationContext.xml”，复制一套“org.springframework.jdbc.datasource.DataSourceTransactionManager”对应的bean，修改对应的name值为transactionManager2，然后复制一套数据库连接的配置，改为数据源2的数据信息

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E6%95%B0%E6%8D%AE%E5%BA%93/clipboard2.png?raw=true)

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E6%95%B0%E6%8D%AE%E5%BA%93/clipboard3.png?raw=true)

> 3. 再就是DAO层面的修改了，只需要修改两个地方，一个地方是“sqlSessionTemplate2”对应到上面Sprig配置文件中的“sqlSessionTemplate2”，在一个就是DaoSupport的声明了吧



> 4. 下面就可以直接使用了

