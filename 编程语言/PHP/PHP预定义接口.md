[Traversable](https://www.php.net/manual/zh/class.traversable.php)



[Iterator](https://www.php.net/manual/zh/class.iterator.php)



[IteratorAggregate](https://www.php.net/manual/zh/class.iteratoraggregate.php)



[Throwable](https://www.php.net/manual/zh/class.throwable.php)



[ArrayAccess](https://www.php.net/manual/zh/class.arrayaccess.php)



[Serializable](https://www.php.net/manual/zh/class.serializable.php)



[Closure](https://www.php.net/manual/zh/class.closure.php)

用于代表 [匿名函数](https://www.php.net/manual/zh/functions.anonymous.php) 的类.匿名函数会产生这种类型的对象。这个类带有一些方法允许在匿名函数创建后对其进行更多的控制。除了此处列出的方法，还有一个 `__invoke` 方法。这是为了与其他实现了 [__invoke()魔术方法](https://www.php.net/manual/zh/language.oop5.magic.php#language.oop5.magic.invoke) 的对象保持一致性，但调用匿名函数的过程与它无关。



[Generator](https://www.php.net/manual/zh/class.generator.php)

```php
function fib($n)
{
    $cur = 1;
    $prev = 0;
    for ($i = 0; $i < $n; $i++) {
        yield $cur;

        $temp = $cur;
        $cur = $prev + $cur;
        $prev = $temp;
    }
}

$fibs = fib(9);
foreach ($fibs as $fib) {
    echo " " . $fib;
}
```

[WeakReference](https://www.php.net/manual/zh/class.weakreference.php)



[Stringable](https://www.php.net/manual/zh/class.stringable.php)



[WeakMap](https://www.php.net/manual/zh/class.weakmap.php)



[UnitEnum](https://www.php.net/manual/zh/class.unitenum.php)



[BackedEnum](https://www.php.net/manual/zh/class.backedenum.php)



[Fiber](https://www.php.net/manual/zh/class.fiber.php)

