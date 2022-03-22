## Cookie

**setcookie**

设置cookie

```php
setcookie(
    string $name,
    string $value = "",
    int $expires = 0,
    string $path = "",
    string $domain = "",
    bool $secure = false,
    bool $httponly = false
): bool
```

**setrawcookie**

设置未经 URL 编码的 cookie

```php
setrawcookie(
    string $name,
    string $value = ?,
    int $expire = 0,
    string $path = ?,
    string $domain = ?,
    bool $secure = false,
    bool $httponly = false
): bool
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



## Session

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



## JWT

JSON Web Token（JWT）是一个非常轻巧的规范。这个规范允许我们使用JWT在用户和服务器之间传递安全可靠的信息。

一个JWT实际上就是一个字符串，它由三部分组成，头部、载荷与签名。



JWT站点：https://jwt.io

composer jwt

```
composer require firebase/php-jwt
```

使用jwt

```php
use Firebase\JWT\JWT;
use Firebase\JWT\Key;

$key = "example_key";
$payload = array(
    "iss" => "http://example.org",
    "aud" => "http://example.com",
    "iat" => 1356999524,
    "nbf" => 1357000000
);

/**
 * IMPORTANT:
 * You must specify supported algorithms for your application. See
 * https://tools.ietf.org/html/draft-ietf-jose-json-web-algorithms-40
 * for a list of spec-compliant algorithms.
 */
$jwt = JWT::encode($payload, $key, 'HS256');
$decoded = JWT::decode($jwt, new Key($key, 'HS256'));

print_r($decoded);

/*
 NOTE: This will now be an object instead of an associative array. To get
 an associative array, you will need to cast it as such:
*/

$decoded_array = (array) $decoded;

/**
 * You can add a leeway to account for when there is a clock skew times between
 * the signing and verifying servers. It is recommended that this leeway should
 * not be bigger than a few minutes.
 *
 * Source: http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html#nbfDef
 */
JWT::$leeway = 60; // $leeway in seconds
$decoded = JWT::decode($jwt, new Key($key, 'HS256'));
```





## cookie与session的异同点

相同：

1. 可以储存数据

2. 可以做会话控制

3. 可以设置过期时间



不同：

1. 存储位置不同（cookie数据存放在客户的浏览器上，session数据放在服务器上。）

2. 储存大小不同（单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie，而session没有对存储的数据量的限制）

3. 安全性不同（cookie在浏览器上容易被窃取和cookie欺骗）





## session函数

- [session_abort](https://www.php.net/manual/zh/function.session-abort.php) — Discard session array changes and finish session
- [session_cache_expire](https://www.php.net/manual/zh/function.session-cache-expire.php) — 返回当前缓存的到期时间
- [session_cache_limiter](https://www.php.net/manual/zh/function.session-cache-limiter.php) — 读取/设置缓存限制器
- [session_commit](https://www.php.net/manual/zh/function.session-commit.php) — session_write_close 的别名
- [session_create_id](https://www.php.net/manual/zh/function.session-create-id.php) — Create new session id
- [session_decode](https://www.php.net/manual/zh/function.session-decode.php) — 解码会话数据
- [session_destroy](https://www.php.net/manual/zh/function.session-destroy.php) — 销毁一个会话中的全部数据
- [session_encode](https://www.php.net/manual/zh/function.session-encode.php) — 将当前会话数据编码为一个字符串
- [session_gc](https://www.php.net/manual/zh/function.session-gc.php) — Perform session data garbage collection
- [session_get_cookie_params](https://www.php.net/manual/zh/function.session-get-cookie-params.php) — 获取会话 cookie 参数
- [session_id](https://www.php.net/manual/zh/function.session-id.php) — 获取/设置当前会话 ID
- [session_module_name](https://www.php.net/manual/zh/function.session-module-name.php) — 获取/设置会话模块名称
- [session_name](https://www.php.net/manual/zh/function.session-name.php) — 读取/设置会话名称
- [session_regenerate_id](https://www.php.net/manual/zh/function.session-regenerate-id.php) — 使用新生成的会话 ID 更新现有会话 ID
- [session_register_shutdown](https://www.php.net/manual/zh/function.session-register-shutdown.php) — 关闭会话
- [session_reset](https://www.php.net/manual/zh/function.session-reset.php) — Re-initialize session array with original values
- [session_save_path](https://www.php.net/manual/zh/function.session-save-path.php) — 读取/设置当前会话的保存路径
- [session_set_cookie_params](https://www.php.net/manual/zh/function.session-set-cookie-params.php) — 设置会话 cookie 参数
- [session_set_save_handler](https://www.php.net/manual/zh/function.session-set-save-handler.php) — 设置用户自定义会话存储函数
- [session_start](https://www.php.net/manual/zh/function.session-start.php) — 启动新会话或者重用现有会话
- [session_status](https://www.php.net/manual/zh/function.session-status.php) — 返回当前会话状态
- [session_unset](https://www.php.net/manual/zh/function.session-unset.php) — 释放所有的会话变量
- [session_write_close](https://www.php.net/manual/zh/function.session-write-close.php) — Write session data and end session

