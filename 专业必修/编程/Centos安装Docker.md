# Centos安装Docker

官网地址：https://docs.docker.com/get-docker

![image-20210719165408531](https://cdn.coder369.com/img/blog/image-20210719165408531.png)

安装yum-utils

```
yum install -y yum-utils
```

添加docker yum包

```
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

安装最新版本的 Docker Engine 和 containerd

```
yum install docker-ce docker-ce-cli containerd.io
```

启动 Docker。

```
systemctl start docker
```

开机自启动

```
systemctl enable docker
```

