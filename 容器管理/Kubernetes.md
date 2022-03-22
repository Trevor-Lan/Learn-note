## 基础
### 安装
#### 方式一：minikube

下载并安装minikube：https://minikube.sigs.k8s.io/docs/start

启动集群

```
minikube start
```
停止集群

```
minikube stop
```

安装集群GUI

```
minikube dashboard
```

删除集群

```
minikube delete --all
```

#### 方式二：裸机安装
关闭防火墙
```
systemctl stop firewalld
systemctl disable firewalld
```
禁用SELinux（临时）
```
setenforce 0
```
禁用SELinux（永久）

```
sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config
```

关闭swap（临时）
```
swapoff -a  
```

关闭swap（永久）

```
sed -ri 's/.*swap.*/#&/' /etc/fstab
```

