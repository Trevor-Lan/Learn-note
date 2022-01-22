## 查找并kill进程

```
ps -ef | grep 查找名称 | awk '{print $2}' | xargs kill -9
```

