## PHP中Exception类

```php
class Exception implements Throwable
{
    protected $message;
    protected $code;
    protected $file;
    protected $line;

    final private function __clone() {}
    public function __construct($message = "", $code = 0, Throwable $previous = null) {}
    final public function getMessage() {}
    final public function getCode() {}
    final public function getFile() {}
    final public function getLine() {}
    final public function getTrace() {}
    final public function getPrevious() {}
    final public function getTraceAsString() {}
    public function __toString() {}
    public function __wakeup() {}
}
```

## 捕获异常

方式1

```php
try {
    // 代码块
} catch (Exception $e) {
    // 异常处理
}
```

方式2

```php
try {
    // 代码块
} catch (Throwable $e) {
    // 异常处理
}
```

以上两种方式都可以捕获和处理异常



## 自定义异常

```
set_exception_handler(callable $exception_handler): callable
```

```php
set_exception_handler(function ($exception) {
    // 异常处理;
});
```

