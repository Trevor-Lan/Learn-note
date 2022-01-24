## 字符串的定义方式

**单引号**

1. 不能解析变量
2. 不能解析转义字符，只能解析单引号和反斜线本身
3. 变量或字符串可以使用 . 连接

**双引号**

1. 可以解析变量
2. 可以解析所有转义字符
3. 变量或字符串可以使用 . 连接

**newdoc和heredoc**

1. newdoc类似单引号

```php
<?php
    
$a = <<<'EOF'
hello world
EOF;

```

2. heredoc类似双引号

```php
<?php
    
$a = <<<EOF
hello world
EOF;

```

3. 常用于处理大文本

> 注：因为单引号不解析变量，所以单引号的解析效率要高于双引号



## 常用

- [addcslashes](https://www.php.net/manual/zh/function.addcslashes.php) — 以 C 语言风格使用反斜线转义字符串中的字符
- [addslashes](https://www.php.net/manual/zh/function.addslashes.php) — 使用反斜线引用字符串
- [echo](https://www.php.net/manual/zh/function.echo.php) — 输出一个或多个字符串
- [explode](https://www.php.net/manual/zh/function.explode.php) — 使用一个字符串分割另一个字符串
- [htmlspecialchars_decode](https://www.php.net/manual/zh/function.htmlspecialchars-decode.php) — 将特殊的 HTML 实体转换回普通字符
- [htmlspecialchars](https://www.php.net/manual/zh/function.htmlspecialchars.php) — 将特殊字符转换为 HTML 实体
- [implode](https://www.php.net/manual/zh/function.implode.php) — 将一个一维数组的值转化为字符串
- [lcfirst](https://www.php.net/manual/zh/function.lcfirst.php) — 使一个字符串的第一个字符小写
- [ltrim](https://www.php.net/manual/zh/function.ltrim.php) — 删除字符串开头的空白字符（或其他字符）
- [md5_file](https://www.php.net/manual/zh/function.md5-file.php) — 计算指定文件的 MD5 散列值
- [md5](https://www.php.net/manual/zh/function.md5.php) — 计算字符串的 MD5 散列值
- [parse_str](https://www.php.net/manual/zh/function.parse-str.php) — 将字符串解析成多个变量
- [print](https://www.php.net/manual/zh/function.print.php) — 输出字符串
- [printf](https://www.php.net/manual/zh/function.printf.php) — 输出格式化字符串
- [sha1_file](https://www.php.net/manual/zh/function.sha1-file.php) — 计算文件的 sha1 散列值
- [sha1](https://www.php.net/manual/zh/function.sha1.php) — 计算字符串的 sha1 散列值
- [sprintf](https://www.php.net/manual/zh/function.sprintf.php) — 返回格式化字符串
- [str_repeat](https://www.php.net/manual/zh/function.str-repeat.php) — 重复一个字符串
- [str_replace](https://www.php.net/manual/zh/function.str-replace.php) — 子字符串替换
- [str_shuffle](https://www.php.net/manual/zh/function.str-shuffle.php) — 随机打乱一个字符串
- [str_split](https://www.php.net/manual/zh/function.str-split.php) — 将字符串转换为数组
- [strcmp](https://www.php.net/manual/zh/function.strcmp.php) — 二进制安全字符串比较
- [stripos](https://www.php.net/manual/zh/function.stripos.php) — 查找字符串首次出现的位置（不区分大小写）
- [strlen](https://www.php.net/manual/zh/function.strlen.php) — 获取字符串长度
- [strpos](https://www.php.net/manual/zh/function.strpos.php) — 查找字符串首次出现的位置
- [strrchr](https://www.php.net/manual/zh/function.strrchr.php) — 查找指定字符在字符串中的最后一次出现
- [strrev](https://www.php.net/manual/zh/function.strrev.php) — 反转字符串
- [strstr](https://www.php.net/manual/zh/function.strstr.php) — 查找字符串的首次出现
- [strtok](https://www.php.net/manual/zh/function.strtok.php) — 标记分割字符串
- [strtolower](https://www.php.net/manual/zh/function.strtolower.php) — 将字符串转化为小写
- [strtoupper](https://www.php.net/manual/zh/function.strtoupper.php) — 将字符串转化为大写
- [strtr](https://www.php.net/manual/zh/function.strtr.php) — 转换指定字符
- [substr_compare](https://www.php.net/manual/zh/function.substr-compare.php) — 二进制安全比较字符串（从偏移位置比较指定长度）
- [substr_count](https://www.php.net/manual/zh/function.substr-count.php) — 计算字串出现的次数
- [substr_replace](https://www.php.net/manual/zh/function.substr-replace.php) — 替换字符串的子串
- [substr](https://www.php.net/manual/zh/function.substr.php) — 返回字符串的子串
- [trim](https://www.php.net/manual/zh/function.trim.php) — 去除字符串首尾处的空白字符（或者其他字符）
- [ucfirst](https://www.php.net/manual/zh/function.ucfirst.php) — 将字符串的首字母转换为大写
- [ucwords](https://www.php.net/manual/zh/function.ucwords.php) — 将字符串中每个单词的首字母转换为大写



## 其它

- [bin2hex](https://www.php.net/manual/zh/function.bin2hex.php) — 函数把包含数据的二进制字符串转换为十六进制值
- [chop](https://www.php.net/manual/zh/function.chop.php) — rtrim 的别名
- [chr](https://www.php.net/manual/zh/function.chr.php) — 返回指定的字符
- [chunk_split](https://www.php.net/manual/zh/function.chunk-split.php) — 将字符串分割成小块
- [convert_cyr_string](https://www.php.net/manual/zh/function.convert-cyr-string.php) — 将字符由一种 Cyrillic 字符转换成另一种
- [convert_uudecode](https://www.php.net/manual/zh/function.convert-uudecode.php) — 解码一个 uuencode 编码的字符串
- [convert_uuencode](https://www.php.net/manual/zh/function.convert-uuencode.php) — 使用 uuencode 编码一个字符串
- [count_chars](https://www.php.net/manual/zh/function.count-chars.php) — 返回字符串所用字符的信息
- [crc32](https://www.php.net/manual/zh/function.crc32.php) — 计算一个字符串的 crc32 多项式
- [crypt](https://www.php.net/manual/zh/function.crypt.php) — 单向字符串散列
- [fprintf](https://www.php.net/manual/zh/function.fprintf.php) — 将格式化后的字符串写入到流
- [get_html_translation_table](https://www.php.net/manual/zh/function.get-html-translation-table.php) — 返回使用 htmlspecialchars 和 htmlentities 后的转换表
- [hebrev](https://www.php.net/manual/zh/function.hebrev.php) — 将逻辑顺序希伯来文（logical-Hebrew）转换为视觉顺序希伯来文（visual-Hebrew）
- [hebrevc](https://www.php.net/manual/zh/function.hebrevc.php) — 将逻辑顺序希伯来文（logical-Hebrew）转换为视觉顺序希伯来文（visual-Hebrew），并且转换换行符
- [hex2bin](https://www.php.net/manual/zh/function.hex2bin.php) — 转换十六进制字符串为二进制字符串
- [html_entity_decode](https://www.php.net/manual/zh/function.html-entity-decode.php) — Convert HTML entities to their corresponding characters
- [htmlentities](https://www.php.net/manual/zh/function.htmlentities.php) — 将字符转换为 HTML 转义字符
- [join](https://www.php.net/manual/zh/function.join.php) — 别名 implode
- [levenshtein](https://www.php.net/manual/zh/function.levenshtein.php) — 计算两个字符串之间的编辑距离
- [localeconv](https://www.php.net/manual/zh/function.localeconv.php) — Get numeric formatting information
- [metaphone](https://www.php.net/manual/zh/function.metaphone.php) — Calculate the metaphone key of a string
- [money_format](https://www.php.net/manual/zh/function.money-format.php) — 将数字格式化成货币字符串
- [nl_langinfo](https://www.php.net/manual/zh/function.nl-langinfo.php) — Query language and locale information
- [nl2br](https://www.php.net/manual/zh/function.nl2br.php) — 在字符串所有新行之前插入 HTML 换行标记
- [number_format](https://www.php.net/manual/zh/function.number-format.php) — 以千位分隔符方式格式化一个数字
- [ord](https://www.php.net/manual/zh/function.ord.php) — 转换字符串第一个字节为 0-255 之间的值
- [quoted_printable_decode](https://www.php.net/manual/zh/function.quoted-printable-decode.php) — 将 quoted-printable 字符串转换为 8-bit 字符串
- [quoted_printable_encode](https://www.php.net/manual/zh/function.quoted-printable-encode.php) — 将 8-bit 字符串转换成 quoted-printable 字符串
- [quotemeta](https://www.php.net/manual/zh/function.quotemeta.php) — 转义元字符集
- [rtrim](https://www.php.net/manual/zh/function.rtrim.php) — 删除字符串末端的空白字符（或者其他字符）
- [setlocale](https://www.php.net/manual/zh/function.setlocale.php) — 设置地区信息
- [similar_text](https://www.php.net/manual/zh/function.similar-text.php) — 计算两个字符串的相似度
- [soundex](https://www.php.net/manual/zh/function.soundex.php) — Calculate the soundex key of a string
- [sscanf](https://www.php.net/manual/zh/function.sscanf.php) — 根据指定格式解析输入的字符
- [str_contains](https://www.php.net/manual/zh/function.str-contains.php) — Determine if a string contains a given substring
- [str_ends_with](https://www.php.net/manual/zh/function.str-ends-with.php) — Checks if a string ends with a given substring
- [str_getcsv](https://www.php.net/manual/zh/function.str-getcsv.php) — 解析 CSV 字符串为一个数组
- [str_ireplace](https://www.php.net/manual/zh/function.str-ireplace.php) — str_replace 的忽略大小写版本
- [str_pad](https://www.php.net/manual/zh/function.str-pad.php) — 使用另一个字符串填充字符串为指定长度
- [str_rot13](https://www.php.net/manual/zh/function.str-rot13.php) — 对字符串执行 ROT13 转换
- [str_starts_with](https://www.php.net/manual/zh/function.str-starts-with.php) — Checks if a string starts with a given substring
- [str_word_count](https://www.php.net/manual/zh/function.str-word-count.php) — 返回字符串中单词的使用情况
- [strcasecmp](https://www.php.net/manual/zh/function.strcasecmp.php) — 二进制安全比较字符串（不区分大小写）
- [strchr](https://www.php.net/manual/zh/function.strchr.php) — 别名 strstr
- [strcoll](https://www.php.net/manual/zh/function.strcoll.php) — 基于区域设置的字符串比较
- [strcspn](https://www.php.net/manual/zh/function.strcspn.php) — 获取不匹配遮罩的起始子字符串的长度
- [strip_tags](https://www.php.net/manual/zh/function.strip-tags.php) — 从字符串中去除 HTML 和 PHP 标记
- [stripcslashes](https://www.php.net/manual/zh/function.stripcslashes.php) — 反引用一个使用 addcslashes 转义的字符串
- [stripslashes](https://www.php.net/manual/zh/function.stripslashes.php) — 反引用一个引用字符串
- [stristr](https://www.php.net/manual/zh/function.stristr.php) — strstr 函数的忽略大小写版本
- [strnatcasecmp](https://www.php.net/manual/zh/function.strnatcasecmp.php) — 使用“自然顺序”算法比较字符串（不区分大小写）
- [strnatcmp](https://www.php.net/manual/zh/function.strnatcmp.php) — 使用自然排序算法比较字符串
- [strncasecmp](https://www.php.net/manual/zh/function.strncasecmp.php) — 二进制安全比较字符串开头的若干个字符（不区分大小写）
- [strncmp](https://www.php.net/manual/zh/function.strncmp.php) — 二进制安全比较字符串开头的若干个字符
- [strpbrk](https://www.php.net/manual/zh/function.strpbrk.php) — 在字符串中查找一组字符的任何一个字符
- [strripos](https://www.php.net/manual/zh/function.strripos.php) — 计算指定字符串在目标字符串中最后一次出现的位置（不区分大小写）
- [strrpos](https://www.php.net/manual/zh/function.strrpos.php) — 计算指定字符串在目标字符串中最后一次出现的位置
- [strspn](https://www.php.net/manual/zh/function.strspn.php) — 计算字符串中全部字符都存在于指定字符集合中的第一段子串的长度。
- [vfprintf](https://www.php.net/manual/zh/function.vfprintf.php) — 将格式化字符串写入流
- [vprintf](https://www.php.net/manual/zh/function.vprintf.php) — 输出格式化字符串
- [vsprintf](https://www.php.net/manual/zh/function.vsprintf.php) — 返回格式化字符串
- [wordwrap](https://www.php.net/manual/zh/function.wordwrap.php) — 打断字符串为指定数量的字串