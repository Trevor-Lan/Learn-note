官网配置：https://www.php.net/manual/zh/ini.php

配置文件

```php
<?php
echo phpinfo()
```

![image-20210727103632485](https://cdn.coder369.com/img/blog/image-20210727103632485.png)

日志配置

```
1. error_reporting  =  E_ALL                   #将会向PHP报告发生的每个错误   
2. display_errors = Off                        #不显示满足上条 指令所定义规则的所有错误报告   
3. log_errors = On                             #决定日志语句记录的位置   
4. log_errors_max_len = 1024                   #设置每个日志项的最大长度   
5. error_log = E:/php_log/php_error.log        #指定产生的 错误报告写入的日志文件位置  
```

![image-20210727104224721](https://cdn.coder369.com/img/blog/image-20210727104224721.png)

时区配置

```
date.timezone = PRC
```

> 注：默认为UTC（标准时间），PRC（中华人民共和国），修改后需要重新启动php-fpm
>
> ```
> systemctl restart php-fpm
> ```

![image-20210727105316401](https://cdn.coder369.com/img/blog/image-20210727105316401.png)

编码配置

```
default_charset = "UTF-8"
```

