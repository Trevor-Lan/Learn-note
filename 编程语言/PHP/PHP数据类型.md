## 布尔（Boolean）

布尔表达真假值，可以为 **`true`** 或 **`false`**（不区分大小写）

**注：以下情况的布尔值都为false**

> 布尔值为false
> 空字符串
> 空数组
> 整型值 0
> 浮点型值 0.0
> 字符串 "0"
> NULL



## 整型（Integer）

整型可以表示二进制、八进制、十进制、十六进制

> 二进制以0b开头
>
> 八进制以0o开头
>
> 十六进制以0x开头



## 浮点（Float）

浮点型（也叫浮点数 float，双精度数 double 或实数 real）

```php
<?php
$a = 1.234; 
$b = 1.2e3; 
$c = 7E-10;
$d = 1_234.567; // 从 PHP 7.4.0 开始支持
?>
```

> 浮点类型不能用于精确的数学运算



## 字符（String）

由一系列的字符组成，其中每个字符等同于一个字节

> - [单引号](https://www.php.net/manual/zh/language.types.string.php#language.types.string.syntax.single)
> - [双引号](https://www.php.net/manual/zh/language.types.string.php#language.types.string.syntax.double)
> - [heredoc 语法结构](https://www.php.net/manual/zh/language.types.string.php#language.types.string.syntax.heredoc)
> - [nowdoc 语法结构](https://www.php.net/manual/zh/language.types.string.php#language.types.string.syntax.nowdoc)



## 数组（Array）

数据的集合

```php
$a = array();
$b = [];
```

超全局数组

- [$GLOBALS](https://www.php.net/manual/zh/reserved.variables.globals.php)
- [$_SERVER](https://www.php.net/manual/zh/reserved.variables.server.php)
- [$_GET](https://www.php.net/manual/zh/reserved.variables.get.php)
- [$_POST](https://www.php.net/manual/zh/reserved.variables.post.php)
- [$_FILES](https://www.php.net/manual/zh/reserved.variables.files.php)
- [$_COOKIE](https://www.php.net/manual/zh/reserved.variables.cookies.php)
- [$_SESSION](https://www.php.net/manual/zh/reserved.variables.session.php)
- [$_REQUEST](https://www.php.net/manual/zh/reserved.variables.request.php)
- [$_ENV](https://www.php.net/manual/zh/reserved.variables.environment.php)





## 可迭代对象（Iterable）

[Iterable](https://www.php.net/manual/zh/language.types.iterable.php)是 PHP 7.1 中引入的一个伪类型。它接受任何 array 或实现了 [Traversable](https://www.php.net/manual/zh/class.traversable.php) 接口的对象。这些类型都能用 [foreach](https://www.php.net/manual/zh/control-structures.foreach.php) 迭代， 也可以和 [生成器](https://www.php.net/manual/zh/language.generators.php) 里的 **yield from** 一起使用。



## 对象（Object）

使用new语句实例化一个类即可创建一个新的对象 



## 枚举（Enum）

定义包含可能值的封闭集合类型。



## 资源（Resource）

资源 resource 是一种特殊变量，保存了到外部资源的一个引用。



## NULL

特殊的 **`null`** 值表示一个变量没有值。

> - 被赋值为 **`null`**。
> - 尚未被赋值。
> - 被 [unset()](https://www.php.net/manual/zh/function.unset.php)。



## Callback与Callable

### 传递回调函数

> 不仅可以使用普通的用户自定义函数，也接受 [匿名函数](https://www.php.net/manual/zh/functions.anonymous.php) 和 [箭头函数](https://www.php.net/manual/zh/functions.arrow.php)。

**自定义函数**

```php
function add(int $num1, int $num2): int
{
    return $num1 + $num2;
}
call_user_func('add',1,2);  // 或者 call_user_func('add',...[1,2]);
```

**匿名函数**

```php
$add = function (int $num1, int $num2): int {
    return $num1 + $num2;
};
call_user_func($add, 1, 2);
```

**箭头函数**

```php
$add = fn(int $num1, int $num2) => $num1 + $num2;
call_user_func($add, 1, 2);
```

### 传递对象

下标 为 0 的位置传递object，下标 1 包含方法名。 

```php
class Person
{
    public static function eat()
    {
        echo 'eating';
    }
    public function program()
    {
        echo 'programing';
    }
}
$person = new Person();
call_user_func([$person, 'program']);
```

### 传递静态方法

下标为 0 的位置传递类名 ，或者传递 `'ClassName::methodName'`。

```php
class Person
{
    public static function eat()
    {
        echo 'eating';
    }
    public function program()
    {
        echo 'programing';
    }
}
call_user_func(['Person', 'eat']);  // 或者 call_user_func('Person::eat');
```



## 类型转化

- (int), (integer) - 转换为整形 int
- (bool), (boolean) - 转换为布尔类型 bool
- (float), (double), (real) - 转换为浮点型 float
- (string) - 转换为字符串 string
- (array) - 转换为数组 array
- (object) - 转换为对象 object
- (unset) - 转换为 NULL

