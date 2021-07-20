# Docker run常见问题



**docker运行centos后无法使用systemctl**

在run命令中加入--privileged参数，并指定/usr/sbin/init作为启动命令，例如

```
docker run -itd --name centos --privileged centos:7 /usr/sbin/init
```



