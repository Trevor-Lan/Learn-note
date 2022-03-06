# PXC集群

**创建数据卷**

```
docker volume create v1
docker volume create v2
docker volume create v3
```

**创建网络**

```
docker network create -d overlay --attachable net_pxc
```

**创建PXC节点1**

```
docker run -di -p 33060:3306 -v v1:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -e CLUSTER_NAME=PXC -e XTRABACKUP_PASSWORD=123456 --privileged --name node1 --net
net_pxc pxc:5.7
```

**创建PXC节点2**

```
docker run -di -p 33070:3306 -v v2:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -e CLUSTER_NAME=PXC -e XTRABACKUP_PASSWORD=123456 -e CLUSTER_JOIN=node1 --privileged --name node2 --net net_pxc pxc:5.7
```

**创建PXC节点3**

```
docker run -di -p 33070:3306 -v v3:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -e CLUSTER_NAME=PXC -e XTRABACKUP_PASSWORD=123456 -e CLUSTER_JOIN=node1 --privileged --name node3 --net net_pxc pxc:5.7
```

