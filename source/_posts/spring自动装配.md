### spring自动装配

IOC流程

1.我们要把所有托管给spring管理的bean拿到，beandefination并且放到一个map里面

2.getbean  实例化，进行属性注入，

3.初始化bean，是否实现了beannameaware

4.是否实现了beanpostprocessor类，调用postprocessbefore...

5.初始化方法

6.是否实现了beanpostprocessor类，调用postprocessafter... aop在这里实现



入口在refresh（）里面



#### 扫描

1.默认会扫描当前目录以及子目录下@service @component @controller  @repository





### springboot手写starter



spring.factories