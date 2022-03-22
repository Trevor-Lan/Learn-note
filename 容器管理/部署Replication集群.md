# 部署Replication集群

DockerHub：https://hub.docker.com/r/mishamx/mysql



下载镜像

```
docker pull mishamx/mysql
```



master

```
docker run -d -p 3306:3306 \
  --name mysql_master \
  -e MYSQL_DATABASE=web \
  -e MYSQL_USER=web \
  -e MYSQL_PASSWORD=web \
  -e MYSQL_ROOT_PASSWORD=root_password \
  -e MYSQL_REPLICATION_USER=user_for_slave \
  -e MYSQL_REPLICATION_PASSWORD=user_password_for_slave \
  mishamx/mysql:5.7
```



slave

```
docker run -d -p 3307:3306  \
  --name mysql_slave \
  -e MYSQL_MASTER_HOST=mysql_master \
  -e MYSQL_MASTER_PORT=3306 \
  -e MYSQL_ROOT_PASSWORD=root_password \
  -e MYSQL_REPLICATION_USER=user_for_slave \
  -e MYSQL_REPLICATION_PASSWORD=user_password_for_slave \
  --link mysql_master:mysql_master \
  mishamx/mysql:5.7
```

