## 服务端

```php
<?php
set_time_limit(0);
$address = "127.0.0.1";
$port = 9527;
/**
 * 创建一个SOCKET
 * AF_INET=是ipv4 如果用ipv6，则参数为 AF_INET6
 * SOCK_STREAM为socket的tcp类型，如果是UDP则使用SOCK_DGRAM
 */
$sock = socket_create(AF_INET, SOCK_STREAM, SOL_TCP);
//阻塞模式
socket_set_block($sock);
//绑定到socket端口
socket_bind($sock, $address, $port);
//开始监听
socket_listen($sock, 4);
while (true) {
    $accept = socket_accept($sock);
    $msg = socket_read($accept, 8192);
    echo "Received:" . $msg;
    $response = "Request success";
    socket_write($accept, $response, strlen($response));
    socket_close($accept);
} 
```



## 客户端

```php
<?php
set_time_limit(0);
$host = "127.0.0.1";
$port = 9527;
$socket = socket_create(AF_INET, SOCK_STREAM, SOL_TCP);
socket_connect($socket, $host, $port);
$msg = "Hello world";
socket_write($socket, $msg);
while ($buff = @socket_read($socket, 1024, PHP_NORMAL_READ)) {
    echo("Response:" . $buff);
}
socket_close($socket);
```



