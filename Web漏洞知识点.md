重点：一定要明白漏洞的危害，要达到什么样的目的。
学习目的：CTF,SRC,红蓝对抗，实战
**一.漏洞危害**
1.SQL注入
  危害：盗取数据库数据，获取账号密码等信息，进一步获得更高的权限。
2.文件上传
  危害：
3.xss
4.文件包含
5.反序列化
6.代码执行
7.逻辑安全
8.未授权访问
**二.等级划分**
中，高，低

**三.目录遍历漏洞**
1.源码结构泄露
2.通过修改参数值
 ../../../,其中../ 表示未知的一个目录
 危害：有的可以看到目录而看不到内容，反之亦可；具体看程序员设计时存在的问题。
 **四.文件下载漏洞**
 1.修改下载路径，可以下载自己所要想下载的文件，从而实现信息收集。 

实例：文件下载漏洞当然在下载文件的地方了。

![1619191635425](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619191635425.png)

  通过百度进行搜索，一个一个的进行筛选；

> 禁止非法 后果自负
>
> 实例网站     http://down.znds.com/

![1619191762863](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619191762863.png)

首先打开网站，选择任意文件/软件进行下载，下载文件大家都会，就不用多说；

![1619191883923](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619191883923.png)

![1619191969463](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619191969463.png)

接下来，我们对下载地址链接进行分析；

> 这是我们从页面复制下来的下载链接；
> 'http://down.znds.com/getdownurl/?s=L2Rvd24vMjAyMDExMTkva2pzXzEuMC4xX2RhbmdiZWkuYXBr

> 这是已经下载完成的文件链接；
> http://106.225.224.12/app.znds.com/down/20201119/kjs_1.0.1_dangbei.apk

> 所以可知道；
>

> s=L2Rvd24vMjAyMDExMTkva2pzXzEuMC4xX2RhbmdiZWkuYXBr 是已经进行了加密的，通过观察加密后密文的形式，可以判定为base64加密的；

![1619192492879](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619192492879.png)

显然，这已经很明确了。

如果我们想搞点其他事情的话，可以依据上面的思路进行操作。

比如；

  我们要进行下载该网站的 index.php 文件 或者 config.inc.php 之类的敏感性文件，就可以尝试用一下这样的一个漏洞，从而可以获取更多该网站的信息。

首先要将 config.inc.php 进行base64加密，然后带入到网站标签对应的值处。

![1619192861542](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619192861542.png)

> 代码整理后为 ：  http://down.znds.com/getdownurl/?s=Y29uZmlnLmluYy5waHA=

![1619192951541](C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619192951541.png)

当然，我这是随便猜测的一个文件，存不存在根本不知道，所以失败了，倘若硬是要搞这个网站，还需要了解此网站的目录结构，这儿就可以用一些扫描工具进行扫一扫，我就不扫了，哈哈！