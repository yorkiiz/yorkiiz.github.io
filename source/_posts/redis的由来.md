#### redis的由来

08年 antirez

mysql 优化

09年 C语言 内存型的数据库 redis Remote Dictionary service 远程字典服务

redis的默认端口 6379

意大利 明星 merz 女的





#### redis的特性

1.快，最需要去满足的，内存里面的kv结构 多路复用 单线程 （没有磁盘）

2.持久化，过期，淘汰（内存小，没那么多空间）

3.高可用，集群





keys *

get huihui

set huihui 1

dbsize

ttl huihui1 看多久过期

http://redisdoc.com/sorted_set/index.html



常用数据类型

string ，hash ，list ，sets ，sorted set

geo



key的最大值512MB

value 看内存

setnx lock 1 设置锁

set huihui 1 EX 10 NX 不存在设置成功，存在设置失败

set huihui 1 EX 10 XX 存在设置成功



#### 底层数据编码

int    8字节的长整型

embstr  小于44个字节的字符串

raw   大于44个字节的字符串



#### 应用场景

1.缓存  JSon序列  session（失效）

2.分布式锁

3.自增ID，统计数据



#### redis的常用数据类型以及场景

String

set

get



hash

hset field value

hset  h1 f  6

hget h1 f

hgetall h1



list

rpush queue a

rpush queue b c 

lrange queue 0 -1    cba

lpush queue d e       cbade



有序 消息有序列表

消息队列 不建议做 mq

没有ack  消息结果返回



Jedisutil.getJedisutil().spop()

