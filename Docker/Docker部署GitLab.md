# Docker安装GitLab



docker-compose.yml

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



![image-20210720022347833](https://cdn.coder369.com/img/blog/image-20210720022347833.png)

超级管理员：root

查看初始秘密cat /server/gitlab/conf/initial_root_password

```
# WARNING: This value is valid only in the following conditions
#          1. If provided manually (either via `GITLAB_ROOT_PASSWORD` environment variable or via `gitlab_rails['initial_root_password']` setting in `gitlab.rb`, it was provided before database was seeded for the first time (usually, the first reconfigure run).
#          2. Password hasn't been changed manually, either via UI or via command line.
#
#          If the password shown here doesn't work, you must reset the admin password following https://docs.gitlab.com/ee/security/reset_user_password.html#reset-your-root-password.

Password: MHmuxP9HW+kzDQ/RpJrxcl54aTBhO8ir647oRPsPqD8=

# NOTE: This file will be automatically deleted in the first reconfigure run after 24 hours.

```

