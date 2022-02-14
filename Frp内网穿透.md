## 下载

GitHub：https://github.com/fatedier/frp/releases

根据操作系统下载对应的版本，Windows客户端下载Windows版本，Linux服务端下载Linux版本

![image-20220214130448857](https://cdn.coder369.com/img/blog/image-20220214130448857.png)



## 服务端

配置（frps.ini）

```ini
[common]
bind_port = 7000
vhost_http_port = 7001

#连接池
max_pool_count = 5

#自定义二级域名
subdomain_host = coder369.com

#控制面板
dashboard_port = 7003
dashboard_user = admin
dashboard_pwd = password

#日志
log_file = ./frps.log
log_level = info
log_max_days = 3
```

启动

```shell
nohup ./frps -c ./frps.ini > running.log 2>&1 &
```



## 客户端

配置（frpc.ini）

```ini
[common]
server_addr = 106.52.40.152
server_port = 7000

[api]
type = http
local_port = 9501
subdomain = api

[ws]
type = tcp
local_port = 9502
subdomain = api
protocol = websocket
remote_port = 7002
```

启动

```shell
frpc.exe -c frpc.ini
```



## 注意事项

1. 内网穿透的域名需要解析到服务器上