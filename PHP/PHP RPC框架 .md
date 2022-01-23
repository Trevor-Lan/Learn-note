composer require hprose/hprose



服务端

```php
<?php
require 'vendor/autoload.php';
use Hprose\Socket\Server;

function hello($name): string
{
    return "Hello {$name}";
}

$server = new Server("tcp://0.0.0.0:3344");
$server->setErrorTypes(E_ALL);
$server->setDebugEnabled();
try {
    $server->addFunction('hello');
} catch (Exception $e) {
}
$server->start();
```



客户端

```php
<?php
require_once "./vendor/autoload.php";

use Hprose\Future;
use Hprose\Socket\Client;

$client = new Client("tcp://127.0.0.1:3344");
$client->fullDuplex = true;

Future\co(function () use ($client) {
    try {
        var_dump((yield $client->hello("trevor")));
    } catch (\Exception $e) {
        echo $e->getMessage();
    }
});
```

