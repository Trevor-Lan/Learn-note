## 基础
### 安装
移除原有的docker（没有则跳过）
```
sudo yum remove docker*
```
安装yum-utils
```
sudo yum install -y yum-utils
```
配置docker的yum地址
```
sudo yum-config-manager \
--add-repo \
http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```
安装指定版本
```
sudo yum install -y docker-ce-20.10.7 docker-ce-cli-20.10.7 containerd.io-1.4.6
```
启动docker
```
systemctl enable docker
systemctl start docker
```
docker加速配置
```
cat > /etc/docker/daemon.json << EOF
{
"registry-mirrors": ["https://rlhg2sxi.mirror.aliyuncs.com"]
}
EOF
```
重启docker
```
sudo systemctl daemon-reload
sudo systemctl restart docker
```
## 架构
## 仓库
## 镜像
## 容器
## 编排

## 部署

### Filebrowser

docker:https://hub.docker.com/r/filebrowser/filebrowser

```yml
version: '3'
services:
  netdata:
    image: filebrowser/filebrowser
    container_name: filebrowser
    restart: unless-stopped
    networks:
      - default
    volumes:
      - /:/srv
networks:
  default:
    external: true
    name: nginx-proxy_default 
```

### GitLab

docker:https://hub.docker.com/r/gitlab/gitlab-ce

```yml
version: '3'
services:
  web:
    image: gitlab/gitlab-ce:latest
    container_name: gitlab
    restart: always
    hostname: gitlab.coder369.com
    volumes:
      - /server/gitlab/conf:/etc/gitlab
      - /server/gitlab/logs:/var/log/gitlab
      - /server/gitlab/data:/var/opt/gitlab
networks:
  default:
    external: true
    name: nginx-proxy_default
```

### MySQL

docker:https://hub.docker.com/_/mysql

```yml
version: '3'
services:
  db:
    image: mysql:5.7
    restart: always
    container_name: mysql5.7
    networks:
      - default
    volumes:
      - /server/mysql/mysql5.7:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: ah4gsVFY4cTP
networks:
  default:
    external: true
    name: nginx-proxy_default 
```

### Netdata

docker:https://hub.docker.com/r/netdata/netdata

```yml
version: '3'
services:
  netdata:
    image: netdata/netdata
    container_name: netdata
    hostname: https://netdata.coder369.com
    restart: unless-stopped
    cap_add:
      - SYS_PTRACE
    security_opt:
      - apparmor:unconfined
    networks:
      - default
    volumes:
      - /etc/passwd:/host/etc/passwd:ro
      - /etc/group:/host/etc/group:ro
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /etc/os-release:/host/etc/os-release:ro
networks:
  default:
    external: true
    name: nginx-proxy_default 
```

### Nginx-Proxy

docker:https://hub.docker.com/r/jc21/nginx-proxy-manager

```yml
version: '3'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '443:443'
    environment:
      DB_MYSQL_HOST: "db"
      DB_MYSQL_PORT: 3306
      DB_MYSQL_USER: "proxy"
      DB_MYSQL_PASSWORD: "nQXYmkrHed77PoY8"
      DB_MYSQL_NAME: "proxy"
    volumes:
      - /server/nginx-proxy/data:/data
      - /server/nginx-proxy/letsencrypt:/etc/letsencrypt
  db:
    image: 'jc21/mariadb-aria:latest'
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: 'fXSR3C8zQq3uXJSL'
      MYSQL_DATABASE: 'proxy'
      MYSQL_USER: 'proxy'
      MYSQL_PASSWORD: 'nQXYmkrHed77PoY8'
    volumes:
      - /server/nginx-proxy/mariadb:/var/lib/mysql
```

### phpMyAdmin

docker:https://hub.docker.com/_/phpmyadmin

```yml
version: '3'
services:
  phpmyadmin:
    image: phpmyadmin
    restart: always
    container_name: phpmyadmin
    networks:
      - default
    external_links:
      - mysql57
networks:
  default:
    external: true
    name: nginx-proxy_default 
```

### Rabbitmq

docker:https://hub.docker.com/_/rabbitmq

```yml
version: '3'
services:
  rabbitmq:
    image: rabbitmq:3-management
    container_name: rabbitmq
    restart: always
    hostname: rabbitmq.coder369.com
    volumes:
      - /server/rabbitmq:/var/lib/rabbitmq
    networks:
      - default
networks:
  default:
    external: true
    name: nginx-proxy_default
```

### Redis

docker:https://hub.docker.com/_/redis

```yml
version: '3'
services:
  redis:
    image: redis:latest
    restart: always
    container_name: redis
    networks:
      - default
    volumes:
      - /server/redis:/data
networks:
  default:
    external: true
    name: nginx-proxy_default 
```

### Redmine

docker:https://hub.docker.com/_/redmine

```yml
version: '3'
services:
  redmine:
    image: redmine
    restart: always
    container_name: redmine_web
    networks:
      - default
    volumes:
      - /server/redmine/files:/usr/src/redmine/files
      - /server/redmine/plugins:/usr/src/redmine/plugins
    depends_on:
      - db
    environment:
      REDMINE_DB_MYSQL: redmine_mysql
      REDMINE_DB_PASSWORD: wRjANqsxPbBs9BJ5t
      REDMINE_DB_USERNAME: redmine

  db:
    image: mysql:5.7
    restart: always
    container_name: redmine_mysql
    networks:
      - default
    volumes:
      - /server/redmine/mysql:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: HUim8m3jjktchCn4
      MYSQL_USER: redmine
      MYSQL_PASSWORD: wRjANqsxPbBs9BJ5t
      MYSQL_DATABASE: redmine
networks:
  default:
    external: true
    name: nginx-proxy_default 
```

### Nginx

docker:https://hub.docker.com/_/nginx

```yml
version: '3'
services:
  www:
    image: nginx:latest
    container_name: nginx
    restart: unless-stopped
    networks:
      - default
    volumes:
      - /server/nginx/html:/usr/share/nginx/html
networks:
  default:
    external: true
    name: nginx-proxy_default
```

### Vaultwarden

docker：https://hub.docker.com/r/vaultwarden/server

```yml
version: '3'
services:
  bitwarden:
    image: vaultwarden/server:latest
    container_name: vaultwarden
    restart: always
    volumes:
      - /server/vaultwarden/data:/data
    networks:
      - default
    environment:
      SIGNUPS_ALLOWED: 'false'
      DOMAIN: 'https://vaultwarden.coder369.com'
      WEB_VAULT_ENABLED: 'false'
networks:
  default:
    external: true
    name: nginx-proxy_default 
```

### Replication集群

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

### PXC集群

创建数据卷

```
docker volume create v1
docker volume create v2
docker volume create v3
```

创建网络

```
docker network create -d overlay --attachable net_pxc
```

创建PXC节点1

```
docker run -di -p 33060:3306 -v v1:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -e CLUSTER_NAME=PXC -e XTRABACKUP_PASSWORD=123456 --privileged --name node1 --net
net_pxc pxc:5.7
```

创建PXC节点2

```
docker run -di -p 33070:3306 -v v2:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -e CLUSTER_NAME=PXC -e XTRABACKUP_PASSWORD=123456 -e CLUSTER_JOIN=node1 --privileged --name node2 --net net_pxc pxc:5.7
```

创建PXC节点3

```
docker run -di -p 33070:3306 -v v3:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -e CLUSTER_NAME=PXC -e XTRABACKUP_PASSWORD=123456 -e CLUSTER_JOIN=node1 --privileged --name node3 --net net_pxc pxc:5.7
```

## 数据
## 网络
### docker0网桥
docker启动的时候会自动在宿主机上创建docker0网桥，之后创建的容器在没有指定网络的情况下会自动连接到该网桥上，如此以来就可以实现容器与主机、容器与容器之间的网络通讯了。
![image.png](https://cdn.coder369.com/img/blog/WEBRESOURCEcdc16ede6aa599d1b992aef4009de1ab)

#### 实验一：容器与主机通讯
创建容器1（名称：box1；镜像busybox）
```
docker run -itd --name box1 busybox
```
查看容器ip
```
docker exec -it box1 ifconfig
```
![image.png](https://cdn.coder369.com/img/blog/WEBRESOURCEb5cdf91057cc9d9b1b8cdd1910efaf6a)
宿主机ping容器

```
ping 172.17.0.2
```
![iamge.png](https://cdn.coder369.com/img/blog/WEBRESOURCE886017a47cfc565d5d99a8f63596aff5)

> 以上实验表明，创建容器时，如果不指定网络的话，容器会默认连接到docker0网桥上，并且可以实现与宿主机的网络通讯

#### 实验二：容器与容器间通讯
创建容器2（名称：box2；镜像busybox）
```
docker run -itd --name box2 busybox
```
查看容器ip
```
docker exec -it box2 ifconfig
```
![image.png](https://cdn.coder369.com/img/blog/WEBRESOURCEce745fecbe8121a8d7d7e6d41b2366d5)
容器1 ping 容器2
![image.png](https://cdn.coder369.com/img/blog/WEBRESOURCEa573c69d674d6afafd50dd5094b15160)

> 以上实验表明，连接到docker0网桥上的容器之间可以实现相互通讯
#### 原理
创建容器的时候，docker会在容器与宿主机之间创建成对的虚拟网卡
![image.png](https://cdn.coder369.com/img/blog/WEBRESOURCE7ce7635fe0c51af7e1c010b6dea7de12)
![image.png](https://cdn.coder369.com/img/blog/WEBRESOURCE9884959f0645444a6cd177305476eb95)

### 容器连接（link）
link参数可以在创建容器的时候指定要连接的容器名称，这样创建的容器会在容器的/etc/host文件里生成互联容器的ip映射表，这样可以通过容器的名称直接ping到该容器

创建box3容器（link box1）
```
docker run -itd --name box3 --link box1 busybox
```
box3 ping box1
![image.png](https://cdn.coder369.com/img/blog/WEBRESOURCE0b6d1f8463473047bae4de4ccddae008)

> 注意，link属性创建的容器，只能单向的通过容器名访问，要实现容器名的双向访问可以通过自定义网络的形式来实现（推荐使用自定义网络）
### 自定义网络
## 安全

