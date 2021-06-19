  在进行SQL注入时，有很多注入会出现无回显的情况，其中不回显的原因可能是SQL语句查询方式的问题所导致，这个时候我们要用到相关的报错或者盲注进行后续的操作，同时在手工注入的时候，有了解sql语句写法的必要。

#SQL注入盲注

报错盲注

  insert，delete，update；

延时盲注

> SQL语句
>
> if(条件，5，0)     -----条件成立返回5，反之为0
>
> sleep（）     ------SQL语句延时秒
>
> mid（a,b,c)      -----从位置b开始，截取a字符串的c位
>
> substr(a,b,c)      ------从b位置开始，截取字符串a的c长度
>
> length(database())     ------判断数据库名的长度

​    if 语句的用法：在对的时候返回123，错的时候返回456

![1619684020926](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619684020926.png)

  sleep(延时显示结果)

![1619684293715](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619684293715.png)

布尔盲注

依然无回显，但是可以判断是否存在。

#布尔盲注



