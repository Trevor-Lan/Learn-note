## 数据结构

**双向链表**

```php
class SplDoublyLinkedList implements Iterator, ArrayAccess, Countable, Serializable {
/* 常量 */
const int IT_MODE_LIFO = 2;
const int IT_MODE_FIFO = 0;
const int IT_MODE_DELETE = 1;
const int IT_MODE_KEEP = 0;
/* 方法 */
public add(mixed $index, mixed $newval): void
public bottom(): mixed
public count(): int
public current(): mixed
public getIteratorMode(): int
public isEmpty(): bool
public key(): mixed
public next(): void
public offsetExists(mixed $index): bool
public offsetGet(mixed $index): mixed
public offsetSet(mixed $index, mixed $newval): void
public offsetUnset(mixed $index): void
public pop(): mixed
public prev(): void
public push(mixed $value): void
public rewind(): void
public serialize(): string
public setIteratorMode(int $mode): void
public shift(): mixed
public top(): mixed
public unserialize(string $serialized): void
public unshift(mixed $value): void
public valid(): bool
}
```



**堆栈**

```php
class SplStack extends SplDoublyLinkedList implements Iterator, ArrayAccess, Countable {
/* 方法 */
public __construct()
public setIteratorMode(int $mode): void
/* 继承的方法 */
public SplDoublyLinkedList::add(mixed $index, mixed $newval): void
public SplDoublyLinkedList::bottom(): mixed
public SplDoublyLinkedList::count(): int
public SplDoublyLinkedList::current(): mixed
public SplDoublyLinkedList::getIteratorMode(): int
public SplDoublyLinkedList::isEmpty(): bool
public SplDoublyLinkedList::key(): mixed
public SplDoublyLinkedList::next(): void
public SplDoublyLinkedList::offsetExists(mixed $index): bool
public SplDoublyLinkedList::offsetGet(mixed $index): mixed
public SplDoublyLinkedList::offsetSet(mixed $index, mixed $newval): void
public SplDoublyLinkedList::offsetUnset(mixed $index): void
public SplDoublyLinkedList::pop(): mixed
public SplDoublyLinkedList::prev(): void
public SplDoublyLinkedList::push(mixed $value): void
public SplDoublyLinkedList::rewind(): void
public SplDoublyLinkedList::serialize(): string
public SplDoublyLinkedList::setIteratorMode(int $mode): void
public SplDoublyLinkedList::shift(): mixed
public SplDoublyLinkedList::top(): mixed
public SplDoublyLinkedList::unserialize(string $serialized): void
public SplDoublyLinkedList::unshift(mixed $value): void
public SplDoublyLinkedList::valid(): bool
}
```



**队列**

```php
class SplQueue extends SplDoublyLinkedList implements Iterator, ArrayAccess, Countable {
/* 方法 */
public __construct()
public dequeue(): mixed
public enqueue(mixed $value): void
public setIteratorMode(int $mode): void
/* 继承的方法 */
public SplDoublyLinkedList::add(mixed $index, mixed $newval): void
public SplDoublyLinkedList::bottom(): mixed
public SplDoublyLinkedList::count(): int
public SplDoublyLinkedList::current(): mixed
public SplDoublyLinkedList::getIteratorMode(): int
public SplDoublyLinkedList::isEmpty(): bool
public SplDoublyLinkedList::key(): mixed
public SplDoublyLinkedList::next(): void
public SplDoublyLinkedList::offsetExists(mixed $index): bool
public SplDoublyLinkedList::offsetGet(mixed $index): mixed
public SplDoublyLinkedList::offsetSet(mixed $index, mixed $newval): void
public SplDoublyLinkedList::offsetUnset(mixed $index): void
public SplDoublyLinkedList::pop(): mixed
public SplDoublyLinkedList::prev(): void
public SplDoublyLinkedList::push(mixed $value): void
public SplDoublyLinkedList::rewind(): void
public SplDoublyLinkedList::serialize(): string
public SplDoublyLinkedList::setIteratorMode(int $mode): void
public SplDoublyLinkedList::shift(): mixed
public SplDoublyLinkedList::top(): mixed
public SplDoublyLinkedList::unserialize(string $serialized): void
public SplDoublyLinkedList::unshift(mixed $value): void
public SplDoublyLinkedList::valid(): bool
}
```



更多数据结构：https://www.php.net/manual/zh/spl.datastructures.php

> 堆
>
> 降序堆
>
> 升序堆
>
> 优先级队列
>
> 定长数组
>
> 对象容器



![image-20210731162236699](https://cdn.coder369.com/img/blog/image-20210731162236699.png)

## 迭代器

迭代器：https://www.php.net/manual/zh/spl.iterators.php



## 接口

**Countable**

```php
class Countable {
/* 方法 */
abstract public count(): int
}
```

**OuterIterator**

```php
interface OuterIterator extends Iterator {
/* 方法 */
public getInnerIterator(): Iterator
/* 继承的方法 */
abstract public Iterator::current(): mixed
abstract public Iterator::key(): scalar
abstract public Iterator::next(): void
abstract public Iterator::rewind(): void
abstract public Iterator::valid(): bool
}
```

**RecursiveIterator**

```php
interface RecursiveIterator extends Iterator {
/* 方法 */
public getChildren(): RecursiveIterator
public hasChildren(): bool
/* 继承的方法 */
abstract public Iterator::current(): mixed
abstract public Iterator::key(): scalar
abstract public Iterator::next(): void
abstract public Iterator::rewind(): void
abstract public Iterator::valid(): bool
}
```

**SeekableIterator**

```php
interface SeekableIterator extends Iterator {
/* 方法 */
abstract public seek(int $position): void
/* 继承的方法 */
abstract public Iterator::current(): mixed
abstract public Iterator::key(): scalar
abstract public Iterator::next(): void
abstract public Iterator::rewind(): void
abstract public Iterator::valid(): bool
}
```



## 异常

异常：https://www.php.net/manual/zh/spl.exceptions.php



## 函数

函数：https://www.php.net/manual/zh/ref.spl.php



## 文件处理

**SplFileInfo**

```php
class SplFileInfo {
/* 方法 */
public __construct(string $file_name)
public getATime(): int
public getBasename(string $suffix = ?): string
public getCTime(): int
public getExtension(): string
public getFileInfo(string $class_name = ?): SplFileInfo
public getFilename(): string
public getGroup(): int
public getInode(): int
public getLinkTarget(): string
public getMTime(): int
public getOwner(): int
public getPath(): string
public getPathInfo(string $class_name = ?): SplFileInfo
public getPathname(): string
public getPerms(): int
public getRealPath(): string
public getSize(): int
public getType(): string
public isDir(): bool
public isExecutable(): bool
public isFile(): bool
public isLink(): bool
public isReadable(): bool
public isWritable(): bool
public openFile(string $open_mode = "r", bool $use_include_path = false, resource $context = null): SplFileObject
public setFileClass(string $class_name = "SplFileObject"): void
public setInfoClass(string $class_name = "SplFileInfo"): void
public __toString(): string
}
```

**SplFileObject**

```php
class SplFileObject extends SplFileInfo implements RecursiveIterator, SeekableIterator {
/* 常量 */
const integer DROP_NEW_LINE = 1;
const integer READ_AHEAD = 2;
const integer SKIP_EMPTY = 4;
const integer READ_CSV = 8;
/* 方法 */
public current(): string|array
public eof(): bool
public fflush(): bool
public fgetc(): string
public fgetcsv(string $delimiter = ",", string $enclosure = "\"", string $escape = "\\"): array
public fgets(): string
public fgetss(string $allowable_tags = ?): string
public flock(int $operation, int &$wouldblock = ?): bool
public fpassthru(): int
public fputcsv(
    array $fields,
    string $delimiter = ",",
    string $enclosure = '"',
    string $escape = "\\"
): int|false
public fread(int $length): string|false
public fscanf(string $format, mixed &...$vars): mixed
public fseek(int $offset, int $whence = SEEK_SET): int
public fstat(): array
public ftell(): int
public ftruncate(int $size): bool
public fwrite(string $str, int $length = ?): int
public getChildren(): void
public getCsvControl(): array
public getFlags(): int
public getMaxLineLen(): int
public hasChildren(): bool
public key(): int
public next(): void
public rewind(): void
public seek(int $line_pos): void
public setCsvControl(string $delimiter = ",", string $enclosure = "\"", string $escape = "\\"): void
public setFlags(int $flags): void
public setMaxLineLen(int $max_len): void
public valid(): bool
/* 继承的方法 */
public SplFileInfo::getATime(): int
public SplFileInfo::getBasename(string $suffix = ?): string
public SplFileInfo::getCTime(): int
public SplFileInfo::getExtension(): string
public SplFileInfo::getFileInfo(string $class_name = ?): SplFileInfo
public SplFileInfo::getFilename(): string
public SplFileInfo::getGroup(): int
public SplFileInfo::getInode(): int
public SplFileInfo::getLinkTarget(): string
public SplFileInfo::getMTime(): int
public SplFileInfo::getOwner(): int
public SplFileInfo::getPath(): string
public SplFileInfo::getPathInfo(string $class_name = ?): SplFileInfo
public SplFileInfo::getPathname(): string
public SplFileInfo::getPerms(): int
public SplFileInfo::getRealPath(): string
public SplFileInfo::getSize(): int
public SplFileInfo::getType(): string
public SplFileInfo::isDir(): bool
public SplFileInfo::isExecutable(): bool
public SplFileInfo::isFile(): bool
public SplFileInfo::isLink(): bool
public SplFileInfo::isReadable(): bool
public SplFileInfo::isWritable(): bool
public SplFileInfo::openFile(string $open_mode = "r", bool $use_include_path = false, resource $context = null): SplFileObject
public SplFileInfo::setFileClass(string $class_name = "SplFileObject"): void
public SplFileInfo::setInfoClass(string $class_name = "SplFileInfo"): void
public SplFileInfo::__toString(): string
}
```



## 其它

**ArrayObject**

```php
class ArrayObject implements IteratorAggregate, ArrayAccess, Serializable, Countable {
/* 常量 */
const int STD_PROP_LIST = 1;
const int ARRAY_AS_PROPS = 2;
/* 方法 */
public __construct(mixed $input = array(), int $flags = 0, string $iterator_class = "ArrayIterator")
public append(mixed $value): void
public asort(int $flags = SORT_REGULAR): void
public count(): int
public exchangeArray(mixed $input): array
public getArrayCopy(): array
public getFlags(): int
public getIterator(): ArrayIterator
public getIteratorClass(): string
public ksort(int $flags = SORT_REGULAR): void
public natcasesort(): void
public natsort(): void
public offsetExists(mixed $index): bool
public offsetGet(mixed $index): mixed
public offsetSet(mixed $index, mixed $newval): void
public offsetUnset(mixed $index): void
public serialize(): string
public setFlags(int $flags): void
public setIteratorClass(string $iterator_class): void
public uasort(callable $cmp_function): void
public uksort(callable $cmp_function): void
public unserialize(string $serialized): void
}
```

