## 反转字符串

```
strrev(string $string): string
```

```php
<?php
    
function new_strrev(string $str): string
{
    $rev = '';
    if (strlen($str) < 2) {
        $rev = $str;
    } else {
        $rev = '';
        for ($i = strlen($str) - 1; $i >= 0; $i--) {
            $rev .= $str[$i];
        }
    }
    return $rev;
}
```



## 合并数组

```
array_merge(array `$...` = ?): array
```

```php
<?php
    
function new_array_merge(array ...$array): array
{
    $merge = [];
    if (!empty($array)) {
        $merge = $array[0];
        $count = count($array);
        if ($count > 1) {
            for ($i = 1; $i < $count; $i++) {
                foreach ($array[$i] as $item) {
                    $merge[] = $item;
                }
            }
            unset($array);
        }
    }
    return $merge;
}

```

