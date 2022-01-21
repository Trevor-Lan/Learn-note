## 10个常用的socket函数

创建socket

```php
socket_create(int $domain, int $type, int $protocol): Socket|false
```

绑定socket

```php
socket_bind(Socket $socket, string $address, int $port = 0): bool
```

设置阻塞状态

```php
socket_set_block(Socket $socket): bool
```

监听socket

```php
socket_listen(Socket $socket, int $backlog = 0): bool
```

连接socket

```php
socket_connect(Socket $socket, string $address, ?int $port = null): bool
```

接受socket上的连接

```php
socket_accept(Socket $socket): Socket|false
```

接收数据（请求）

```php
socket_read(Socket $socket, int $length, int $mode = PHP_BINARY_READ): string|false
```

回复数据（响应）

```php
socket_write(Socket $socket, string $data, ?int $length = null): int|false
```

错误信息

```php
socket_strerror(int $error_code): string
```

错误代码

```php
socket_last_error(?Socket $socket = null): int
```



## 服务端

```php
<?php
// 不限制运行时间    
set_time_limit(0);
// 待绑定的IP
$address = "127.0.0.1";
// 待绑定的接口
$port = 9527;
// 创建socket
$socket = socket_create(AF_INET, SOCK_STREAM, SOL_TCP);
// 设置阻塞模式（不写也行，默认就是阻塞模式）
socket_set_block($socket);
// 绑定socket
socket_bind($socket, $address, $port);
// 监听socket
socket_listen($socket, 4);
while (true) {
    // 从socket上获取连接
    $request_connect = socket_accept($socket);
    // 读取连接数据
    $msg = socket_read($request_connect, 2048);
    var_dump($msg);
    $response = "Response success";
    // 响应数据
    socket_write($request_connect, $response, strlen($response));
    // 关闭连接
    socket_close($request_connect);
} 

```



## 客户端

```php
<?php
    
$host = "127.0.0.1";
$port = 9527;
$socket = socket_create(AF_INET, SOCK_STREAM, SOL_TCP);
socket_connect($socket, $host, $port);
$msg = "Hello world";
socket_write($socket, $msg);
$response = socket_read($socket,2048);
var_dump($response);
socket_close($socket);

```

## 获取错误

```php
<?php

$error_code = socket_last_error();
socket_strerror($error_code);

```



