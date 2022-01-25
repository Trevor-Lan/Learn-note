官网教程：https://www.php.net/manual/zh/install.unix.nginx.php

**下载源码**

```
https://www.php.net/releases
```

或

```
https://museum.php.net
```

**解压**

```
tar -zvxf php-x.x.x
```

**安装编译工具**

```
yum install -y gcc gcc-c++ make libxml2-devel
```

**配置并构建PHP**

```
cd ../php-x.x.x
./configure --enable-fpm
make
make install
```

> 注：可以使用 ./configure --help查看更多配置选项
>
> 如果出现：
>
> ![image-20210729112211818](https://cdn.coder369.com/img/blog/image-20210729112211818.png)
>
> ```
> yum install sqlite-devel
> ```
>
> 

创建配置文件

```
cp php.ini-development /usr/local/php/php.ini
cp /usr/local/etc/php-fpm.d/www.conf.default /usr/local/etc/php-fpm.d/www.conf
cp sapi/fpm/php-fpm /usr/local/bin
```

