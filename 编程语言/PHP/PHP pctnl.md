## 常用

- [pcntl_fork](https://www.php.net/manual/zh/function.pcntl-fork.php) — 在当前进程当前位置产生分支（子进程）。译注：fork是创建了一个子进程，父进程和子进程 都从fork的位置开始向下继续执行，不同的是父进程执行过程中，得到的fork返回值为子进程 号，而子进程得到的是0。

- [pcntl_alarm](https://www.php.net/manual/zh/function.pcntl-alarm.php) — 为进程设置一个alarm闹钟信号

- [pcntl_setpriority](https://www.php.net/manual/zh/function.pcntl-setpriority.php) — 修改任意进程的优先级

- [pcntl_signal](https://www.php.net/manual/zh/function.pcntl-signal.php) — 安装一个信号处理器

- [pcntl_wait](https://www.php.net/manual/zh/function.pcntl-wait.php) — 等待或返回 fork 的子进程状态

  

## 其他

- [pcntl_async_signals](https://www.php.net/manual/zh/function.pcntl-async-signals.php) — Enable/disable asynchronous signal handling or return the old setting
- [pcntl_errno](https://www.php.net/manual/zh/function.pcntl-errno.php) — 别名 pcntl_get_last_error
- [pcntl_exec](https://www.php.net/manual/zh/function.pcntl-exec.php) — 在当前进程空间执行指定程序
- [pcntl_waitpid](https://www.php.net/manual/zh/function.pcntl-waitpid.php) — 等待或返回fork的子进程状态
- [pcntl_wexitstatus](https://www.php.net/manual/zh/function.pcntl-wexitstatus.php) — 返回一个中断的子进程的返回代码
- [pcntl_wifexited](https://www.php.net/manual/zh/function.pcntl-wifexited.php) — 检查状态代码是否代表一个正常的退出。
- [pcntl_wifsignaled](https://www.php.net/manual/zh/function.pcntl-wifsignaled.php) — 检查子进程状态码是否代表由于某个信号而中断
- [pcntl_wifstopped](https://www.php.net/manual/zh/function.pcntl-wifstopped.php) — 检查子进程当前是否已经停止
- [pcntl_wstopsig](https://www.php.net/manual/zh/function.pcntl-wstopsig.php) — 返回导致子进程停止的信号
- [pcntl_wtermsig](https://www.php.net/manual/zh/function.pcntl-wtermsig.php) — 返回导致子进程中断的信号
- [pcntl_sigprocmask](https://www.php.net/manual/zh/function.pcntl-sigprocmask.php) — 设置或检索阻塞信号
- [pcntl_sigtimedwait](https://www.php.net/manual/zh/function.pcntl-sigtimedwait.php) — 带超时机制的信号等待
- [pcntl_sigwaitinfo](https://www.php.net/manual/zh/function.pcntl-sigwaitinfo.php) — 等待信号
- [pcntl_strerror](https://www.php.net/manual/zh/function.pcntl-strerror.php) — Retrieve the system error message associated with the given errno
- [pcntl_signal_dispatch](https://www.php.net/manual/zh/function.pcntl-signal-dispatch.php) — 调用等待信号的处理器
- [pcntl_signal_get_handler](https://www.php.net/manual/zh/function.pcntl-signal-get-handler.php) — Get the current handler for specified signal
- [pcntl_get_last_error](https://www.php.net/manual/zh/function.pcntl-get-last-error.php) — Retrieve the error number set by the last pcntl function which failed
- [pcntl_getpriority](https://www.php.net/manual/zh/function.pcntl-getpriority.php) — 获取任意进程的优先级