## PHP7中Error异常类

**PHP 错误处理**

当未设置错误处理函数时，PHP 会根据配置处理出现的错误。 php.ini 中 [`error_reporting`](https://www.php.net/manual/zh/errorfunc.configuration.php#ini.error-reporting) 的配置或者是运行时调用 [error_reporting()](https://www.php.net/manual/zh/function.error-reporting.php) 控制了哪些错误需要报告，哪些错误需要自动忽略。 由于有些错误会在运行用户脚本前就可能出现，所以强烈推荐用配置指令来设置。

在开发环境里为了发现并修复 PHP 产生的问题， 应该总是把 [`error_reporting`](https://www.php.net/manual/zh/errorfunc.configuration.php#ini.error-reporting) 设置为 **`E_ALL`**。 在生产环境里，用户可能为了降低信息的详细程度， 想要将它设置为类似 `E_ALL & ~E_NOTICE & ~E_DEPRECATED`， 但很多情况下 **`E_ALL`** 也同样适用，这样可以更早地警告潜在问题。

PHP 对这些错误的处理方式，取决于两个更深的 php.ini 指令。 [`display_errors`](https://www.php.net/manual/zh/errorfunc.configuration.php#ini.display-errors) 控制了是否要将错误作为脚本输出的一部分显示。 在生产环境里应该禁用，因为可能包含类似数据库密码这样的敏感信息， 而在开发环境中应该启用，能确保立即报告问题。

PHP 不仅能显示错误，还可以开启 [`log_errors`](https://www.php.net/manual/zh/errorfunc.configuration.php#ini.log-errors) 指令来记录错误日志。它能根据 [`error_log`](https://www.php.net/manual/zh/errorfunc.configuration.php#ini.error-log) 的设置，记录任意错误到文件或者 syslog。 特别适用于生产环境，用户可以记录发生的错误，并根据这些错误生成报告。

**用户的错误处理器**

如果 PHP 默认错误处理器还不能满足要求，用户可以通过 [set_error_handler()](https://www.php.net/manual/zh/function.set-error-handler.php) 设置自定义错误处理器，可处理很多类型的错误。 虽然有些类型的错误不能通过这种方式处理，但能处理的类型可以用脚本合适的方式处理： 例如为用户显示自定义错误页面，同时以一种比日志更直接的方式上报错误，例如发送邮件。

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