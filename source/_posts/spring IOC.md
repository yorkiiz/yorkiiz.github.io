### spring IOC



#### 核心容器

1.BeanFactory

![](https://raw.githubusercontent.com/yorkiiz/picture/master/20210920174740.png)

工厂的顶层接口，但是只负责生产对象，不负责怎么生产对象。

IOC容器负责具体生产过程。



2.BeanDefinition

bean对象的定义

![image-20210920180524436](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210920180524436.png)

3.BeanDefinitionReader

bean的解析

![](https://raw.githubusercontent.com/yorkiiz/picture/master/20210920182031.png)





#### web IOC初始化流程

| 序号/类名 | DispatcherServlet | FrameworkServlet                         | HttpServletBean | HttpServlet |
| --------- | ----------------- | ---------------------------------------- | --------------- | ----------- |
|           |                   |                                          | init            |             |
|           |                   | initServletBean                          |                 |             |
|           |                   | initWebApplicationContext                |                 |             |
|           |                   | configureAndRefreshWebApplicationContext |                 |             |
|           |                   | refresh                                  |                 |             |
|           | onRefresh         |                                          |                 |             |
|           | initStrategies    |                                          |                 |             |





### 基于xml的IOC容器初始化

IOC容器的初始化包括beandefinition的resource定位，加载和注册三个基本过程

![](https://raw.githubusercontent.com/yorkiiz/picture/master/20210921103448.png)

```
super(parent);   //设置容器资源加载器
this.setConfigLocations(configLocations);//设置bean资源路径定位
 this.refresh();//开始启动
```





#### IOC容器的启动

IOC容器对bean配置资源的载入是从refresh（）函数开始的，refresh是一个模板方法，规定了IOC容器的启动流程，有些逻辑交给子类实现。ClassPathXmlApplicationContext通过调用父类AbstractApplicationContext的refresh方法启动IOC容器对Bean定义的载入过程



作用：IOC容器创建前，如果已经有容器存在，把已经有的容器给销毁，保证refresh之后使用的是新建立起来的IOC容器



#### 容器的创建

```
AbstractApplicationContext中 obtainFreshBeanFactory方法调用子容器的refreshBeanFactory
实际实现是在AbstractRefreshableApplicationContext中
```

先销毁，再载入



#### 载入配置路径

AbstractRefreshableApplicationContext中定义了抽象的loadBeanDefinitions方法，实际实现是其子类AbstractXmlApplicatioContext中对该方法实现，并且调用了loadBeanDefinitions方法载入Bean



#### 分配路径处理策略

loadBeanDefinitions方法对Bean进行加载

![image-20210921163013437](C:\Users\admin\Desktop\spring IOC\image-20210921163013437.png)



#### 解析配置文件路径

XmlBeanDefinitionReader通过调用ClassPathXmlApplicatioinContext的父类DefaultResourceLoader的getResource方法获取加载的资源





#### 开始读取配置内容

XmlBeanDefinitionReader里面的loadBeanDefinitions（Resource...）方法代表bean文件的资源定义以后的载入过程，将Bean配置信息转换成Document对象，该过程有documentLoader方法实现





#### 准备文档对象

DocumentLoader将Bean配置资源转换成Document对象



#### 分配解析策略

xmlBeanDefinitionReader类中的doLoadBeanDefinition方法从特定的XML文件中实际载入Bean配置资源的方法。

Bean配置资源的载入解析分为以下两个过程：

xml解析器将Bean配置信息转换得到Document对象；

完成xml解析后，按照spring Bean的定义规则对Document对象进行解析





#### 将配置载入内存

BeanDefinitionDocumentReader接口通过registerBeanDefinitions方法调用其实现类DefaultBeanDefinitionDocumentReader对Document对象进行解析



#### 载入\<bean>元素

Bean配置信息中的\<import>和\<alias>元素解析在DefaultBeanDefinitionDocumentReader中已经完成，对Bean配置信息中使用最多的\<bean>元素交由BeanDefinitionParserDelegate来解析





#### 载入\<property>元素

BeanDefinitionParserDelegate在解析\<Bean>调用parsePropertyElements方法解析\<Bean>元素中的\<property>属性子元素





#### 载入\<property>子元素





#### 载入\<list>子元素





#### 分配注册策略

DefaultBeanDefinitionDocumentReader对Bean定义转换的Document对象解析的流程中，在其parseDefaultElement方法中完成对Document对象的解析流程中，封装BeanDefinition的BeanDefinitionHold对象，然后调用BeanDefinitionReaderUtils的registerBeanDefinition方法向IOC容器注册解析的Bean，BeanDefinitionReaderUtils的注册的源码如下





#### 向容器注册







### 基于Annotation的IOC初始化



#### 定义

类级别的注解

类内部的注解



#### 定位扫描Bean路径

直接将注解Bean注册到容器中

通过扫描指定的包及其包下的所有类



#### 读取Annotation元数据





### IOC时序图

![](https://raw.githubusercontent.com/yorkiiz/picture/master/%E4%B8%80%E6%AD%A5%E4%B8%80%E6%AD%A5%E6%89%8B%E7%BB%98Spring%20IoC%E8%BF%90%E8%A1%8C%E6%97%B6%E5%BA%8F%E5%9B%BE.jpg)

