## 解释

PSR-4规范：  将PHP 命名空间映射到文件系统的规则，并且可以与其他 SPL 注册的自动加载器共存。

> 也就是说类的命名空间要与文件相互对应，如类文件在
>
> App/Controller/IndexController.php下，则
>
> ```php
> <?php
> 
> namespace App\Controller;
> 
> class IndexController{
>     
> }
> ```
>
> 这样一来，命名框架加上类名称就可以确定类文件的所在路径了



## 实现

在项目中，要实现类的自动加载的话，可以使用类的自动注册函数

```
spl_autoload_register(?callable $callback, bool $throw = true, bool $prepend = false): bool
```

**案例**

> Project:
>
> │  autoload.php
> │  index.php
>
> │
> └─utils
>         Email.php



**utils/Email.php**

```php
<?php
    
declare(strict_types=1);

namespace utils;

class Email
{
	
	function __construct()
	{
		echo 'Email';
	}
}
```

**autoload.php**

```php
<?php
    
declare(strict_types=1);

spl_autoload_register('autoload');

function autoload($class){
	require __DIR__.'/'.$class.'.php';
}
```

**index.php**

```php
<?php

declare(strict_types=1);

require 'autoload.php';

use utils\Email;
$email = new Email();

```

