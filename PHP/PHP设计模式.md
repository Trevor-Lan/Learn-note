## 1 工厂模式

> - 使用工厂方法或者类生成对象，而不是在代码中直接new

```php
class Person
{
    public string $age;
    public string $name;

    public function study()
    {
    }

    public function eat()
    {
    }

    public function sleep()
    {
    }

    public function work()
    {
    }
}

class Factory
{
    public static function instancePerson(): Person
    {
        return new Person();
    }
}
```



## 2 单例模式

> - 类对象仅允许创建一个
>
> - 构造方法声明为私有

```php
class Database
{

    private static $db;

    private function __construct()
    {

    }

    static function getInstance(): Database
    {
        if (!self::$db) {
            self::$db = new self();
        }
        return self::$db;
    }
}
```



## 3 注册模式

> - 全局共享和交换对象

```php
class Register
{
    protected static $object;

    static function set($alis, $obj)
    {
        self::$object[$alis] = $obj;
    }

    static function get($alis)
    {
        return self::$object[$alis];
    }

    static function unset($alis)
    {
        unset(self::$object[$alis]);
    }
}

class Person
{
    public string $age;
    public string $name;

    public function study()
    {
    }

    public function eat()
    {
    }

    public function sleep()
    {
    }

    public function work()
    {
    }
}
```

```php
$person = new Person();
Register::set(Person::class, $person);
```



## 4 适配器模式

> - 将不同的函数接口封装成统一的API，比如：
>
> - 数据库适配器：mysql、mysqli、pdo
>
> - 缓存适配器：file、redis、memcache

```php
interface DatabaseInterface
{
    public function connect();

    public function query();

    public function insert();

    public function update();

    public function delete();
}

class DiyMysqli implements DatabaseInterface
{

    public function connect()
    {
        // TODO: Implement connect() method.
    }

    public function query()
    {
        // TODO: Implement query() method.
    }

    public function insert()
    {
        // TODO: Implement insert() method.
    }

    public function update()
    {
        // TODO: Implement update() method.
    }

    public function delete()
    {
        // TODO: Implement delete() method.
    }
}

class DiyPDO implements DatabaseInterface
{

    public function connect()
    {
        // TODO: Implement connect() method.
    }

    public function query()
    {
        // TODO: Implement query() method.
    }

    public function insert()
    {
        // TODO: Implement insert() method.
    }

    public function update()
    {
        // TODO: Implement update() method.
    }

    public function delete()
    {
        // TODO: Implement delete() method.
    }
}
```



## 5 策略模式

> - 将一组特定的行为和算法封装成类，以适应某些特定的上下文环境，比如首页根据不同活动来展示不同的广告。

```php
/**
 * 策略接口
 */
interface AdvStrategyInterface
{
    public function showAdv();
}

/**
 * 秒杀广告
 */
class SeckillAdvStrategy implements AdvStrategyInterface
{
    public function showAdv()
    {
        // TODO: Implement showAdv() method.
    }
}

/**
 * 促销广告
 */
class PromotionAdvStrategy implements AdvStrategyInterface
{
    public function showAdv()
    {
        // TODO: Implement showAdv() method.
    }
}

/**
 * 电商系统
 */
class System
{
    /**
     * @var AdvStrategyInterface
     */
    protected $strategy;

    /**
     * 首页展现位
     */
    public function index()
    {
        $this->strategy->showAdv();
    }

    /**
     * 设置策略
     * @param AdvStrategyInterface $strategy
     */
    public function setStrategy(AdvStrategyInterface $strategy)
    {
        $this->strategy = $strategy;
    }
}
```

```php
$system = new System();
$system->setStrategy(new SeckillAdvStrategy());
$system->index();
```



## 6 数据对象映射模式（ORM）

> - 将对象和数据存储映射起来，对一个对象的操作会映射为堆数据存储的操作

```php
class UserModel
{
    public int $id;
    public string $name;
    public string $age;
    public string $address;

    public function __construct(int $id)
    {
        // 初始化数据
    }

    public function __destruct()
    {
        // 更新数据
    }
}
```

```php
$user = new UserModel(1);
$user->name = 'new name';
$user->name = 22;
$user->address = 'new address';
```



## 7 观察者模式

> - 当对象状态发生变化时，依赖它的对象会收到通知，并自动更新，实现了低耦合，非侵入式的通知与更新机制。

```php
/**
 * 观察者接口
 */
interface Observer
{
    public function update();
}

/**
 * 更新事件观察者
 */
class UpdateEventObserver implements Observer
{
    public function update()
    {
        // TODO: Implement update() method.
    }
}

/**
 * 添加事件观察者
 */
class AddEventObserver implements Observer
{
    public function update()
    {
        // TODO: Implement update() method.
    }
}

/**
 * 事件生成器
 */
abstract class EvenGenerator
{
    private array $observer = [];

    public function add(Observer $observer)
    {
        $this->observer[] = $observer;
    }

    public function notify()
    {
        foreach ($this->observer as $observer) {
            $observer->update();
        }
    }
}

/**
 * 特定事件
 */
class Event extends EvenGenerator
{
    public function trigger()
    {
        $this->notify();
    }
}

```

```php
$e = new Event();
$e->add(new AddEventObserver());
$e->add(new UpdateEventObserver());
$e->notify();
```



## 8 原型模式

> - 与工厂模式作用类似，都是用来创建对象
>
> - 与工厂模式的实现不同，原型模式是先创建好一个原型对象，然后通过clone原型对象来创建新的对象，这样就免去类创建时的重复的初始化操作。
>
> - 原型模式适用于大对象的创建，创建一个大的对象需要很大的开销，如果每次new就会消耗很大，而原型模式仅需内存拷贝即可。

```php
class Person
{
    public string $age;
    public string $name;

    public function study()
    {
    }

    public function eat()
    {
    }

    public function sleep()
    {
    }

    public function work()
    {
    }
}
```

```php
$person1 = new Person();
$person2 = clone $person1;
```



## 9 装饰器模式

> - 可以动态的修改类的功能。
>
> - 一个类提供了一项功能，如果在修改并添加额外的功能，传统的编码模式，需要写一个子类继承它，并重新实现类的方法。
>
> - 仅需在运行时添加一个装饰器对象即可实现，可以实现最大化的灵活性。

```php
/**
 * 装饰器接口
 */
interface DecoratorInterface
{
    public function before();

    public function after();
}

/**
 * 家具装饰器
 */
class FurnitureDecorator implements DecoratorInterface
{

    public function before()
    {
        // TODO: Implement before() method.
    }

    public function after()
    {
        // TODO: Implement after() method.
    }
}

/**
 * 房子
 */
class House
{
    protected array $decorator;

    /**
     * 添加装饰器
     *
     * @param DecoratorInterface $decorator
     */
    public function addDecorator(DecoratorInterface $decorator)
    {
        $this->decorator[] = $decorator;
    }

    /**
     * 销售前
     */
    public function before()
    {
        foreach ($this->decorator as $decorator) {
            $decorator->before();
        }
    }

    /**
     * 销售后
     */
    public function after()
    {
        $this->decorator = array_reverse($this->decorator);
        foreach ($this->decorator as $decorator) {
            $decorator->after();
        }
    }

    /**
     * 销售房子
     */
    public function sale()
    {
        $this->before();
        // 业务代码
        $this->after();
    }
}
```

```php
$house = new House();
$house->addDecorator(new FurnitureDecorator());
$house->sale();
```



## 10 迭代器模式

> - 在不需要了解内部实现的前提下，遍历一个聚合对象的内部元素。
>
> - 相比于传统的编码模式，迭代器模式可以隐藏遍历元素的所需的操作。

```php
class NewIterator implements Iterator{

    public function current()
    {
        // TODO: Implement current() method.
    }

    public function next()
    {
        // TODO: Implement next() method.
    }

    public function key()
    {
        // TODO: Implement key() method.
    }

    public function valid()
    {
        // TODO: Implement valid() method.
    }

    public function rewind()
    {
        // TODO: Implement rewind() method.
    }
}
```



## 11 代理模式

> - 在客户端与实体之间建立一个代理对象，客户端对实体进行操作全部委派给代理对象，隐藏实体的具体实现细节。
> - 代理还可以与业务代码分离，部署到另外的服务器，业务代码中通过RPC来委派。

```php
interface UserProxy
{
    public function get(int $id);
}

class Proxy implements UserProxy
{
    public function get(int $id)
    {
        // TODO: Implement get() method.
    }
}
```

