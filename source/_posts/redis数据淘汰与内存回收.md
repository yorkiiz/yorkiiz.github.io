### 数据淘汰与内存回收

1.定时过期：到了key的过期时间，立即删除

2.**惰性过期**：key被访问的时候才判断是否过期，过期则删除

3.**定时过期**：每隔一段时间，清除一定数量的过期的key



![image-20210811192730434](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210811192730434.png)

maxmemory 

config set maxmemory 2GB





lru:least recently used

lfu:least frequently used



实现一个lru的算法：

链表+hash

链表里面放元素，放满了就把最后面的元素给删除



redis里面是每个key保持一个时间戳，key更新时从server.lruclock拿取时间

采样的时候就删除一些数据



lfu

基于访问频率实现

![image-20210811195353107](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210811195353107.png)

log-factor越大，计数器增长越慢

lfu-decay-time 一分钟减小1