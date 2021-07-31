## Cookie

**cookie设置函数**

```php
bool setcookie (
 string $name
 [, string $value = ""
 [, int $expire = 0
 [, string $path = ""
 [, string $domain = ""
 [, bool$secure = false 
 [, bool $httponly = false ]]]]]]
)
```

> **1 name**
> Cookie 名称。
>
> value
> Cookie 值。 这个值储存于用户的电脑里，请勿储存敏感信息。 比如 name 是 'cookiename'， 可通过 
> $_COOKIE['cookiename'] 获取它的值。
>
> **2 expire**
> Cookie 的过期时间。 这是个 Unix 时间戳，即 Unix 纪元以来（格林威治时间 1970 年 1 月 1 日 
> 00:00:00）的秒数。 也就是说，基本可以用 time() 函数的结果加上希望过期的秒数。 或者也可以用 
> mktime()。 time()+60*60*24*30 就是设置 Cookie 30 天后过期。 如果设置成零，或者忽略参数，
>  Cookie 会在会话结束时过期（也就是关掉浏览器时）。
>
> Note:
>
> 你可能注意到了，expire 使用 Unix 时间戳而非 Wdy, DD-Mon-YYYY HH:MM:SS GMT 这样的日期格式，是
> 因为 PHP 内部作了转换。
>
> **3 path**
> Cookie 有效的服务器路径。 设置成 '/' 时，Cookie 对整个域名 domain 有效。 如果设置成 '/foo/'，
>  Cookie 仅仅对 domain 中 /foo/ 目录及其子目录有效（比如 /foo/bar/）。 默认值是设置 Cookie 时
> 的当前目录。
>
> **4 domain**
> Cookie 的有效域名/子域名。 设置成子域名（例如 'www.example.com'），会使 Cookie 对这个子域名和
> 它的三级域名有效（例如 w2.www.example.com）。 要让 Cookie 对整个域名有效（包括它的全部子域
> 名），只要设置成域名就可以了（这个例子里是 'example.com'）。
>
> 旧版浏览器仍然在使用废弃的 » RFC 2109， 需要一个前置的点 . 来匹配所有子域名。
>
> **5 secure**
> 设置这个 Cookie 是否仅仅通过安全的 HTTPS 连接传给客户端。 设置成 TRUE 时，只有安全连接存在时才
> 会设置 Cookie。 如果是在服务器端处理这个需求，程序员需要仅仅在安全连接上发送此类 Cookie （通过 
> $_SERVER["HTTPS"] 判断）。
>
> **6 httponly**
> 设置成 TRUE，Cookie 仅可通过 HTTP 协议访问。 这意思就是 Cookie 无法通过类似 JavaScript 这样的
> 脚本语言访问。 要有效减少 XSS 攻击时的身份窃取行为，可建议用此设置（虽然不是所有浏览器都支持），
> 不过这个说法经常有争议。 PHP 5.2.0 中添加。 TRUE 或 FALSE

**设置cookie**

```php
<?php
setcookie('username','lwqbrell');
?>
```

**去除cookie**
方式一：用unset($_COOKIE[name])去除该变量。

方式二：将cookie设为过去时间，setcookie(name,value,time-1);

**获取cookie值**
可以使用$_COOKIE，需要注意的是cookie是在下次刷新才生效的

```php
<?php
setcookie('name','lwqbrell');
var_dump($_COOKIE);
?>
```



## session

**session文件在服务器的位置**
php.ini文件中session.save_path既是session文件的存储位置。

开启会话

```
bool session_start ([ array $options = array() ] )
```

> options
> 此参数是一个关联数组，如果提供，那么会用其中的项目覆盖 会话配置指示 中的配置项。此数组中的键无需包含 

**设置session**

```php
$_SESSION[key]=value
```

```php
<?php
session_start();
$_SESSION['name']='brell';
$_SESSION['age']=22;
$_SESSION['sex']='boy';
var_dump($_SESSION);
?>
```

**禁用cookie后如何使用session**

> cookie被禁用后任然可以使用session，只是不推荐这么做，那么cookie被禁用后要如何使用session呢，答案就是通过URL传递sessionID来获取

```php
<?php
header('Content-Type: text/html; charset=utf-8');

session_start();
$_SESSION['name']='trevor';
$_SESSION['age']='23';

echo "<a href='./session.php?'".session_name()."=".session_id()."'>URL传sessionid</a>";
?>
```

```php
<?php
session_id($_GET[session_name()]);
session_start();
echo $_SESSION['name'];
?>
```



![img](https://cdn.coder369.com/img/blog/20190106184400210.png)