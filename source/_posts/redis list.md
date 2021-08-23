### redis list

指令：

flushall 删库跑路

lpush queue c

lpush queue d e

rpush queue f g

lpop queue 

rpop queue

lindex queue 0          单个索引获取数据

lrange queue 0 -1     获取所有数据



**特点：**

数据可以重复

简单的消息队列：

rpush lpop

blpop key1 timeput