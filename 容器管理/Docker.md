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
### 加速

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

### Docker官方

https://hub.docker.com

### Harbor

https://goharbor.io

### 云服务仓库

阿里云容器服务

腾讯云容器服务

## 镜像

### 搜索

```shell
Usage:  docker search [OPTIONS] TERM

Search the Docker Hub for images

Options:
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print search using a Go template
      --limit int       Max number of search results (default 25)
      --no-trunc        Don't truncate output
```

### 拉取

```shell
Usage:  docker pull [OPTIONS] NAME[:TAG|@DIGEST]

Pull an image or a repository from a registry

Options:
  -a, --all-tags                Download all tagged images in the repository
      --disable-content-trust   Skip image verification (default true)
      --platform string         Set platform if server is multi-platform
                                capable
  -q, --quiet                   Suppress verbose output
```

### 查看

```shell
Usage:  docker images [OPTIONS] [REPOSITORY[:TAG]]

List images

Options:
  -a, --all             Show all images (default hides intermediate images)
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print images using a Go template
      --no-trunc        Don't truncate output
  -q, --quiet           Only show image IDs
```

### 导入

```shell
Usage:  docker import [OPTIONS] file|URL|- [REPOSITORY[:TAG]]

Import the contents from a tarball to create a filesystem image

Options:
  -c, --change list       Apply Dockerfile instruction to the created image
  -m, --message string    Set commit message for imported image
      --platform string   Set platform if server is multi-platform capable
```

### 导出

```shell
Usage:  docker export [OPTIONS] CONTAINER

Export a container's filesystem as a tar archive

Options:
  -o, --output string   Write to a file, instead of STDOUT
```

### 构建

```shell
Usage:  docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]

Create a new image from a container's changes

Options:
  -a, --author string    Author (e.g., "John Hannibal Smith
                         <hannibal@a-team.com>")
  -c, --change list      Apply Dockerfile instruction to the created image
  -m, --message string   Commit message
  -p, --pause            Pause container during commit (default true)
```

```shell
sage:  docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]

Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
```

### Dockerfile

```
FROM
MAINTAINER
RUN
CMD
VOLUME
USER
LABEL
WORKDIR
ARG
EXPOSE
ENV
ADD
COPY
ENTYPOINT
```

### 删除

```shell
Usage:  docker rmi [OPTIONS] IMAGE [IMAGE...]

Remove one or more images

Options:
  -f, --force      Force removal of the image
      --no-prune   Do not delete untagged parents
```

### 检查

```shell
Usage:  docker inspect [OPTIONS] NAME|ID [NAME|ID...]

Return low-level information on Docker objects

Options:
  -f, --format string   Format the output using the given Go template
  -s, --size            Display total file sizes if the type is container
      --type string     Return JSON for specified type
```

## 容器

### 启动

```shell
Usage:  docker unpause CONTAINER [CONTAINER...]

Unpause all processes within one or more containers
```

```shell
Usage:  docker start [OPTIONS] CONTAINER [CONTAINER...]

Start one or more stopped containers

Options:
  -a, --attach               Attach STDOUT/STDERR and forward signals
      --detach-keys string   Override the key sequence for detaching a
                             container
  -i, --interactive          Attach container's STDIN
```

### 查看

```shell
Usage:  docker ps [OPTIONS]

List containers

Options:
  -a, --all             Show all containers (default shows just running)
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print containers using a Go template
  -n, --last int        Show n last created containers (includes all
                        states) (default -1)
  -l, --latest          Show the latest created container (includes all
                        states)
      --no-trunc        Don't truncate output
  -q, --quiet           Only display container IDs
  -s, --size            Display total file sizes
```

### 日志

```shell
Usage:  docker logs [OPTIONS] CONTAINER

Fetch the logs of a container

Options:
      --details        Show extra details provided to logs
  -f, --follow         Follow log output
      --since string   Show logs since timestamp (e.g.
                       2013-01-02T13:23:37Z) or relative (e.g. 42m for 42
                       minutes)
  -n, --tail string    Number of lines to show from the end of the logs
                       (default "all")
  -t, --timestamps     Show timestamps
      --until string   Show logs before a timestamp (e.g.
                       2013-01-02T13:23:37Z) or relative (e.g. 42m for 42
                       minutes)
```

### 停止

```shell
Usage:  docker stop [OPTIONS] CONTAINER [CONTAINER...]

Stop one or more running containers

Options:
  -t, --time int   Seconds to wait for stop before killing it (default 10)
```

### 暂停

```shell
Usage:  docker pause CONTAINER [CONTAINER...]

Pause all processes within one or more containers
```

### 重启

```shell
Usage:  docker restart [OPTIONS] CONTAINER [CONTAINER...]

Restart one or more containers

Options:
  -t, --time int   Seconds to wait for stop before killing the container
```

### 进入

```shell
Usage:  docker attach [OPTIONS] CONTAINER

Attach local standard input, output, and error streams to a running container

Options:
      --detach-keys string   Override the key sequence for detaching a
                             container
      --no-stdin             Do not attach STDIN
      --sig-proxy            Proxy all received signals to the process
                             (default true)
```

```shell
Usage:  docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

Run a command in a running container

Options:
  -d, --detach               Detached mode: run command in the background
      --detach-keys string   Override the key sequence for detaching a
                             container
  -e, --env list             Set environment variables
      --env-file list        Read in a file of environment variables
  -i, --interactive          Keep STDIN open even if not attached
      --privileged           Give extended privileges to the command
  -t, --tty                  Allocate a pseudo-TTY
  -u, --user string          Username or UID (format:
                             <name|uid>[:<group|gid>])
  -w, --workdir string       Working directory inside the container
```

### 删除

```shell
Usage:  docker rm [OPTIONS] CONTAINER [CONTAINER...]

Remove one or more containers

Options:
  -f, --force     Force the removal of a running container (uses SIGKILL)
  -l, --link      Remove the specified link
  -v, --volumes   Remove anonymous volumes associated with the container
```

### 复制

```shell
Usage:  docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
        docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH

Copy files/folders between a container and the local filesystem

Use '-' as the source to read a tar archive from stdin
and extract it to a directory destination in a container.
Use '-' as the destination to stream a tar archive of a
container source to stdout.

Options:
  -a, --archive       Archive mode (copy all uid/gid information)
  -L, --follow-link   Always follow symbol link in SRC_PATH
```

## 编排

### Swarm

### Mesos

### Kubernetes

## 部署

### docker compose

### docker stack

### 应用部署

#### Filebrowser

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

#### GitLab

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

#### MySQL

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

#### Netdata

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

#### Nginx-Proxy

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

#### phpMyAdmin

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

#### Rabbitmq

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

#### Redis

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

#### Redmine

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

#### Nginx

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

#### Vaultwarden

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

#### Replication集群

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

#### PXC集群

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

### 数据卷

```shell
Usage:  docker volume COMMAND

Manage volumes

Commands:
  create      Create a volume
  inspect     Display detailed information on one or more volumes    
  ls          List volumes
  prune       Remove all unused local volumes
  rm          Remove one or more volumes
```

### 目录挂载

### 数据卷容器

## 网络
### docker0
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
#### 通讯原理
创建容器的时候，docker会在容器与宿主机之间创建成对的虚拟网卡
![image.png](https://cdn.coder369.com/img/blog/WEBRESOURCE7ce7635fe0c51af7e1c010b6dea7de12)
![image.png](https://cdn.coder369.com/img/blog/WEBRESOURCE9884959f0645444a6cd177305476eb95)

### 容器连通
link参数可以在创建容器的时候指定要连接的容器名称，这样创建的容器会在容器的/etc/host文件里生成互联容器的ip映射表，这样可以通过容器的名称直接ping到该容器

创建box3容器（link box1）
```
docker run -itd --name box3 --link box1 busybox
```
box3 ping box1
![image.png](https://cdn.coder369.com/img/blog/WEBRESOURCE0b6d1f8463473047bae4de4ccddae008)

> 注意，link属性创建的容器，只能单向的通过容器名访问，要实现容器名的双向访问可以通过自定义网络的形式来实现（推荐使用自定义网络）
### 自定义网络

```shell
Usage:  docker network create [OPTIONS] NETWORK

Create a network

Options:
      --attachable           Enable manual container attachment
      --aux-address map      Auxiliary IPv4 or IPv6 addresses used by        
                             Network driver (default map[])
      --config-from string   The network from which to copy the configuration
      --config-only          Create a configuration only network
  -d, --driver string        Driver to manage the Network (default "bridge") 
      --gateway strings      IPv4 or IPv6 Gateway for the master subnet      
      --ingress              Create swarm routing-mesh network
      --internal             Restrict external access to the network
      --ip-range strings     Allocate container ip from a sub-range
      --ipam-driver string   IP Address Management Driver (default "default")
      --ipam-opt map         Set IPAM driver specific options (default map[])
      --ipv6                 Enable IPv6 networking
      --label list           Set metadata on a network
  -o, --opt map              Set driver specific options (default map[])     
      --scope string         Control the network's scope
      --subnet strings       Subnet in CIDR format that represents a
                             network segment
```

创建自定义子网

```shell
docker network create --subnet 192.168.0.0/16 --gateway 192.168.0.1 -d bridge diy-net
```

> 注：自定义的子网，连接在该子网上的容器之间可以通过容器名相互ping通

## 安全

