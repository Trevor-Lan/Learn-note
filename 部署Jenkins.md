# 部署Jenkins

官网：https://www.jenkins.io/zh

DockerHub：https://hub.docker.com/_/jenkins



pull Jenkins

```
docker pull jenkins
```

运行容器

```
docker run -d --name jenkins -p 8080:8080 -p 50000:50000 -v /your/home:/var/jenkins_home jenkins
```

获取初始密码

```
cat /var/jenkins_home/secrets/initialAdminPassword
```

