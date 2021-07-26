**docker-compose**

```yml
version: '3'

services:
  www:
    image: lwqbrell/www:fpm-nginx
    container_name: www
    privileged: true
    volumes:
      - /docker/www/data:/www
      - /docker/www/conf.d/default.conf:/etc/nginx/conf.d/default.conf
    ports:
      - "9980:80"
  db:
    image: mysql:5.7
    restart: always
    container_name: mysql57
    environment:
      MYSQL_ROOT_PASSWORD: ah4gsVFY4cTP   
  phpmyadmin:
    image: phpmyadmin:latest
    restart: always
    container_name: phpmyadmin
    ports:
      - "9990:80"
    external_links:
      - mysql57
  redis:
    image: redis:latest
    restart: always
    container_name: redis
```

 **default.conf**

```nginx
server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;

    location / {
        root   /www/public;
        index  index.html index.php index.htm;
        if (!-e $request_filename){
          rewrite ^(.*)$ /index.php?s=$1 last; break;
        }
    }

    location ~ \.php$ {
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  /www/public/$fastcgi_script_name;
        include        fastcgi_params;
    }
}
```

