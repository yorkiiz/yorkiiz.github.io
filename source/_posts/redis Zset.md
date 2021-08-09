### redis Zset

每个值都有一个分数

![image-20210809203057248](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210809203057248.png)





zset操作指令

zadd myzset 10 java 20 php 30 ruby 40 cpp 50 python

zrange myzset 0 -1 withscores

zrevrange myzset 0 -1 withscores

zrangebyscore myzset 20 30

zrem myzset php cpp 移除

zcard myzset 统计还有多少

zcount myzset 20 60

zcount myzset 20 60

zrank myzset java

zscore myzset java



应用

![image-20210809204202227](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210809204202227.png)

排行榜