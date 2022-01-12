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



## 项目结构

```
DiyFramework:
├─app
│  ├─Command
│  ├─Controller
│  ├─Exception
│  └─Model
├─boot
│  └─System.php
├─config
├─public
│  ├─nginx.htaccess
│  └─index.php
├─route
├─runtime
│  ├─log
│  └─cache
├─utils
└─vendor
|
└─command.php
└─.env
└─composer.json
```



入口文件

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
require_once BASE_PATH . '/boot/System.php';

// 初始化项目
\Boot\System::init();
// 启动项目
\Boot\System::run();

```





自动加载



项目配置

依赖注入

路由

缓存

日志

ORM

命令行