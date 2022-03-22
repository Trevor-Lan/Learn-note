## 安装Linux子系统

应用商店中查找Linux子系统

![image-20220215105410542](https://cdn.coder369.com/img/blog/image-20220215105410542.png)

> 注：如果提示wls相关错误的话，则更新wls
>
> WLS下载更新：https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi



## 设置root密码

第一次打开时，首先设置自己的用户名和密码，然后再设置root密码

```
coder@WIN-N9TALMBR5NO:~$ sudo passwd
[sudo] password for coder:                  // 用户密码
New password:                               // root密码
Retype new password:                        // 确认root密码
passwd: password updated successfully
coder@WIN-N9TALMBR5NO:~$ su root            // 切换到root
Password:                                   // 输入root密码
root@WIN-N9TALMBR5NO:/home/coder#
```

