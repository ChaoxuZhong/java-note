#### redis

#####  Q redis 特性有哪些

>1.快，**<u>官方证据在哪里</u>**？
>
>2.can run atomic operations 支持多种原子操作命令
>
>3.内存数据库，能持久化到硬盘



##### Q redis 为什么快？

>1.内存本身快
>
>2.单线程本身不快，避免了并发访问控制和上下文切换至少不会太慢
>
>3.IO 多路复用机制



##### Q redis有哪些数据结构及常见应用

Redis is not a *plain* key-value store, it is actually a *data structures server*

>String  锁，key-value键值存储
>
>Hashes 存储对象
>
>List 消息队列，remember the latest updates posted by users into a social network
>
>Set  主要是集合操作，比如好友列表set，共同好友sinter，是否为好友sismember
>
>Sorted sets 排行榜，和List不同它可以动态排序
>
>Bit arrays
>
>HyperLogLogs
>
>Streams



##### Q redis数据结构和底层数据结构的关系

>String：Simple Dynamic String
>
>Hashes：初始化时使用ZipList，满足条件时升级为HashTable。（条件：当元素大于512个或者某键、值大于64字节）
>
>List：Redis3.2之前，初始化时使用ZipList，满足条件时升级为LinkedList（条件：当元素大于512个，或某个元素大于64字节）
>
>reids3.2之后，变成了QuickList。
>
>Set：初始化时是IntSet，满足条件升级为HashTable（条件：当集合中元素不是整数或集合中元素大于512个）
>
>SortedSet：初始化是ZipList，满足条件升级为SkipList（条件：元素长度大于64字节或元素个数大于128）

<img src="/Users/chaoxu/Documents/Life/note/program/image/redis-data-structure.png" alt="image-20220413162859023"/>

##### Q redis 底层数据结构的特点

SDS Simple Dynamic String:

>1.空间换时间，存储了字符串长度
>
>2.动态扩容，避免溢出，1M一下翻倍扩容，1M以上每次只扩1M
>
>3.空间换时间，空间预分配，空间惰性释放
>
>4.二进制安全 \0截断问题处理

ZipList

>header 头
>
>字节数zlbytes，节点数zllen（提前存储数量）；尾结点偏移量zltail
>
>entries 信息
>
>上一节点长度 pre_entry_length
>
>编码格式 encoding
>
>数据长度 length
>
>数据内容 content

HashTable

拉链法，跟java差不多

IntSet



SkipList



QuickList





##### Q redis AOF（append only file）介绍

How？

AOF写入的是正确执行了的命令，即命令已经执行

实时写、每秒写、操作系统决定什么时候写

TradeOff：实时写还是延时或定时写，决定了保障性能还是保护数据不丢失。

When?

>1.手动执行bgrewriteaof命令时，没有AOF子进程，没有RDB子进程
>
>2.config set appendonly 为 yes时
>
>3.定时轮询变量flag，能执行时执行，该变量由1、2设置

AOF文件日志太大会触发重写。

重写是fork子进程重写，新数据会通过父子进程的管道传递给子进程



##### Q redis RDB (redis database)介绍

对redis中数据进行全量快照

读写并发问题使用cow解决



