## 算法的特征

有穷性

确切性

可行性

输入项

输出项



## 排序

冒泡排序

```php
<?php
    
function bubbling(array $array): array
{
    $count = count($array);
    if ($count <= 1) {
        return $array;
    } else {
        for ($i = 0; $i < $count; $i++) {
            for ($j = 0; $j < $count - $i; $j++) {
                if ($array[$j] < $array[$j + 1]) {
                    $tmp = $array[$j];
                    $array[$j] = $array[$j + 1];
                    $array[$j + 1] = $tmp;
                }
            }
        }
    }
    return $array;
}

```



插入排序



希尔排序

选择排序

快速排序

堆排序

归并排序



## 查找

二分查找

顺序查找





## 时间复杂度



## 空间复杂度