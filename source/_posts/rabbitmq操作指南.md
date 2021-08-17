### rabbitmq操作指南





#### 消费者

- 创建工厂（host，port，virtualhost，username，password）
- 创建连接
- 创建channel
- 调用channel

消费者方法：channel.basicConsume(,,)

消费者创建mq配置：channel.exchangeDeclare；channel.queueDeclare；channel.queueBind

```java
//1.创建工厂
ConnectionFactory factory = new ConnectionFactory();
// 连接IP
factory.setHost("192.168.1.128");
// 默认监听端口
factory.setPort(5672);
// 虚拟机
factory.setVirtualHost("/");

// 设置访问的用户
factory.setUsername("admin");
factory.setPassword("admin");
// 2.建立连接
Connection conn = factory.newConnection();
// 3.创建消息通道
Channel channel = conn.createChannel();

        // 创建消费者
        Consumer consumer = new DefaultConsumer(channel) {
            @Override
            public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties,
                                       byte[] body) throws IOException {
                String msg = new String(body, "UTF-8");
                System.out.println("Received message : '" + msg + "'");
                System.out.println("consumerTag : " + consumerTag );
                System.out.println("deliveryTag : " + envelope.getDeliveryTag() );
            }
        };


// 4.开始获取消息
// String queue, boolean autoAck, Consumer callback
channel.basicConsume(QUEUE_NAME, true, consumer);
```





#### 生产者

- 创建工厂
- 创建连接
- 创建通道
- 发送消息

生产者方法：channel.basicpublish(,,)

生产者必须关闭通道和连接

```java
//1.创建工厂
ConnectionFactory factory = new ConnectionFactory();
// 连接IP
factory.setHost("192.168.1.128");
// 连接端口
factory.setPort(5672);
// 虚拟机
factory.setVirtualHost("/");
// 用户
factory.setUsername("admin");
factory.setPassword("admin");

// 2.建立连接
Connection conn = factory.newConnection();
// 3.创建消息通道
Channel channel = conn.createChannel();

// 4.发送消息
String msg = "Hello world, Rabbit MQ";

// String exchange, String routingKey, BasicProperties props, byte[] body
channel.basicPublish(EXCHANGE_NAME, "gupao.best", null, msg.getBytes());

channel.close();
conn.close();
```



#### 队列删除

```
channel.queueDelete
channel.exchangeDelete
```



### 死信队列

![image-20210817010215043](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210817010215043.png)

生产者抛消息给队列，队列没有消息，队列绑定了过期的exchange或者queue，消息里面有设置过期时间，过期后就把消息丢给对应的exchange或者queue

启用插件

rabbitmq-plugins enable rabbitmq_management