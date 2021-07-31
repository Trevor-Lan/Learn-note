## cURL函数

1.初始化

```
curl_init()
```

2.设置属性

```
curl_setopt()
```

3.执行并获取结果

```
curl_exec()
```

4.释放句柄

```
curl_close()
```

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

