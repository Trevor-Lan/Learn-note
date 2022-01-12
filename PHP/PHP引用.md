## 引用的解释

用不同的名字访问同一个变量内容



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



