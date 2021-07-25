# Docker环境中安装PHP扩展



安装redis扩展

```
pecl install redis
```

编辑配置文件（/usr/local/etc/php/conf.d/docker-php-ext-sodium.ini）

```
extension=redis
```

> 注：如果容器中不能vi的话，则可以中宿主机上先编辑好，然后再拷贝到容器中
>
> docker cp php.in /usr/local/etc/php/conf.d/docker-php-ext-sodium.ini

重启容器



