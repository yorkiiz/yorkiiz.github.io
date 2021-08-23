### springboot自动装配

#### 1.IOC流程

1.把所有要托管的spring管理的bean拿到，beanDefinition，并且放到beanDefinitionMap

2.bean实例化，进行属性注入

3.初始化Bean，是否实现BeanNameAware

4.是否实现了BeanPostProcessor类，调用postProcessBeforeIn

5.初始化方法

6.是否实现了BeanPostProcessor类，调用postProcessAfterIn。。。。AOP实现





入口在哪里

refresh（）



扫描

1.默认会扫描当前目录及子目录下@Service @Component @Controller @Repository @Bean @Configuration

2.加注解@ComponentScans（{“com.huihui.demo”,"com.huihui.boot"}）,或@Import（ClassB.class）

3.importselector selectimport

4.xml



```。
SpringApplication.run--->refreshContext---refresh---this.finishBeanFactoryInitialization(beanFactory)---eanFactory.preInstantiateSingletons()---getBean---doGetBean---createBean---doCreateBean


    public void refresh() throws BeansException, IllegalStateException {
        synchronized(this.startupShutdownMonitor) {
            this.prepareRefresh();
            ConfigurableListableBeanFactory beanFactory = this.obtainFreshBeanFactory();
            this.prepareBeanFactory(beanFactory);

            try {
                this.postProcessBeanFactory(beanFactory);
                this.invokeBeanFactoryPostProcessors(beanFactory);
                this.registerBeanPostProcessors(beanFactory);
                this.initMessageSource();
                this.initApplicationEventMulticaster();
                this.onRefresh();
                this.registerListeners();
                this.finishBeanFactoryInitialization(beanFactory);//getbean的方法
                this.finishRefresh();
            } catch (BeansException var9) {
                if (this.logger.isWarnEnabled()) {
                    this.logger.warn("Exception encountered during context initialization - cancelling refresh attempt: " + var9);
                }

                this.destroyBeans();
                this.cancelRefresh(var9);
                throw var9;
            } finally {
                this.resetCommonCaches();
            }

        }
    }
```

```
protected Object doCreateBean(String beanName, RootBeanDefinition mbd, @Nullable Object[] args) throws BeanCreationException {
    BeanWrapper instanceWrapper = null;
    if (mbd.isSingleton()) {
        //2.创建实例
        instanceWrapper = (BeanWrapper)this.factoryBeanInstanceCache.remove(beanName);
    }

    if (instanceWrapper == null) {
        instanceWrapper = this.createBeanInstance(beanName, mbd, args);
    }

    Object bean = instanceWrapper.getWrappedInstance();
    Class<?> beanType = instanceWrapper.getWrappedClass();
    if (beanType != NullBean.class) {
        mbd.resolvedTargetType = beanType;
    }

    synchronized(mbd.postProcessingLock) {
        if (!mbd.postProcessed) {
            try {
                this.applyMergedBeanDefinitionPostProcessors(mbd, beanType, beanName);
            } catch (Throwable var17) {
                throw new BeanCreationException(mbd.getResourceDescription(), beanName, "Post-processing of merged bean definition failed", var17);
            }

            mbd.postProcessed = true;
        }
    }

    boolean earlySingletonExposure = mbd.isSingleton() && this.allowCircularReferences && this.isSingletonCurrentlyInCreation(beanName);
    if (earlySingletonExposure) {
        if (this.logger.isTraceEnabled()) {
            this.logger.trace("Eagerly caching bean '" + beanName + "' to allow for resolving potential circular references");
        }

        this.addSingletonFactory(beanName, () -> {
            return this.getEarlyBeanReference(beanName, mbd, bean);
        });
    }

    Object exposedObject = bean;

    try {
        //2.属性注入，DI
        this.populateBean(beanName, mbd, instanceWrapper);
        //3.初始化Bean，是否实现BeanNameAware
        exposedObject = this.initializeBean(beanName, exposedObject, mbd);
    } catch (Throwable var18) {
        if (var18 instanceof BeanCreationException && beanName.equals(((BeanCreationException)var18).getBeanName())) {
            throw (BeanCreationException)var18;
        }

        throw new BeanCreationException(mbd.getResourceDescription(), beanName, "Initialization of bean failed", var18);
    }

    if (earlySingletonExposure) {
        Object earlySingletonReference = this.getSingleton(beanName, false);
        if (earlySingletonReference != null) {
            if (exposedObject == bean) {
                exposedObject = earlySingletonReference;
            } else if (!this.allowRawInjectionDespiteWrapping && this.hasDependentBean(beanName)) {
                String[] dependentBeans = this.getDependentBeans(beanName);
                Set<String> actualDependentBeans = new LinkedHashSet(dependentBeans.length);
                String[] var12 = dependentBeans;
                int var13 = dependentBeans.length;

                for(int var14 = 0; var14 < var13; ++var14) {
                    String dependentBean = var12[var14];
                    if (!this.removeSingletonIfCreatedForTypeCheckOnly(dependentBean)) {
                        actualDependentBeans.add(dependentBean);
                    }
                }

                if (!actualDependentBeans.isEmpty()) {
                    throw new BeanCurrentlyInCreationException(beanName, "Bean with name '" + beanName + "' has been injected into other beans [" + StringUtils.collectionToCommaDelimitedString(actualDependentBeans) + "] in its raw version as part of a circular reference, but has eventually been wrapped. This means that said other beans do not use the final version of the bean. This is often the result of over-eager type matching - consider using 'getBeanNamesForType' with the 'allowEagerInit' flag turned off, for example.");
                }
            }
        }
    }

    try {
        this.registerDisposableBeanIfNecessary(beanName, bean, mbd);
        return exposedObject;
    } catch (BeanDefinitionValidationException var16) {
        throw new BeanCreationException(mbd.getResourceDescription(), beanName, "Invalid destruction signature", var16);
    }
}
```

```
protected Object initializeBean(String beanName, Object bean, @Nullable RootBeanDefinition mbd) {
    if (System.getSecurityManager() != null) {
        AccessController.doPrivileged(() -> {
            //3.初始化Bean，是否实现BeanNameAware
            this.invokeAwareMethods(beanName, bean);
            return null;
        }, this.getAccessControlContext());
    } else {
        this.invokeAwareMethods(beanName, bean);
    }

    Object wrappedBean = bean;
    if (mbd == null || !mbd.isSynthetic()) {
       4.是否实现了BeanPostProcessor类，调用postProcessBeforeIn
        wrappedBean = this.applyBeanPostProcessorsBeforeInitialization(bean, beanName);
    }

    try {
        //5.初始化方法
        this.invokeInitMethods(beanName, wrappedBean, mbd);
    } catch (Throwable var6) {
        throw new BeanCreationException(mbd != null ? mbd.getResourceDescription() : null, beanName, "Invocation of init method failed", var6);
    }

    if (mbd == null || !mbd.isSynthetic()) {
       //6.是否实现了BeanPostProcessor类，调用postProcessAfterIn。。。。AOP实现
        wrappedBean = this.applyBeanPostProcessorsAfterInitialization(wrappedBean, beanName);
    }

    return wrappedBean;
}
```





#### 2.手写start组件

```
@SpringBootApplication->@EnableAutoConfiguration->@Import({AutoConfigurationImportSelector.class})->DeferredImportSelector->ImportSelector->selectImports->this.getAutoConfigurationEntry->this.getCandidateConfigurations-> SpringFactoriesLoader.loadFactoryNames->loadSpringFactories->classLoader.getResources("META-INF/spring.factories")
```

META-INF/spring

![image-20210824013535315](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210824013535315.png)





1.写一个自动装配的类

PersonTest

2.META-INF/spring.factories 添加

```
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.example.start001.start.PersonTest
```

3.pom文件里面build删除，防止maven冲突

4.clean,package,install

5.其他项目引入当前项目生产的maven包

```
<groupId>com.example.start001</groupId>
<artifactId>start</artifactId>
<version>0.0.1-SNAPSHOT</version>
```