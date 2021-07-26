**安装PHP**

```
参考YUM安装PHP指定版本章节
```

**按装pecl**

```
yum install -y php-pear
```

**安装redis扩展**

```
pecl install redis
```

![image-20210726174855959](https://cdn.coder369.com/img/blog/image-20210726174855959.png)

> 注：如果没有安装php-devel，则会报以下错误，此时yum安装一下，然后再继续安装redis扩展
>
> ```
> yum install -y php-devel
> ```

![image-20210726174445812](https://cdn.coder369.com/img/blog/image-20210726174445812.png)

**修改配置文件**

```
echo "extension=redis" > /etc/php.d/50-redis.ini
```

**查看扩展**

```
php -v
```

```
[root@22ec960b86e0 /]# php -m
[PHP Modules]
bz2
calendar
Core
ctype
curl
date
dom
exif
fileinfo
filter
ftp
gd
gettext
hash
iconv
json
ldap
libxml
mbstring
mysqli
mysqlnd
odbc
openssl
pcntl
pcre
PDO
pdo_mysql
PDO_ODBC
pdo_sqlite
Phar
posix
readline
redis
Reflection
session
shmop
SimpleXML
soap
sockets
sodium
SPL
sqlite3
standard
sysvmsg
sysvsem
sysvshm
tokenizer
xml
xmlreader
xmlrpc
xmlwriter
xsl
zlib

[Zend Modules]
```

