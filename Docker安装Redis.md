# Docker安装Redis



**下载redis镜像**

```
docker pull redis
```

**下载redis配置文件**

官方：http://www.redis.cn/download.html

![image-20210721174620935](https://cdn.coder369.com/img/blog/image-20210721174620935.png)

![image-20210721174732640](https://cdn.coder369.com/img/blog/image-20210721174732640.png)

**修改以下默认配置**

```
bind 127.0.0.1        #注释掉这部分，使redis可以外部访问
daemonize no          #用守护线程的方式启动
requirepass password  #给redis设置密码
appendonly yes        #redis持久化　　默认是no
tcp-keepalive 300     #防止出现远程主机强迫关闭了一个现有的连接的错误 默认是300
```

**运行容器**

```
docker run -p 6379:6379 --name redis -v /server/redis/redis.conf:/etc/redis/redis.conf  -v /server/redis/data:/data -d redis redis-server /etc/redis/redis.conf --appendonly yes
```

参数说明：

> -p 6379:6379                                                                把容器内的6379端口映射到宿主机6379端口
> -v /data/redis/redis.conf:/etc/redis/redis.conf       把宿主机配置好的redis.conf放到容器内的这个位置中
> -v /data/redis/data:/data                                           把redis持久化的数据在宿主机内显示，做数据备份
> redis-server /etc/redis/redis.conf                            这个是关键配置，让redis不是无配置启动，而是按照这个redis.conf的配置启动
> –appendonly yes                                                         redis启动后数据持久化

