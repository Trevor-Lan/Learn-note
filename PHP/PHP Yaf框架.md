## 安装yaf扩展

查看php版本信息

```php
phpinfo();
```

![image-20220116010001459](https://cdn.coder369.com/img/blog/image-20220116010001459.png)

现在yaf扩展

地址：https://pecl.php.net/package/yaf

![image-20220116010305741](https://cdn.coder369.com/img/blog/image-20220116010305741.png)

根据phpinfo查看的信息下载对应的扩展

![image-20220116010404214](https://cdn.coder369.com/img/blog/image-20220116010404214.png)

把扩展复制到php的ext目录下

![image-20220116010609442](https://cdn.coder369.com/img/blog/image-20220116010609442.png)

php.ini中开启yaf扩展

![image-20220116010812251](https://cdn.coder369.com/img/blog/image-20220116010812251.png)

重启php-cgi服务

![image-20220116010950939](https://cdn.coder369.com/img/blog/image-20220116010950939.png)



## phpstorm yaf提示

下载提示文件

https://github.com/xudianyang/yaf.auto.complete/archive/master.zip

下载后解压到PhpStorm x.x.x\plugins\php\lib\yaf目录下（手动创建该目录）

![image-20220116011309266](https://cdn.coder369.com/img/blog/image-20220116011309266.png)

配置提示目录

![image-20220116011407044](https://cdn.coder369.com/img/blog/image-20220116011407044.png)

![image-20220116011448570](https://cdn.coder369.com/img/blog/image-20220116011448570.png)

