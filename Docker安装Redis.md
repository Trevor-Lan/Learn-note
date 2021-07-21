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
docker run -v /redis/redis.conf:/redis/redis.conf --name redis -d -p 6379:6379 redis redis-server /redis/redis.conf
```



