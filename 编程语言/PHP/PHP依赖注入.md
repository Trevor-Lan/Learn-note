## 依赖注入与控制反转

DI（Dependency Injection，简称DI）：依赖注入（当创建的对象依赖另外的对象时，自动注入依赖的对象）

IoC（Inversion of Control，简称IoC）：控制反转（将对象的控制器交由容器管理）

依赖注入的实现：https://php-di.org/doc/getting-started.html



## PSR-11 容器接口

**接口**

```php
<?php
namespace Psr\Container;

/**
 * 容器的接口类，提供了获取容器中对象的方法。
 */
interface ContainerInterface
{
    /**
     * 在容器中查找并返回实体标识符对应的对象。
     *
     * @param string $id 查找的实体标识符字符串。
     *
     * @throws NotFoundExceptionInterface  容器中没有实体标识符对应对象时抛出的异常。
     * @throws ContainerExceptionInterface 查找对象过程中发生了其他错误时抛出的异常。
     *
     * @return mixed 查找到的对象。
     */
    public function get($id);

    /**
     * 如果容器内有标识符对应的内容时，返回 true 。
     * 否则，返回 false。
     *
     * 调用 `has($id)` 方法返回 true，并不意味调用  `get($id)` 不会抛出异常。
     * 而只意味着 `get($id)` 方法不会抛出 `NotFoundExceptionInterface` 实现类的异常。
     *
     * @param string $id 查找的实体标识符字符串。
     *
     * @return bool
     */
    public function has($id);
}
```

**基础异常类**

```php
<?php
    
namespace Psr\Container;

/**
 * 容器中的基础异常类。
 */
interface ContainerExceptionInterface
{
}
```

**没有查找到对应对象时的异常**

```php
<?php
namespace Psr\Container;

/**
 * 容器中没有查找到对应对象时的异常
 */
interface NotFoundExceptionInterface extends ContainerExceptionInterface
{
}
```



## 实现

> 注：该容器实现类并未考虑异常情况，可根据自己的业务情况抛异常

```php
<?php
    
namespace Di;

use Psr\Container\ContainerInterface;

class Container implements ContainerInterface
{
    /**
     * 注册树
     *
     * @var array
     */
    protected array $register;

    /**
     * @throws ReflectionException
     */
    public function get(string $class)
    {
        // 构造函数参数
        $constructorParams = [];
        // 判断当前类是否已注册
        if (isset($this->register[$class])) {
            return $this->register[$class];
        }
        // 反射类
        $reflector = new ReflectionClass($class);
        // 是否需要处理构造函数
        if ($reflector->getConstructor()) {
            // 构造函数参数
            $params = $reflector->getConstructor()->getParameters();
            if (!empty($params)) {
                foreach ($params as $param) {
                    // 反射参数类
                    $paramReflector = new ReflectionClass($param->getClass()->name);
                    // 参数类名
                    $paramClass = $paramReflector->name;
                    // 递归实例化参数
                    $constructorParams[] = $this->get($paramClass);
                }
            }
        }
        if (!empty($constructorParams)) {
            return new $class(...$constructorParams);
        }
        $object = new $class();
        // 更新注册树
        $this->register[$class] = $object;
        return $object;
    }

    /**
     * @param string $class
     * @return bool
     */
    public function has(string $class): bool
    {
        return isset($this->register[$class]);
    }
}
```

## 使用

```php
<?php

use Di\Container;
    
class Person
{
    public function eat()
    {
        var_dump('eat');
    }
}

$container = new Container();
/**
* @var Person
*/
$person = $container->get(Person:class);
$person->eat()
```

