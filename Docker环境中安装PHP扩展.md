## 方式1

PHP容器中安装扩展

```
docker-php-ext-install 扩展名  
```

例如

```
docker-php-ext-install pcntl  
```



## 方式2

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



