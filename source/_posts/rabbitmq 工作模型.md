### rabbitmq 工作模型



![image-20210814110251211](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210814110251211.png)



生产者--channel--broker--channel--consumer

broker里面的queue是放在erlang写的Mnesia数据库里面





```
while{

   channel.basicGet();

}

channel.basicPublish(msg);

channel.basicPublish(flag,msg);
```



exchange来路由消息

vhost



### Exchange路由消息详解



#### 直连类型

![image-20210814141557476](C:\Users\admin\Desktop\rabbitmq 工作模型\image-20210814141557476.png)

消息的路由键：routing key

channel.basicPublish(exc_name,"spring","msg1");

exc_name:exchange直连交换机名称

spring：routing key

msg1：消息内容

路由键==绑定建



#### topic主题

*一个单词

#0个或者多个单词

routing key可以带通配符



#### fanout广播

routing key为空

 所有绑定exchange的queue都会收到消息



### rabbitmq的基本使用

1.引入依赖

2.消费者

3.生产者

4.
