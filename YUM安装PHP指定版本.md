# YUM安装PHP指定版本

**安装epel-release**

```
yum -y install epel-release
```

**添加remi源**

```
rpm -Uvh http://rpms.remirepo.net/enterprise/remi-release-7.rpm
```

> 注：
>
> php yum源站点：http://rpms.remirepo.net
>
> 根据操作系统版本下载不同的yum

**安装yum-config-manager**

```
yum -y install yum-utils
```

**指定PHP版本**

```
yum-config-manager --enable remi-php70
```

> 注：指定PHP版本的格式为remi-phpxx，比如
>
> 5.4的版本：remi-php54
>
> 7.0的版本：remi-php70
>
> 7.4的版本：remi-php74

**安装PHP**

```
yum install -y php
```

**安装扩展**

```
yum -y install php-mysql php-gd php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-soap curl curl-devel php-devel
```

**安装fpm**

```
yum install -y php-fpm
```

**启动fpm**

```
php-fpm
```

**查看9000端口是否在监听**

```
netstat -tulnp
```

>  注：如果出现
>
> bash: netstat: command not found
>
> 则：
>
> ```
> yum install -y net-tools
> ```









