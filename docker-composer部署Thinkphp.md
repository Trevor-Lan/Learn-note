# docker-compose部署Thinkphp



```yml
version: '3'

services:
  nginx:
    image: nginx
    container_name: nginx2
    volumes:
      - /server/fangzhou/nginx/www:/www
      - /server/fangzhou/nginx/conf.d/default.conf:/etc/nginx/conf.d/default.conf
    ports:
      - "8080:80"
    networks:
      - default
  php:
    image: php:fpm
    container_name: php
    volumes:
      - /server/fangzhou/nginx/www:/www
    networks:
      - default
  db:
    image: mysql:5.7
    restart: always
    container_name: mysql57
    volumes:
      - /server/fangzhou/mysql5.7/data:/var/lib/mysql
    networks:
      - default
    environment:
      MYSQL_ROOT_PASSWORD: ah4gsVFY4cTP   
  phpmyadmin:
    image: phpmyadmin
    restart: always
    depends_on:
      - db
    container_name: phpmyadmin
    ports:
      - "8000:80"
    networks:
      - default
    external_links:
      - mysql57
  redis:
    image: redis:latest
    restart: always
    container_name: redis
    volumes:
      - /server/fangzhou/redis/data:/data
    command: [ "redis-server", "/server/fangzhou/redis/conf/redis.conf" ]
    networks:
      - default
networks:
  default:
    external: true
    name: net_www
```

