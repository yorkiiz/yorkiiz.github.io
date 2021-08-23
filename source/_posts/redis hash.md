### redis hash

#### 1.1string来存储多个键值对

String 里面一个值只能对应一个对象

hash里面一个



利用key为冒号分层的效果，达到目的

set food:meat:beaf  1

set food:meat:pork  2

keys food*



String来存储多个键值对

mset批量set

第一级表名：第二级主键的值：第三级字段的名称   字段的内容

key不同导致不好



#### hash来存储对个键值对

hash

key--field--value

**好处：**

1.节省空间-----不用冒号，用聚集

2.减少命名冲突---用一个key

3.减少资源消耗---不用mget，用hget，只用一个key，不用多个key



**坏处：**

1.过期只能对key，不能对field

2.bit位

3.每个field 500M，有500 field，hash里面集群只能对key取模导致不能对单个key分布式



**指令：**

hset h1 f 6

hmset h1 a 1 b 2 c 3 d 4

hget h1 a

hmget h1 a b c d

hkeys h1

hvals h1

hgetall h1

hget exists h1

hdel h1 f

hlen h1

hincrby h1 a 10

hincrby h1 a -10



**购物车：**

key:用户id

field：商品id

value：商品数量

删除 hdel

全选 hgetall

商品数量 hlen