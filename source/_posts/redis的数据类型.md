### redis的数据类型

#### 目前官网一共有8中

strings, hashes, lists, sets, sorted sets 

hyperloglogs, geospatial indexes, and streams



字符串

String

int

float

#### 操作指令



#### String

指令

mset yongjie 1234 qingshan 666 EX 10   10秒过期

mset yongjie 1234 qingshan 666 PX 10    10毫秒过期

mset yongjie 1234 qingshan 666 NX 10     不存在才成功

mset yongjie 1234 qingshan 666 XX 10     存在才成功

mget yongjie qingshan

strlen qingshan

append qingshang good

getranger qingshan 0 8

incr qingshan

incrby qingshan 100

decr qingshan

decrby qingshan 100

set f 2.6

incrbyfloat f 7.3

del f

批量赋值可以保证原子性



string应用场景

1.缓存

2.分布式session

3.set NX EX分布式锁

4.incr全局ID

5.incr计数器

6.incr限流

7.位操作统计



#### Hash

| id   | sno   | sname | company |
| ---- | ----- | ----- | ------- |
| 1    | 16666 | 张岩  | 腾讯    |
| 2    | 17777 | 王芳  | 百度    |
| 3    | 18888 | 刘厉  | 阿里    |

mset student:1:sno 1666 student:1:sname 张岩





hash里面value只能存储字符串

hash和string区别：

- 用冒号去分层，减少内存的消耗

- 减少命名的冲突

- 一次取多个，减少资源的消耗

hash是按照key取模去做集群，如果一个key特别大，没办法分流



指令：

hset h1 f 6