### rabbit mq连接失败

```java
ConnectionFactory factory = new ConnectionFactory();
// 连接IP
factory.setHost("192.168.1.128");
// 默认监听端口
factory.setPort(15672);
// 虚拟机
factory.setVirtualHost("/");

// 设置访问的用户
factory.setUsername("admin");
factory.setPassword("admin");
// 建立连接
Connection conn = factory.newConnection();
```

```java
"C:\Program Files\java\jdk1.8.0_91\bin\java.exe" "-javaagent:C:\Program Files\JetBrains\IntelliJ IDEA 2019.2.4\lib\idea_rt.jar=54668:C:\Program Files\JetBrains\IntelliJ IDEA 2019.2.4\bin" -Dfile.encoding=UTF-8 -classpath "C:\Program Files\java\jdk1.8.0_91\jre\lib\charsets.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\deploy.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\ext\access-bridge-64.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\ext\cldrdata.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\ext\dnsns.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\ext\jaccess.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\ext\jfxrt.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\ext\localedata.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\ext\nashorn.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\ext\sunec.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\ext\sunjce_provider.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\ext\sunmscapi.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\ext\sunpkcs11.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\ext\zipfs.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\javaws.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\jce.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\jfr.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\jfxswt.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\jsse.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\management-agent.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\plugin.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\resources.jar;C:\Program Files\java\jdk1.8.0_91\jre\lib\rt.jar;D:\study\mq\gupaoedu-vip-rabbitmq-javaapi\target\classes;D:\repository\com\rabbitmq\amqp-client\5.6.0\amqp-client-5.6.0.jar;D:\repository\org\slf4j\slf4j-api\1.7.25\slf4j-api-1.7.25.jar;D:\repository\org\slf4j\slf4j-simple\1.7.25\slf4j-simple-1.7.25.jar" com.gupaoedu.simple.MyConsumer
Exception in thread "main" java.io.IOException
	at com.rabbitmq.client.impl.AMQChannel.wrap(AMQChannel.java:129)
	at com.rabbitmq.client.impl.AMQChannel.wrap(AMQChannel.java:125)
	at com.rabbitmq.client.impl.AMQConnection.start(AMQConnection.java:375)
	at com.rabbitmq.client.impl.recovery.RecoveryAwareAMQConnectionFactory.newConnection(RecoveryAwareAMQConnectionFactory.java:64)
	at com.rabbitmq.client.impl.recovery.AutorecoveringConnection.init(AutorecoveringConnection.java:156)
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:1106)
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:1063)
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:1021)
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:1182)
	at com.gupaoedu.simple.MyConsumer.main(MyConsumer.java:29)
Caused by: com.rabbitmq.client.ShutdownSignalException: connection error
	at com.rabbitmq.utility.ValueOrException.getValue(ValueOrException.java:66)
	at com.rabbitmq.utility.BlockingValueOrException.uninterruptibleGetValue(BlockingValueOrException.java:36)
	at com.rabbitmq.client.impl.AMQChannel$BlockingRpcContinuation.getReply(AMQChannel.java:502)
	at com.rabbitmq.client.impl.AMQConnection.start(AMQConnection.java:317)
	... 7 more
Caused by: java.io.EOFException
	at java.io.DataInputStream.readUnsignedByte(DataInputStream.java:290)
	at com.rabbitmq.client.impl.Frame.readFrom(Frame.java:91)
	at com.rabbitmq.client.impl.SocketFrameHandler.readFrame(SocketFrameHandler.java:164)
	at com.rabbitmq.client.impl.AMQConnection$MainLoop.run(AMQConnection.java:598)
	at java.lang.Thread.run(Thread.java:745)

Process finished with exit code 1
```

#### 代码如1，报错如2

报错原因，rabbit mq的15672为管理端口，使用5672端口即可。

某些情况用15672端口也行