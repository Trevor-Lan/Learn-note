## 常用

初始化

```php
curl_init(string $url = null): resource
```

设置属性

```php
curl_setopt(resource $ch, int $option, mixed $value): bool
```

执行并获取结果

```php
curl_exec(resource $ch): mixed
```

释放句柄

```php
curl_close(resource $ch): void
```

错误代码

```php
curl_errno(resource $ch): int
```

错误信息

```php
curl_error(resource $ch): string
```



## 其它

- [curl_copy_handle](https://www.php.net/manual/zh/function.curl-copy-handle.php) — 复制一个cURL句柄和它的所有选项
- [curl_escape](https://www.php.net/manual/zh/function.curl-escape.php) — 使用 URL 编码给定的字符串
- [curl_file_create](https://www.php.net/manual/zh/function.curl-file-create.php) — 创建一个 CURLFile 对象
- [curl_getinfo](https://www.php.net/manual/zh/function.curl-getinfo.php) — 获取一个cURL连接资源句柄的信息
- [curl_multi_add_handle](https://www.php.net/manual/zh/function.curl-multi-add-handle.php) — 向curl批处理会话中添加单独的curl句柄
- [curl_multi_close](https://www.php.net/manual/zh/function.curl-multi-close.php) — 关闭一组cURL句柄
- [curl_multi_errno](https://www.php.net/manual/zh/function.curl-multi-errno.php) — 返回上一次 curl 批处理的错误码
- [curl_multi_exec](https://www.php.net/manual/zh/function.curl-multi-exec.php) — 运行当前 cURL 句柄的子连接
- [curl_multi_getcontent](https://www.php.net/manual/zh/function.curl-multi-getcontent.php) — 如果设置了CURLOPT_RETURNTRANSFER，则返回获取的输出的文本流
- [curl_multi_info_read](https://www.php.net/manual/zh/function.curl-multi-info-read.php) — 获取当前解析的cURL的相关传输信息
- [curl_multi_init](https://www.php.net/manual/zh/function.curl-multi-init.php) — 返回一个新cURL批处理句柄
- [curl_multi_remove_handle](https://www.php.net/manual/zh/function.curl-multi-remove-handle.php) — 移除cURL批处理句柄资源中的某个句柄资源
- [curl_multi_select](https://www.php.net/manual/zh/function.curl-multi-select.php) — 等待所有cURL批处理中的活动连接
- [curl_multi_setopt](https://www.php.net/manual/zh/function.curl-multi-setopt.php) — 为 cURL 并行处理设置一个选项
- [curl_multi_strerror](https://www.php.net/manual/zh/function.curl-multi-strerror.php) — 返回字符串描述的错误代码
- [curl_pause](https://www.php.net/manual/zh/function.curl-pause.php) — 暂停和取消暂停一个连接。
- [curl_reset](https://www.php.net/manual/zh/function.curl-reset.php) — 重置一个 libcurl 会话句柄的所有的选项
- [curl_setopt_array](https://www.php.net/manual/zh/function.curl-setopt-array.php) — 为 cURL 传输会话批量设置选项
- [curl_share_close](https://www.php.net/manual/zh/function.curl-share-close.php) — 关闭 cURL 共享句柄
- [curl_share_errno](https://www.php.net/manual/zh/function.curl-share-errno.php) — 返回共享 curl 句柄的最后一次错误号
- [curl_share_init](https://www.php.net/manual/zh/function.curl-share-init.php) — 初始化一个 cURL 共享句柄。
- [curl_share_setopt](https://www.php.net/manual/zh/function.curl-share-setopt.php) — 为 cURL 共享句柄设置选项。
- [curl_share_strerror](https://www.php.net/manual/zh/function.curl-share-strerror.php) — 返回错误号对应的错误消息
- [curl_strerror](https://www.php.net/manual/zh/function.curl-strerror.php) — 返回错误代码的字符串描述
- [curl_unescape](https://www.php.net/manual/zh/function.curl-unescape.php) — 解码给定的 URL 编码的字符串
- [curl_version](https://www.php.net/manual/zh/function.curl-version.php) — 获取 cURL 版本信息



## GET请求

```php
//初始化
$curl = curl_init();
//设置抓取的url
curl_setopt($curl, CURLOPT_URL, 'http://www.baidu.com');
//设置头文件的信息
curl_setopt($curl, CURLOPT_HEADER,0);
//执行成功后不直接输出。
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
//执行命令
$data = curl_exec($curl);
//关闭URL请求
curl_close($curl);
//显示获得的数据
echo($data);
```

## POST请求

```php
//初始化
$curl = curl_init();
//设置抓取的url
curl_setopt($curl, CURLOPT_URL, 'http://www.domain.com');
//设置头文件的信息
curl_setopt($curl, CURLOPT_HEADER, 1);
//执行成功后不直接输出。
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
//设置post方式提交
curl_setopt($curl, CURLOPT_POST, 1);
//设置post数据
$data = array(
    "user" => "admin",
    "pwd" => "admin"
);
curl_setopt($curl, CURLOPT_POSTFIELDS, $post_data);
//执行命令
$data = curl_exec($curl);
//关闭URL请求
curl_close($curl);
//显示获得的数据
echo($data);
```

