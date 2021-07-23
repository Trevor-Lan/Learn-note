# Docker部署常用应用



Filebrowser

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



gitlab

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



mysql

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



netdata

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



nginx-proxy

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



phpmyadmin

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



rabbitmq

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



redis

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



redmine

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



nginx

docker:https://hub.docker.com/_/nginx

```yml
version: '3'
services:
  swagger:
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



vaultwarden

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

