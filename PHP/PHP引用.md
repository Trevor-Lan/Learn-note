## 引用的解释

用不同的名字访问同一个变量内容



## 写时复制

当一个变量赋值给另一个变量的时，并不会立刻为另一个变量开辟内存空间，此时两个变量指向同一块内存空间，只有在其中的某一个变量的内容发生改变时才会开辟新的内存空间。

```php
<?php

$a = range(1,100);
$b = $a; // $a和$b指向同一块内存空间
$a = range(1,100); // 改变$a的内容，此时$a和$b指向不同的内存空间
```



## 引用传递

```php
function num(&$var)
{
    $var++;
}
$a = 1;
num($a);
echo $a;
```

```
输出：2
```



## 取消引用

```php
$a = 1;
$b =& $a;
unset($b);
```



## 对象为引用赋值

```php
<?php

$obj1 = new Stdclass();
$obj2 = $obj1;  // 对象赋值为引用赋值，所以$obj1和$obj2指向同一块内存地址

```



## 查看变量的使用情况

```php
<?php
    
$a = range(1, 2);
$b = &$a;
$c = $a;
xdebug_debug_zval('a');

```

```
a: (refcount=2, is_ref=1)=array (0 => (refcount=0, is_ref=0)=1, 1 => (refcount=0, is_ref=0)=2)
```

> 注：refcount为使用次数，is_ref为是否是是引用（0为否，1为是）



## 练习题

每次var_dump的data内容是什么？

```php
<?php
    
$data = ['a', 'b', 'c'];
foreach ($data as $k => $v) {
    $v =&$data[$k];
    var_dump($data);
}

```



