## PHP7中Error异常类

```php
class Error implements Throwable
{
    protected $message;
    protected $code;
    protected $file;
    protected $line;

    public function __construct($message = "", $code = 0, Throwable $previous = null) {}
    final public function getMessage() {}
    final public function getCode() {}
    final public function getFile() {}
    final public function getLine() {}
    final public function getTrace() {}
    final public function getTraceAsString() {}
    final public function getPrevious() {}
    public function __toString() {}
    final private function __clone() {}
    public function __wakeup() {}
}
```

## 捕获错误

方式1

```php
try {
    // 代码块
} catch (Error $e) {
    // 错误处理
}
```

方式2

```php
try {
    // 代码块
} catch (Throwable $e) {
    // 错误处理
}
```

以上两种方式都可以捕获和处理错误



## 自定义错误处理

> 注：如果尚未注册错误处理函数，则按照传统方式处理，有注册则先通过注册的错误处理函数

```
set_error_handler(?callable $callback, int $error_levels = E_ALL|E_STRICT)
```

```php
set_error_handler(function (int $number, string $message) {
    // 自定义错误处理
});
```



## 设置错误等级

```
error_reporting(int $level = ?): int
```

> ```
> E_ERROR
> E_WARNING
> E_PARSE
> E_NOTICE
> E_CORE_ERROR
> E_CORE_WARNING
> E_COMPILE_ERROR
> E_COMPILE_WARNING
> E_USER_ERROR
> E_USER_WARNING
> E_USER_NOTICE
> E_ALL
> E_STRICT
> E_RECOVERABLE_ERROR
> E_DEPRECATED
> E_USER_DEPRECATED
> ```