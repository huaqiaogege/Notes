** 1.Sql注入类型**
数字型：？id=2;
字符型。搜索型: name='xxxx'
JSON型注入:少见，遵循一定的格式{‘users':'zhuhuaqiao'} 注入方式犹如列表，其格式就是如此，在APP中常见；

JSON：注入格式

> a=1 and 1=1&b=2&c=3
>
> {
>
> "a":1 and 1=1"
>
> "b":"2"
>
> "c":"3"
>
> }

sql语句中常见特殊干扰符号：‘，%，''。还有单引号，双引号。
#请求方法：GET（单个接收）,POST;COOKIE,REQUEST(全部接收)
可以根据方法，判断网站的接收方法

COOKIE：

```
$_SERVER：在PHP中获取信息：

$_SERVER['PHP_SELF'] #当前正在执行脚本的文件名，与 document root相关。
$_SERVER['argv'] #传递给该脚本的参数。
$_SERVER['argc'] #包含传递给程序的命令行参数的个数（如果运行在命令行模式）。
$_SERVER['GATEWAY_INTERFACE'] #服务器使用的 CGI 规范的版本。例如，“CGI/1.1”。
$_SERVER['SERVER_NAME'] #当前运行脚本所在服务器主机的名称。
$_SERVER['SERVER_SOFTWARE'] #服务器标识的字串，在响应请求时的头部中给出。
$_SERVER['SERVER_PROTOCOL'] #请求页面时通信协议的名称和版本。例如，“HTTP/1.0”。
$_SERVER['REQUEST_METHOD'] #访问页面时的请求方法。例如：“GET”、“HEAD”，“POST”，“PUT”。
$_SERVER['QUERY_STRING'] #查询(query)的字符串。
$_SERVER['DOCUMENT_ROOT'] #当前运行脚本所在的文档根目录。在服务器配置文件中定义。
$_SERVER['HTTP_ACCEPT'] #当前请求的 Accept: 头部的内容。
$_SERVER['HTTP_ACCEPT_CHARSET'] #当前请求的 Accept-Charset: 头部的内容。例如：“iso-8859-1,*,utf-8”。
$_SERVER['HTTP_ACCEPT_ENCODING'] #当前请求的 Accept-Encoding: 头部的内容。例如：“gzip”。
$_SERVER['HTTP_ACCEPT_LANGUAGE']#当前请求的 Accept-Language: 头部的内容。例如：“en”。
$_SERVER['HTTP_CONNECTION'] #当前请求的 Connection: 头部的内容。例如：“Keep-Alive”。
$_SERVER['HTTP_HOST'] #当前请求的 Host: 头部的内容。
$_SERVER['HTTP_REFERER'] #链接到当前页面的前一页面的 URL 地址。
$_SERVER['HTTP_USER_AGENT'] #当前请求的 User_Agent: 头部的内容。
$_SERVER['HTTPS'] — 如果通过https访问,则被设为一个非空的值(on)，否则返回off
$_SERVER['REMOTE_ADDR'] #正在浏览当前页面用户的 IP 地址。
$_SERVER['REMOTE_HOST'] #正在浏览当前页面用户的主机名。
$_SERVER['REMOTE_PORT'] #用户连接到服务器时所使用的端口。
$_SERVER['SCRIPT_FILENAME'] #当前执行脚本的绝对路径名。
$_SERVER['SERVER_ADMIN'] #管理员信息
$_SERVER['SERVER_PORT'] #服务器所使用的端口
$_SERVER['SERVER_SIGNATURE'] #包含服务器版本和虚拟主机名的字符串。
$_SERVER['PATH_TRANSLATED'] #当前脚本所在文件系统（不是文档根目录）的基本路径。
$_SERVER['SCRIPT_NAME'] #包含当前脚本的路径。这在页面需要指向自己时非常有用。
$_SERVER['REQUEST_URI'] #访问此页面所需的 URI。例如，“/index.html”。
$_SERVER['PHP_AUTH_USER'] #当 PHP 运行在 Apache 模块方式下，并且正在使用 HTTP 认证功能，这个变量便是用户输入的用户名。
$_SERVER['PHP_AUTH_PW'] #当 PHP 运行在 Apache 模块方式下，并且正在使用 HTTP 认证功能，这个变量便是用户输入的密码。
$_SERVER['AUTH_TYPE'] #当 PHP 运行在 Apache 模块方式下，并且正在使用 HTTP 认证功能，这个变量便是认证的类型。
$_SERVER[”HTTP_X_FORWARDED_FOR”] #透过代理服务器取得客户端的真实 IP 地址
$_SERVER['HTTP_VIA'] #代理服务器IP
$_SERVER['HTTP_CLIENT_IP'] #客户端IP
```

POST型：
COOKIE方式提交注入点:可以绕过POST提交时的过滤机制（转义）

HTTP头部注入：