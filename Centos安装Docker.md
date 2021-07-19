# Centos安装Docker

官网地址：https://docs.docker.com/get-docker

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

通过运行`hello-world` 映像验证 Docker Engine 是否已正确安装。

```
docker run hello-world
```

