## 布尔（Boolean）

布尔表达真假值，可以为 **`true`** 或 **`false`**（不区分大小写）

**注：以下情况的布尔值都为false**

> 布尔值为false
> 整型值 0
> 浮点型值 0.0或-0.0
> 空字符串或字符串 "0"
> 空数组
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

 可以接受用户自定义的回调函数作为参数。回调函数不止可以是简单函数，还可以是对象的方法，包括静态类方法。

> call_user_func(callable $callback, mixed ...$args): mixed



## 类型转化

- (int), (integer) - 转换为整形 int
- (bool), (boolean) - 转换为布尔类型 bool
- (float), (double), (real) - 转换为浮点型 float
- (string) - 转换为字符串 string
- (array) - 转换为数组 array
- (object) - 转换为对象 object
- (unset) - 转换为 NULL