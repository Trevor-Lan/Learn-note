# Typora配置七牛云



**1 下载并安装typora**

官网：https://www.typora.io

![image-20210720001951186](https://cdn.coder369.com/img/blog/image-20210720001951186.png)



**2 下载并安装pic-go**

GitHub：https://github.com/Molunerfinn/PicGo

![image-20210720002350769](https://cdn.coder369.com/img/blog/image-20210720002350769.png)

在pic-go中配置七牛云

![image-20210720002905414](https://cdn.coder369.com/img/blog/image-20210720002905414.png)



**3 安装PicGo-Core**

GitHub：https://github.com/PicGo/PicGo-Core

```
npm install picgo -g
```



**4 配置typora**

![image-20210720003144474](https://cdn.coder369.com/img/blog/image-20210720003144474.png)



![image-20210720003256930](https://cdn.coder369.com/img/blog/image-20210720003256930.png)

填写七牛云信息

```json
{
  "picBed": {
    "current": "qiniu",
    "uploader": "qiniu",
    "smms": {
      "token": ""
    },
    "qiniu": {
      "accessKey": "******************************",
      "area": "z2",
      "bucket": "cdn-blog-img",
      "options": "",
      "path": "img/blog/",
      "secretKey": "******************************",
      "url": "https://cdn.domain.com"
    }
  },
  "picgoPlugins": {}
}
```

