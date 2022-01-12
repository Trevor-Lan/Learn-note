## 对称加密

**加密**

```php
 openssl_encrypt();
```

```php
openssl_encrypt(
    string $data,
    string $cipher_algo,
    string $passphrase,
    int $options = 0,
    string $iv = "",
    string &$tag = null,
    string $aad = "",
    int $tag_length = 16
): string|false
```

> 注：$cipher_algo为加密算法，可以使用openssl_get_cipher_methods()获取已支持的算法

```php
<?php
declare(strict_types=1);

$data = 'hello';
$cipher_algo = 'AES-256-ECB';
$passphrase = '123456';
echo openssl_encrypt($data,$cipher_algo,$passphrase);
```

加密结果

```
5dVCNTShcEp+/PPuzONnqA==
```

**解密**

```php
 openssl_decrypt();
```

```php
openssl_decrypt(
    string $data,
    string $method,
    string $key,
    int $options = 0,
    string $iv = "",
    string $tag = "",
    string $aad = ""
): string
```

```php
<?php
declare(strict_types=1);

$data = '5dVCNTShcEp+/PPuzONnqA==';
$cipher_algo = 'AES-256-ECB';
$passphrase = '123456';
echo openssl_decrypt('Ei2lhn7i8fzbjO6L8+bh0A==','AES-256-ECB','12345678');
```

解密结果

```
hello
```



## 非对称加密

**创建公钥私钥**

生成RSA私钥文件

```
openssl genrsa -out rsa_private_key.pem 1024
```

将原始 RSA私钥转换为 pkcs8格式

```
openssl pkcs8 -topk8 -inform PEM -in rsa_private_key.pem -outform PEM -nocrypt -out private_key.pem
```

生成RSA公钥 

```
openssl rsa -in rsa_private_key.pem -pubout -out rsa_public_key.pem
```

### 方式1：私钥加密，公钥解密

**私钥加密**

```php
openssl_private_encrypt();
```

```php
openssl_private_encrypt(
    string $data,
    string &$crypted,
    mixed $key,
    int $padding = OPENSSL_PKCS1_PADDING
): bool
```

**公钥解密**

```
openssl_public_decrypt();
```

### 方式2：公钥加密，私钥解密

**公钥加密**

```php
openssl_public_encrypt();
```

**私钥解密**

```
openssl_private_decrypt();
```

