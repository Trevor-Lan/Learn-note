## 初始化项目

```
composer init
```

```
This command will guide you through creating your composer.json config.

Package name (<vendor>/<name>) [administrator/demo]:
Description []:
Author [Trevor-Lan , n to skip]:
Minimum Stability []:
Package Type (e.g. library, project, metapackage, composer-plugin) []:
License []:

Define your dependencies.

Would you like to define your dependencies (require) interactively [yes]? n
Would you like to define your dev dependencies (require-dev) interactively [yes]? n

{
    "name": "administrator/demo",
    "authors": [
        {
            "name": "Trevor-Lan",
            "email": "61399914+Trevor-Lan@users.noreply.github.com"
        }
    ],
    "require": {}
}

Do you confirm generation [yes]? y

```

## 引入依赖库

```json
{
  "name": "administrator/ark-server",
  "authors": [
    {
      "name": "Trevor-Lan",
      "email": "61399914+Trevor-Lan@users.noreply.github.com"
    }
  ],
  "require": {
    "nikic/fast-route": "^1.3",
    "symfony/console": "^5.4",
    "symfony/dotenv": "^5.4",
    "ext-json": "*",
    "topthink/think-orm": "^2.0",
    "topthink/think-validate": "^2.0",
    "predis/predis": "^1.1",
    "php-di/php-di": "^6.3",
    "smarty/smarty": "^4.0",
    "psr/log": "^1.1"
  }
}

```



## 项目结构

```
DiyFramework:
├─app
│  ├─Command
│  ├─Controller
│  ├─Exception
│  ├─View
│  └─Model
├─config
├─public
│    nginx.htaccess
│    index.php
├─route
├─runtime
│  ├─log
│  └─cache
├─utils
|    Framework.php
|    Env.php
|    Config.php
|    Cache.php
|    Log.php
|    Redis.php
|    Request.php
|    Response.php
|    View.php
└─vendor
command.php
.env
composer.json
```



## 入口文件

路径：public/index.php

```php
<?php

// 定义项目根目录为全局常量
define('BASE_PATH', dirname(__DIR__, 1));
// 设置时区
ini_set('date.timezone', 'Asia/Shanghai');
// 设置错误级别
error_reporting(E_ALL);
// composer自动加载
require_once BASE_PATH . '/vendor/autoload.php';
require_once BASE_PATH . '/Utils/Framework.php';

// 运行项目
\Utils\Framework::run();

```



## 核心模块

路径：app/Utils/Framework.php

```php
<?php

declare(strict_types=1);

namespace Utils;

use App\Exception\Handler\ExceptionHandler;
use DI\ContainerBuilder;
use FastRoute\Dispatcher;
use Route\App;
use Symfony\Component\Dotenv\Dotenv;
use think\facade\Db;


class Framework
{
    /**
     * 运行框架
     */
    public static function run()
    {
        self::initAutoload();
        self::initExceptionHandler();
        self::initEnv();
        self::initDatabase();
        self::response(self::request(App::route()));
    }

    /**
     * 自动加载（PSR-4 自动加载规范）
     */
    protected static function initAutoload()
    {
        // 自定义自动加载
        spl_autoload_register(function ($class) {
            include BASE_PATH . '/' . $class . '.php';
        });
    }

    /**
     * 异常接管
     */
    protected static function initExceptionHandler()
    {
        set_exception_handler(function ($exception) {
            ExceptionHandler::handler($exception);
        });
    }

    /**
     * 加载环境变量
     */
    protected static function initEnv()
    {
        $dotenv = new Dotenv();
        $dotenv->load(BASE_PATH . '/.env');
    }

    /**
     *
     */
    protected static function initDatabase()
    {
        Db::setConfig([
            // 默认数据连接标识
            'default' => 'mysql',
            // 数据库连接信息
            'connections' => [
                'mysql' => [
                    'type' => 'mysql',
                    'hostname' => Env::get('DB_HOSTNAME'),
                    'username' => Env::get('DB_USERNAME'),
                    'password' => Env::get('DB_PASSWORD'),
                    'database' => Env::get('DB_DATABASE'),
                    'charset' => 'utf8',
                    'prefix' => '',
                    'debug' => Env::get('DB_DEBUG'),
                ],
            ],
        ]);
    }

    /**
     * 处理请求
     *
     * @param Dispatcher $dispatcher
     * @return mixed
     */
    protected static function request(Dispatcher $dispatcher)
    {
        $httpMethod = $_SERVER['REQUEST_METHOD'];
        $uri = $_SERVER['REQUEST_URI'];
        if (false !== $pos = strpos($uri, '?')) {
            $uri = substr($uri, 0, $pos);
        }
        $uri = rawurldecode($uri);
        return $dispatcher->dispatch($httpMethod, $uri);
    }

    /**
     * @param array $routeInfo
     * @throws \Exception
     */
    protected static function response(array $routeInfo)
    {
        switch ($routeInfo[0]) {
            case \FastRoute\Dispatcher::NOT_FOUND:
                echo 'Not found';
                break;
            case \FastRoute\Dispatcher::METHOD_NOT_ALLOWED:
                $allowedMethods = $routeInfo[1];
                echo 'Not allow';
                break;
            case \FastRoute\Dispatcher::FOUND:
                $handler = $routeInfo[1];
                $vars = $routeInfo[2];
                $controller = explode('@', $handler);
                if (!empty($controller) && count($controller) === 2) {
                    self::di($controller, $vars);
                } else {
                    echo '控制器不存在';
                }
                break;
        }
    }

    /**
     * @throws \Exception
     */
    public static function di(array $controller, array $vars)
    {
        $containerBuilder = new ContainerBuilder;
        $container = $containerBuilder->build();
        /**
         * 容器管理，支持依赖注入
         */
        $container->call($controller, $vars);
    }
}
```



## 配置文件

**环境配置**

路径：utils/Env.php

```php
<?php

declare(strict_types=1);

namespace Utils;

class Env
{
    /**
     * @param string $key
     * @param null $value
     * @return mixed|null
     */
    public static function get(string $key, $value = null)
    {
        return $_ENV[$key] ?? $value;
    }
}
```

**项目配置**

路径：utils/Config.php

```php
<?php

declare(strict_types=1);

namespace Utils;

class Config
{
    /**
     * @param string|null $key
     * @return array|mixed
     */
    public static function get(string $key = null)
    {
        $res = scandir(BASE_PATH . '/config');
        unset($res[0], $res[1]);
        $config = [];
        if (!empty($res)) {
            foreach ($res as $item) {
                $file = explode('.', $item);
                $config[$file[0]] = include BASE_PATH . '/config/' . $item;
            }
        }
        $keyConfig = explode('.', $key);
        foreach ($keyConfig as $key) {
            $config = $config[$key];
        }
        return $config;
    }
}
```

## 缓存

PSR-16 缓存接口规范

路径：utils/Cache.php

```php
<?php

declare(strict_types=1);

namespace Utils;

use Psr\SimpleCache\CacheInterface;

class Cache implements CacheInterface
{
    public function get($key, $default = null)
    {
        // TODO: Implement get() method.
    }

    public function set($key, $value, $ttl = null)
    {
        // TODO: Implement set() method.
    }

    public function delete($key)
    {
        // TODO: Implement delete() method.
    }

    public function clear()
    {
        // TODO: Implement clear() method.
    }

    public function getMultiple($keys, $default = null)
    {
        // TODO: Implement getMultiple() method.
    }

    public function setMultiple($values, $ttl = null)
    {
        // TODO: Implement setMultiple() method.
    }

    public function deleteMultiple($keys)
    {
        // TODO: Implement deleteMultiple() method.
    }

    public function has($key)
    {
        // TODO: Implement has() method.
    }
}
```



## 日志

 PSR-3 日志接口规范

路径：utils/Log.php

```php
<?php

declare(strict_types=1);

namespace Utils;

use Psr\Log\LoggerInterface;

class Log implements LoggerInterface
{

    public function emergency($message, array $context = array())
    {
        // TODO: Implement emergency() method.
    }

    public function alert($message, array $context = array())
    {
        // TODO: Implement alert() method.
    }

    public function critical($message, array $context = array())
    {
        // TODO: Implement critical() method.
    }

    public function error($message, array $context = array())
    {
        // TODO: Implement error() method.
    }

    public function warning($message, array $context = array())
    {
        // TODO: Implement warning() method.
    }

    public function notice($message, array $context = array())
    {
        // TODO: Implement notice() method.
    }

    public function info($message, array $context = array())
    {
        // TODO: Implement info() method.
    }

    public function debug($message, array $context = array())
    {
        // TODO: Implement debug() method.
    }

    public function log($level, $message, array $context = array())
    {
        // TODO: Implement log() method.
    }
}
```



## Redis

路径：utils/Redis.php

```php
<?php

declare(strict_types=1);

namespace Utils;

use Predis\Client;

class Redis
{
    /**
     * @param int $select
     * @return Client
     */
    public static function instance(int $select = 0): Client
    {
        $config = Config::get('redis');
        $config['database'] = $select;
        return new Client($config);
    }

}
```



## 请求

路径：utils/Request.php

```php
<?php

declare(strict_types=1);

namespace Utils;

class Request
{
    /**
     * @return array
     */
    public static function get(): array
    {
        if (!empty($_GET)) {
            foreach ($_GET as $k => $value) {
                $_GET[$k] = trim($value);
            }
        }
        unset($_GET['s']);
        return $_GET;
    }

    /**
     * @return array
     */
    public static function post(): array
    {
        if (!empty($_POST)) {
            foreach ($_POST as $k => $value) {
                $_POST[$k] = trim($value);
            }
        }
        return $_POST;
    }

    /**
     * @return array
     */
    public static function body(): array
    {
        $body = @file_get_contents('php://input');
        return json_decode($body, true);
    }

    /**
     * @return array
     */
    public static function file(): array
    {
        return $_FILES;
    }

}
```



## 响应

路径：utils/Response.php

```php
<?php

declare(strict_types=1);

namespace Utils;

class Response
{
    /**
     * @param array|null $data
     * @param string $msg
     */
    public static function success(array $data = null, string $msg = 'success')
    {
        header("Content-type: application/json");
        echo json_encode([
            'code' => 200,
            'msg' => $msg,
            'data' => $data
        ]);
    }

    /**
     * @param string $msg
     */
    public static function fail(string $msg = 'fail')
    {
        header("Content-type: application/json");
        echo json_encode([
            'code' => 0,
            'msg' => $msg,
        ]);
    }

}
```



## 视图

路径：utils/View.php

```php
<?php

declare(strict_types=1);

namespace Utils;

use Smarty;

class View extends Smarty
{
    public function __construct()
    {
        $this->setTemplateDir(BASE_PATH . '/app/view/');
        $this->setCompileDir(BASE_PATH . '/runtime/compile/');
        parent::__construct();
    }
}
```



## 路由

路径：route/App.php

```php
<?php

declare(strict_types=1);

namespace Route;

use FastRoute\Dispatcher;

class App
{
    /**
     * @return Dispatcher
     */
    public static function route(): Dispatcher
    {
        return \FastRoute\simpleDispatcher(function (\FastRoute\RouteCollector $r) {
            $r->addRoute('GET', '/', 'App\Controller\Index\Action\IndexAction@index');
        });
    }
}
```



## 模型

```php
<?php

declare(strict_types=1);

namespace APP\Model;

use think\Model;

class UserModel extends Model
{
    protected $table = 'table_name';
}
```



## 命令行

路径：command.php

```php
<?php

const BASE_PATH = __DIR__;
require_once BASE_PATH . '/vendor/autoload.php';
// 自定义自动加载
spl_autoload_register(function ($class) {
    include BASE_PATH . '/' . $class . '.php';
});

use App\Command\NewCommand;
use Symfony\Component\Console\Application;

$application = new Application();

$application->add(new NewCommand());

try {
    $application->run();
} catch (Exception $e) {
}
```

