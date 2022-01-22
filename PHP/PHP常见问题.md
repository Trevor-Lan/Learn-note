## include与require的区别

**include**

使用include引用文件时，如果文件不存在会抛出一个warning错误，不会终止程序执行

**include_once**

与include的用法一样，不过只会引用一次

**require**

使用require引用文件时，如果文件不存在会抛出一个fatal错误，终止程序执行

**require_once**

与require的用法一样，不过只会引用一次



## 哪些值为false 

- [布尔](https://www.php.net/manual/zh/language.types.boolean.php)值 false 本身
- [整型](https://www.php.net/manual/zh/language.types.integer.php)值 0（零）
- [浮点型](https://www.php.net/manual/zh/language.types.float.php)值 0.0（零）-0.0(零)
- 空[字符串](https://www.php.net/manual/zh/language.types.string.php)，以及[字符串](https://www.php.net/manual/zh/language.types.string.php) "0"
- 不包括任何元素的[数组](https://www.php.net/manual/zh/language.types.array.php)
- 特殊类型 [NULL](https://www.php.net/manual/zh/language.types.null.php)（包括尚未赋值的变量）
- 由无属性的空元素创建 [SimpleXML](https://www.php.net/manual/zh/ref.simplexml.php) 对象

> 注：字符串'false'，转化bool是为true
>
> ```
> var_dump((bool) "false");   // bool(true)
> ```



## 字符串的表达形式

**单引号与双引号的区别**

单引号：不能识别字符串中插入的变量，需要转义的特殊字符只有反斜杠和单引号本身。

双引号：可以解析字符串中的变量，需要转义的特殊字符有

双引号中需要转义的特殊字符

```
\n	换行
\r	回车
\t	制表
\\	反斜杠
\$	美元符
\"	双引号
```

**heredoc与nowdoc**

heredoc

作用和双引号一样，可以解析变量，特殊字符同样需要用反斜杠进行转义。

语法规则：

```
<<<标志符

 文本信息

标志符;
```

> 注：标志符可以用双引号括起来，结束标志符不能有空格。

例如：以下程序输出hello  PHP。

```php
<?php
$learn="PHP";
$str=<<<FOF
 hello $learn
FOF;
echo $str;
?>
```

nowdoc

作用和单引号一样，不可以解析变量，特殊字符同样需要用反斜杠进行转义。

语法规则：

```
<<<'标志符'

 文本信息

标志符;
```

> 注：标志符可以用双引号括起来，结束标志符不能有空格。

例如：以下程序输出hello $learn。

```php
<?php
$learn="PHP";
$str=<<<'FOF'
 hello $learn
FOF;
echo $str;
?>
```

