# 安装portainer

文档：https://documentation.portainer.io/v2.0/deploy/ceinstalldocker



**独立部署**

创建数据卷

```
docker volume create portainer_data
```

运行portainer容器

```
docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```

![image-20210720015212294](https://cdn.coder369.com/img/blog/image-20210720015212294.png)

![image-20210720015323203](https://cdn.coder369.com/img/blog/image-20210720015323203.png)

![image-20210720015450283](https://cdn.coder369.com/img/blog/image-20210720015450283.png)

**代理模式**

```
docker run -d -p 9001:9001 --name portainer_agent --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/docker/volumes:/var/lib/docker/volumes portainer/agent
```



