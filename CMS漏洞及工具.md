**一.CMSmap工具**
  CMSmap是一个Python编写的针对开源CMS（内容管理系统）的安全扫描器，它可以自动检测当前国外最流行的CMS的安全漏洞。 
  其功能：
  1.可以检测网站的cms基本类型，自带wordPress,Joomla与Drupal插件列表，可以检测各种插件；
  2.多线程扫描工具，默认线程数为5；
  3.简单易操场。

**二.Web应用程序防火墙指纹识别工具WAFw00f**

> 本机安装位置：cd C:\Users\MCY\AppData\Local\Programs\Python\Python38-32\Lib\site-packages\wafw00f

安装教程：如下
安装环境：python3环境 ----> 使用pip install WAFwoof 直接安装；
安装成功后，找到其安装目录下，在cmd命令中打开；比如我的，

![1619171340790](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619171340790.png)

安装完成后就是上图的样子，然后根据提示打开wafw00f目录

![1619171435781](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619171435781.png)

![1619171453366](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619171453366.png)

> 输入命令  python main.py -l   #可以查看能够探测的防火墙

![1619171578441](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619171578441.png)

探测web网站是否存在WAF

> 输入命令   python main.py  网站域名/IP  
>
> 举例：python main.py  www.baidu.com   存在防火墙

![1619171874222](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619171874222.png)

> 这个网站不存在WAF
>
> python main.py http://127.0.0.1/login/

![1619172239747](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619172239747.png)