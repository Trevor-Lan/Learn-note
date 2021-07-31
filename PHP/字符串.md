### 1 单引号与双引号的区别

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



### 2 heredoc与nowdoc

**heredoc**

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

**nowdoc**

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



### 3 字符串的简易操作

**3.1 字符串长度**
int  strlen（string $str）返回字符串长度。

```php
<?php
$str="PHP";
$len=strlen($str);
echo $len;
?>
```

**3.2 字符串查找**

```
int  stripos（string $haystack,string $needle[,int $offset=0]）返回字符串中部分字符串首次出现的位置（不区分大小写）。
```

> **haystack**
> 在该字符串中查找。
>
> **needle**
> 注意 needle 可以是一个单字符或者多字符的字符串。
>
> 如果 needle 不是一个字符串，那么它将被转换为整型并被视为字符顺序值。
>
> **offset**
> 可选的 offset 参数，从字符此数量的开始位置进行搜索。 如果是负数，就从字符末尾此数量的字符数开始统计。

```
int strpos（string $haystack,string $needle[,int $offset=0]）返回字符串中部分字符串首次出现的位置（区分大小写）。
```

> haystack
> 在该字符串中进行查找。
>
> needle
> 如果 needle 不是一个字符串，那么它将被转换为整型并被视为字符的顺序值。
>
> offset
> 如果提供了此参数，搜索会从字符串该字符数的起始位置开始统计。 如果是负数，搜索会从字符串结尾指定字符数开始。

```
int strrpos（string $haystack,string $needle[,int $offset=0]）返回字符串中部分字符串最后出现的位置（区分大小写）。
```

> haystack
> 在此字符串中进行查找。
>
> needle
> 如果 needle不是一个字符串，它将被转换为整型并被视为字符的顺序值。
>
> offset
> 或许会查找字符串中任意长度的子字符串。负数值将导致查找在字符串结尾处开始的计数位置处结束。

```
int strripos（string $haystack,string $needle[,int $offset=0]）返回字符串中部分字符串最后出现的位置（不区分大小写）。
```

> haystack
> 在此字符串中进行查找。
>
> needle
> 注意 needle 可以是一个单字符或者多字符的字符串。
>
> offset
> 参数 offset 可以被指定来查找字符串中任意长度的子字符串。
>
> 负数偏移量将使得查找从字符串的起始位置开始，到 offset 位置为止。

**3.3 字符串替换**

```
mixed str_replace ( mixed $search , mixed $replace , mixed $subject [, int &$count ] )
```

该函数返回一个字符串或者数组。该字符串或数组是将 subject 中全部的 search 都被 replace 替换之后的结果。

```php
<?php
$arr = array("A","B","C","E");
print_r(str_replace("E","D",$arr,$i));
echo "被替换的次数为: $i";
```

```
mixed str_ireplace ( mixed $search , mixed $replace , mixed $subject [, int &$count ] )
```

该函数返回一个字符串或者数组。该字符串或数组是将 subject 中全部的 search 都被 replace 替换（忽略大小写）之后的结果。

```
mixed preg_replace ( mixed $pattern , mixed $replacement , mixed $subject [, int $limit = -1 [, int &$count ]] )
```

> **pattern**
> 要搜索的模式。可以使一个字符串或字符串数组。
>
> 可以使用一些PCRE修饰符。
>
> **replacement**
> 用于替换的字符串或字符串数组。如果这个参数是一个字符串，并且pattern 是一个数组，那么所有的模式都使用这个字符串进行替换。如果pattern和replacement 都是数组，每个pattern使用replacement中对应的 元素进行替换。如果replacement中的元素比pattern中的少， 多出来的pattern使用空字符串进行替换。
>
> replacement中可以包含后向引用\\n 或$n，语法上首选后者。 每个 这样的引用将被匹配到的第n个捕获子组捕获到的文本替换。 n 可以是0-99，\\0和$0代表完整的模式匹配文本。 捕获子组的序号计数方式为：代表捕获子组的左括号从左到右， 从1开始数。如果要在replacement 中使用反斜线，必须使用4个("\\\\"，译注：因为这首先是php的字符串，经过转义后，是两个，再经过 正则表达式引擎后才被认为是一个原文反斜线)。
>
> 当在替换模式下工作并且后向引用后面紧跟着需要是另外一个数字(比如：在一个匹配模式后紧接着增加一个原文数字)， 不能使用\\1这样的语法来描述后向引用。比如， \\11将会使preg_replace() 不能理解你希望的是一个\\1后向引用紧跟一个原文1，还是 一个\\11后向引用后面不跟任何东西。 这种情况下解决方案是使用${1}1。 这创建了一个独立的$1后向引用, 一个独立的原文1。
>
> 当使用被弃用的 e 修饰符时, 这个函数会转义一些字符(即：'、"、 \ 和 NULL) 然后进行后向引用替换。当这些完成后请确保后向引用解析完后没有单引号或 双引号引起的语法错误(比如： 'strlen(\'$1\')+strlen("$2")')。确保符合PHP的 字符串语法，并且符合eval语法。因为在完成替换后， 引擎会将结果字符串作为php代码使用eval方式进行评估并将返回值作为最终参与替换的字符串。
>
> subject
> 要进行搜索和替换的字符串或字符串数组。
>
> 如果subject是一个数组，搜索和替换回在subject 的每一个元素上进行, 并且返回值也会是一个数组。
>
> **limit**
> 每个模式在每个subject上进行替换的最大次数。默认是 -1(无限)。
>
> **count**
> 如果指定，将会被填充为完成的替换次数。

**3.4 字符串截取**

```
string substr ( string $string , int $start [, int $length ] )
```

> string
> 输入字符串。必须至少有一个字符。
>
> start
> 如果 start 是非负数，返回的字符串将从 string 的 start 位置开始，从 0 开始计算。例如，在字符串 “abcdef” 中，在位置 0 的字符是 “a”，位置 2 的字符串是 “c” 等等。
>
> 如果 start 是负数，返回的字符串将从 string 结尾处向前数第 start 个字符开始。
>
> 如果 string 的长度小于 start，将返回 FALSE。

**3.5 字符串转义**

```
string addslashes ( string $str )
```

返回字符串，该字符串为了数据库查询语句等的需要在某些字符前加上了反斜线。
这些字符是单引号（'）、双引号（"）、反斜线（\）与 NUL（NULL 字符）。

字符串分割

```
explode(separator,string,limit)
```

> separator	必需。规定在哪里分割字符串。
> string	必需。要分割的字符串。
> limit	可选。规定所返回的数组元素的数目。

可能的值：

> 大于 0 - 返回包含最多 limit 个元素的数组
> 小于 0 - 返回包含除了最后的 -limit 个元素以外的所有元素的数组
> 0 - 返回包含一个元素的数组

**3.6 改变字符串大小写**

```
string ucfirst ( string $str )
```

> 将 str 的首字符（如果首字符是字母）转换为大写字母，并返回这个字符串。

```
string lcfirst ( string $str )
```

> 返回第一个字母小写的 str 

```
string ucwords ( string $str [, string $delimiters = " \t\r\n\f\v" ] )
```

> 将 str 中每个单词的首字符（如果首字符是字母）转换为大写字母，并返回这个字符串。
>
> 这里单词的定义是紧跟在 delimiters 参数（默认：空格符、制表符、换行符、回车符、水平线以及竖线）之后的子字符串。

```
string strtoupper ( string $string )
```

> 将 string 中所有的字母字符转换为大写并返回。

```
string strtolower ( string $string )
```

> 将 string 中所有的字母字符转换为小写并返回。

**3.7 字符串去首尾空格和特殊字符**

```
string trim ( string $str [, string $character_mask = " \t\n\r\0\x0B" ] )
```

> str
> 待处理的字符串。
>
> character_mask
> 可选参数，过滤字符也可由 character_mask 参数指定。一般要列出所有希望过滤的字符，也可以使用 “..” 列出一个字符范围。

### 4 其它常用字符串函数

> str_repeat ()  重复一个字符串
> is_string() 检测变量是否是字符串；
> str_shuffle () 随机打乱一个字符串
> sprintf()  返回根据格式化字符串生成的字符串（通常用于获取分表后的数据表名）
> strstr()  查找字符串的首次出现