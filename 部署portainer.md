# 搭建portainer

官方文档：https://documentation.portainer.io/v2.0/deploy/ceinstalldocker

DockerHub：https://hub.docker.com/r/portainer/portainer-ce

创建数据卷

```
docker volume create portainer_data
```

运行portainer容器

```
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```

访问

```
http://ip:90000
```

