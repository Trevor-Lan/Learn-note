### 镜像加速

**配置镜像**

方法一：全局配置

```
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

方法二：修改配置文件

```
composer config repo.packagist composer https://packagist.phpcomposer.com
```

**解除镜像**

```
composer config -g --unset repos.packagist
```

### 基本命令

查看命令

```
composer list
```

初始化

```
composer init
```

查找

```
composer search
```

安装

```
composer install
```

声明依赖

```
composer require
```

更新

```
composer update
```

### composer命令文档

https://docs.phpcomposer.com/03-cli.html

