下载php源码

```
git clone https://github.com/php/php-src.git
```

切换到ext目录

```
cd ext
```

生成扩展目录

```
php ext_skel.php --ext 扩展名称
```

切换到扩展目录下

```
cd 扩展目录
```

编译

```
phpize
./configure
make && make install
```

> 注phpize需要php-devel扩展，可以使用yum -y install php-devel安装

