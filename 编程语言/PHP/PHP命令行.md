## 命令行变量

- [$argc](https://www.php.net/manual/zh/reserved.variables.argc.php) — 传递给脚本的参数数目
- [$argv](https://www.php.net/manual/zh/reserved.variables.argv.php) — 传递给脚本的参数数组



## 常用

 读取一行

```php
readline(string $prompt = ?): string
```

添加一行命令行历史记录

```php
readline_add_history(string $line): bool
```

获取/设置readline内部的各个变量

```php
readline_info(string $varname = ?, string $newvalue = ?): mixed
```

获取命令历史列表

```php
readline_list_history(): array
```

清除历史

```php
readline_clear_history(): bool
```

案例

```php
<?php
    
echo "请输入姓名：";
$name = readline();
readline_add_history($name);

echo "请输入年龄：";
$age = readline();
readline_add_history($age);

echo $name . ':' . $age . "\n";

echo "readline_info：\n";
var_dump(readline_info());

echo "before readline_clear_history：\n";
var_dump(readline_list_history());

readline_clear_history();
echo "after readline_clear_history：\n";
var_dump(readline_list_history());

```

```
root@b3f17363b6ff:/data# php test.php 
请输入姓名：trevor
请输入年龄：25
trevor:25      
readline_info：
array(13) {    
  ["line_buffer"]=>
  string(2) "25"
  ["point"]=>
  int(2)
  ["end"]=>
  int(2)
  ["mark"]=>
  int(0)
  ["done"]=>
  int(1)
  ["pending_input"]=>
  int(0)
  ["prompt"]=>
  string(0) ""
  ["terminal_name"]=>
  string(5) "xterm"
  ["completion_append_character"]=>
  string(1) " "
  ["completion_suppress_append"]=> 
  bool(false)
  ["library_version"]=>
  string(3) "8.1"
  ["readline_name"]=>
  string(5) "other"
  ["attempted_completion_over"]=>  
  int(0)
}
before readline_clear_history：    
array(2) {
  [0]=>
  string(6) "trevor"
  [1]=>
  string(2) "25"
}
after readline_clear_history：     
array(0) {
}
```

## 其它

- [readline_callback_handler_install](https://www.php.net/manual/zh/function.readline-callback-handler-install.php) — 初始化一个 readline 回调接口，然后终端输出提示信息并立即返回
- [readline_callback_handler_remove](https://www.php.net/manual/zh/function.readline-callback-handler-remove.php) — 移除上一个安装的回调函数句柄并且恢复终端设置
- [readline_callback_read_char](https://www.php.net/manual/zh/function.readline-callback-read-char.php) — 当一个行被接收时读取一个字符并且通知 readline 调用回调函数
- [readline_completion_function](https://www.php.net/manual/zh/function.readline-completion-function.php) — 注册一个完成函数
- [readline_on_new_line](https://www.php.net/manual/zh/function.readline-on-new-line.php) — 通知readline将光标移动到新行
- [readline_read_history](https://www.php.net/manual/zh/function.readline-read-history.php) — 读取命令历史
- [readline_redisplay](https://www.php.net/manual/zh/function.readline-redisplay.php) — 重绘显示区
- [readline_write_history](https://www.php.net/manual/zh/function.readline-write-history.php) — 写入历史记录