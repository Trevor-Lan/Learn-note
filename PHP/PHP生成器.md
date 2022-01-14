生成器提供了一种更容易的方法来实现简单的[对象迭代](https://www.php.net/manual/zh/language.oop5.iterations.php)，相比较定义类实现 [Iterator](https://www.php.net/manual/zh/class.iterator.php) 接口的方式，性能开销和复杂性大大降低。

生成器允许你在 [foreach](https://www.php.net/manual/zh/control-structures.foreach.php) 代码块中写代码来迭代一组数据而不需要在内存中创建一个数组, 那会使你的内存达到上限，或者会占据可观的处理时间。相反，你可以写一个生成器函数，就像一个普通的自定义[函数](https://www.php.net/manual/zh/functions.user-defined.php)一样, 和普通函数只[返回](https://www.php.net/manual/zh/functions.returning-values.php)一次不同的是, 生成器可以根据需要 [yield](https://www.php.net/manual/zh/language.generators.syntax.php#control-structures.yield) 多次，以便生成需要迭代的值。



生成器函数的核心是**yield**关键字。它最简单的调用形式看起来像一个return申明，不同之处在于普通return会返回值并终止函数的执行，而yield会返回一个值给循环调用此生成器的代码并且只是暂停执行生成器函数。



生成器最主要的优点是简洁。和实现一个 [Iterator](https://www.php.net/manual/zh/class.iterator.php) 类相较而言， 同样的功能，用生成器可以编写更少的代码，可读性也更强。 

生成器是一个只能向前的迭代器，一旦开始遍历就无法后退。 意思也就是说，同样的生成器无法遍历多遍：要么再次调用生成器函数，重新生成后再遍历。

