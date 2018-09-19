> 1. 中文编码问题

如果遇到需要输出中文的情况，需要在程序一开始设定字符集

```python
# -*- coding: UTF-8 -*-
```

> 2. 基础语法

- **交互式编程**：交互式编程不需要创建脚本文件，是通过 Python 解释器的交互模式进来编写代码
- **脚本式编程**：通过脚本参数调用解释器开始执行脚本，直到脚本执行完毕。当脚本执行完成后，解释器不再有效。

> 3. Python标识符

在 Python 里，标识符有字母、数字、下划线组成。

在 Python 中，所有标识符可以包括英文、数字以及下划线(_)，但不能以数字开头.

Python 中的标识符是区分大小写的.

以下划线开头的标识符是有特殊意义的。以单下划线开头 `_foo` 的代表不能直接访问的类属性，需通过类提供的接口进行访问，不能用 `from xxx import *` 而导入

以双下划线开头的 `__foo` 代表类的私有成员；以双下划线开头和结尾的 `__foo__` 代表 Python 里特殊方法专用的标识，如 `__init__()` 代表类的构造函数。

Python 可以同一行显示多条语句，方法是用分号 ; 分开

> 4. Python保留字符

| and      | exec    | not    |
| -------- | ------- | ------ |
| assert   | finally | or     |
| break    | for     | pass   |
| class    | from    | print  |
| continue | global  | raise  |
| def      | if      | return |
| del      | import  | try    |
| elif     | in      | while  |
| else     | is      | with   |
| except   | lamdba  | yield  |

> 5. 行和缩进

Python 的代码块不使用大括号 {} 来控制类,python 最具特色的就是用缩进来写模块

缩进的空白数量是可变的，但是所有代码块语句必须包含相同的缩进空白数量，这个必须严格执行。

不按照标准进行缩进的时候，程序会编译错误（unexpected indent ），空格和TAB键之间不能混用

> 6. 多行注释

Python语句中一般以新行作为为语句的结束符。

但是我们可以使用斜杠（ \）将一行的语句分为多行显示，如下所示

```python
print "This is the first section"+\
    "This is the second section"
```

> 7. Python引号

Python 可以使用引号( ' )、双引号( " )、三引号( ''' 或 """ ) 来表示字符串

> 8. Python注释

```python
# python中单行注释采用 # 开头
#this is the
print ("this is the ....") #这就是单行注释
python 中多行注释使用三个单引号(''')或三个双引号(""")。
'''
这是多行注释，你值得拥有
'''
print ("This is many lines remark")
```

> 9. Python空行

函数之间或类的方法之间用空行分隔，表示一段新的代码的开始。类和函数入口之间也用一行空行分隔，以突出函数入口的开始。空行和TAB、空格不一样，不是代码的一部分，是为了分离两块代码，便于理解和后期重构和维护

> 10. 等待用户输入

```python
var1 = raw_input("\n\n请输入你想输入的内容") #/n是用来换行用的
print var1
```

> 11. 同一行显示多条语句

```python
# Python可以在同一行中使用多条语句，语句之间使用分号(;)分割
import sys; x = 'runoob'; sys.stdout.write(x + '\n')
```

> 12. Print输出

```python
x = "a";y="b"
#这是换行输出
print x
print y
print "---------------"
#这是不换行输出
print x,
print y
```

> 13. 多个语句构成代码组

```python
# 缩进相同的一组语句构成一个代码块，我们称之代码组
# 像if、while、def和class这样的复合语句，首行以关键字开始，以冒号( : )结束，该行之后的一行或多行代码构成代码组
if True:
    print "This is True"
else:
    print "This is False"
```

> 14. 命令行参数

```python
# 很多程序可以执行一些操作来查看一些基本信，Python可以使用-h参数查看各参数帮助信息
$ python -h 
usage: python [option] ... [-c cmd | -m mod | file | -] [arg] ... 
Options and arguments (and corresponding environment variables): 
-c cmd : program passed in as string (terminates option list) 
-d     : debug output from parser (also PYTHONDEBUG=x) 
-E     : ignore environment variables (such as PYTHONPATH) 
-h     : print this help message and exit 
```

