## 设计原则

> 单一原则：一个类只需要做好一件事情。
>
> 开放封闭：一个类应该是可扩展的，而不可修改的。
>
> 依赖倒置：一个类，不应该强依赖于另一个类，每个类对于另一个类都是可替换的。
>
> 配置化：尽可能的使用配置化，而不是硬编码。
>
> 面向接口：只需要关心接口，不需要关心实现。



## 创建类

```php

class ClassName{
    // 类属性
    
    // 类方法  
}

```



## 继承类

当继承一个类时，子类就会继承父类所有 public 和 protected 的方法，属性和常量。

```php

class ClassNameA{
    // 类属性
    
    // 类方法
}

class ClassNameB extends ClassNameA{
    // 类属性
    
    // 类方法
}
```

注：PHP的继承为单继承，不能同时继承多个父类



## 实现接口

```php

interface InterfaceA{
    
   public function add(); 
    
}

class ClassNameA implements InterfaceA{
    
   public function add(){
       
   }
}
```

注：PHP可以同时实现多个接口，如

```php

interface InterfaceA{
    
   public function add();
    
}

interface InterfaceB{
    
   public function delete(); 
    
}

class ClassNameA implements InterfaceA,InterfaceB{
   
   public function add(){
       
   }
    
   public function delete(){
       
   }
}
```



## trait的使用

trait可以让PHP实现类型多继承的功能，如

```php
trait Food
{
    public function eat()
    {
        echo 'eating...';
    }
}

trait Sport
{
    public function run()
    {
        echo 'run...';
    }
}

class Person
{
    use Food;
    use Sport;
}

$person = new Person();
$person->eat();
$person->run();
```

