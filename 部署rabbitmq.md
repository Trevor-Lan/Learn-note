# Docker搭建rabbitmq

pull带有web界面的rabbitmq

```
docker pull rabbitmq:management
```

启动rabbitmq容器

```
docker run -dit --name Myrabbitmq -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=admin -p 15672:15672 -p 5672:5672 rabbitmq:management
```

访问rabbitmq

```
http://ip:15672
```

