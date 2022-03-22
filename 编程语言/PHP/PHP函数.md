## 内置函数

- [get_loaded_extensions()](https://www.php.net/manual/zh/function.get-loaded-extensions.php) 
- [function_exists()](https://www.php.net/manual/zh/function.function-exists.php)
- [get_extension_funcs()](https://www.php.net/manual/zh/function.get-extension-funcs.php)
- [函数参考](https://www.php.net/manual/zh/funcref.php)



## 自定义函数

```php
function foo($arg_1, $arg_2, /* ..., */ $arg_n)
{
    // 代码逻辑;
    return true;
}
```



## 可变函数

PHP 支持可变函数的概念。这意味着如果一个变量名后有圆括号，PHP 将寻找与变量的值同名的函数，并且尝试执行它。可变函数可以用来实现包括回调函数，函数表在内的一些用途。

```php
<?php
    
function demo() {
    echo "demo";
}

$func = 'demo';
$func();        // 调用 demo()

```



## 匿名函数

匿名函数（Anonymous functions），也叫闭包函数（`closures`），允许 临时创建一个没有指定名称的函数。最经常用作回调函数 [callable](https://www.php.net/manual/zh/language.types.callable.php)参数的值。当然，也有其它应用的情况。

匿名函数目前是通过 [Closure](https://www.php.net/manual/zh/class.closure.php) 类来实现的。

```php
<?php


$hello = function($name)
{
    echo "hello {$name}";
};

$hello('Trevor');

```



## 箭头函数

箭头函数是 PHP 7.4 的新语法，是一种更简洁的 [匿名函数](https://www.php.net/manual/zh/functions.anonymous.php) 写法。匿名函数和箭头函数都是 [Closure](https://www.php.net/manual/zh/class.closure.php) 类的实现。箭头函数的基本语法为 

`fn (argument_list) => expr`。箭头函数支持与 [匿名函数](https://www.php.net/manual/zh/functions.anonymous.php) 相同的功能，只是其父作用域的变量总是自动的。当表达式中使用的变量是在父作用域中定义的，它将被隐式地按值捕获。

```php
<?php

$y = 1;

$fn1 = fn($x) => $x + $y;

// 相当于通过 value 使用 $y：
$fn2 = function ($x) use ($y) {
    return $x + $y;
};

var_export($fn1(3));
```



## 递归

符合一点条件下，自己调用自己

```php
<?php


function add($i, $n, $count = 0)
{
    if ($i <= $n) {
        $count += $i;
        $i++;
        $c = add($i, $n, $count);
    }
    return $count;
}

var_dump(add(1, 10));
```



## 迭代

根据变量的原值推算出变量的一个新值

```php
<?php
    
function iteration($n)
{
    for ($i = 0, $j = 0; $i < $n; $i++) {
        $j = $j + $i;
    }
    return $j;
}

var_dump(iteration(10));

```

