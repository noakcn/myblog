---
title: linux启动spring boot项目 redis报cant resolve localhost address
date: 2018-01-19 11:15:05
tags:
- redis
- 异常
categories:
- 笔记
---

### 问题描述

开发环境（win10 64位）启动正常，一旦打包发布的linux测试机上，启动的时候总是有一个错误。

```
2018-01-19 11:08:35.956 [] [localhost-startStop-1] ERROR redis.clients.jedis.HostAndPort - cant resolve localhost address
java.net.UnknownHostException: matrix: matrix: Name or service not known
	at java.net.InetAddress.getLocalHost(InetAddress.java:1505)
	at redis.clients.jedis.HostAndPort.getLocalHostQuietly(HostAndPort.java:105)
	at redis.clients.jedis.HostAndPort.<clinit>(HostAndPort.java:12)
	at redis.clients.jedis.JedisFactory.<init>(JedisFactory.java:37)
	at redis.clients.jedis.JedisPool.<init>(JedisPool.java:185)
	at redis.clients.jedis.JedisPool.<init>(JedisPool.java:169)
	at org.springframework.data.redis.connection.jedis.JedisConnectionFactory.createRedisPool(JedisConnectionFactory.java:275)
	at org.springframework.data.redis.connection.jedis.JedisConnectionFactory.createPool(JedisConnectionFactory.java:250)
	at org.springframework.data.redis.connection.jedis.JedisConnectionFactory.afterPropertiesSet(JedisConnectionFactory.java:237)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeInitMethods(AbstractAutowireCapableBeanFactory.java:1687)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1624)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:555)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:483)
	at org.springframework.beans.factory.support.AbstractBeanFactory$1.getObject(AbstractBeanFactory.java:306)
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:230)
	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:302)
	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:202)
	at org.springframework.beans.factory.config.DependencyDescriptor.resolveCandidate(DependencyDescriptor.java:208)
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.doResolveDependency(DefaultListableBeanFactory.java:1138)
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.resolveDependency(DefaultListableBeanFactory.java:1066)
	at org.springframework.beans.factory.support.ConstructorResolver.resolveAutowiredArgument(ConstructorResolver.java:835)
	at org.springframework.beans.factory.support.ConstructorResolver.createArgumentArray(ConstructorResolver.java:741)
	at org.springframework.beans.factory.support.ConstructorResolver.instantiateUsingFactoryMethod(ConstructorResolver.java:467)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.instantiateUsingFactoryMethod(AbstractAutowireCapableBeanFactory.java:1173)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBeanInstance(AbstractAutowireCapableBeanFactory.java:1067)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:513)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:483)
	at org.springframework.beans.factory.support.AbstractBeanFactory$1.getObject(AbstractBeanFactory.java:306)
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:230)
	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:302)
	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:202)
	at org.springframework.beans.factory.config.DependencyDescriptor.resolveCandidate(DependencyDescriptor.java:208)
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.doResolveDependency(DefaultListableBeanFactory.java:1138)
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.resolveDependency(DefaultListableBeanFactory.java:1066)
	at org.springframework.beans.factory.support.ConstructorResolver.resolveAutowiredArgument(ConstructorResolver.java:835)
	at org.springframework.beans.factory.support.ConstructorResolver.createArgumentArray(ConstructorResolver.java:741)
	at org.springframework.beans.factory.support.ConstructorResolver.instantiateUsingFactoryMethod(ConstructorResolver.java:467)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.instantiateUsingFactoryMethod(AbstractAutowireCapableBeanFactory.java:1173)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBeanInstance(AbstractAutowireCapableBeanFactory.java:1067)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:513)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:483)
	at org.springframework.beans.factory.support.AbstractBeanFactory$1.getObject(AbstractBeanFactory.java:306)
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:230)
	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:302)
	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:202)
	at org.springframework.beans.factory.config.DependencyDescriptor.resolveCandidate(DependencyDescriptor.java:208)
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.doResolveDependency(DefaultListableBeanFactory.java:1138)
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.resolveDependency(DefaultListableBeanFactory.java:1066)
	at org.springframework.beans.factory.support.ConstructorResolver.resolveAutowiredArgument(ConstructorResolver.java:835)
	at org.springframework.beans.factory.support.ConstructorResolver.createArgumentArray(ConstructorResolver.java:741)
	at org.springframework.beans.factory.support.ConstructorResolver.instantiateUsingFactoryMethod(ConstructorResolver.java:467)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.instantiateUsingFactoryMethod(AbstractAutowireCapableBeanFactory.java:1173)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBeanInstance(AbstractAutowireCapableBeanFactory.java:1067)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:513)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:483)
	at org.springframework.beans.factory.support.AbstractBeanFactory$1.getObject(AbstractBeanFactory.java:306)
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:230)
	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:302)
	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:202)
	at org.springframework.boot.web.servlet.ServletContextInitializerBeans.getOrderedBeansOfType(ServletContextInitializerBeans.java:234)
	at org.springframework.boot.web.servlet.ServletContextInitializerBeans.addAsRegistrationBean(ServletContextInitializerBeans.java:182)
	at org.springframework.boot.web.servlet.ServletContextInitializerBeans.addAsRegistrationBean(ServletContextInitializerBeans.java:177)
	at org.springframework.boot.web.servlet.ServletContextInitializerBeans.addAdaptableBeans(ServletContextInitializerBeans.java:159)
	at org.springframework.boot.web.servlet.ServletContextInitializerBeans.<init>(ServletContextInitializerBeans.java:80)
	at org.springframework.boot.context.embedded.EmbeddedWebApplicationContext.getServletContextInitializerBeans(EmbeddedWebApplicationContext.java:241)
	at org.springframework.boot.context.embedded.EmbeddedWebApplicationContext.selfInitialize(EmbeddedWebApplicationContext.java:228)
	at org.springframework.boot.context.embedded.EmbeddedWebApplicationContext.access$000(EmbeddedWebApplicationContext.java:89)
	at org.springframework.boot.context.embedded.EmbeddedWebApplicationContext$1.onStartup(EmbeddedWebApplicationContext.java:213)
	at org.springframework.boot.context.embedded.tomcat.TomcatStarter.onStartup(TomcatStarter.java:55)
	at org.apache.catalina.core.StandardContext.startInternal(StandardContext.java:5196)
	at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:150)
	at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1419)
	at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1409)
	at java.util.concurrent.FutureTask.run(FutureTask.java:266)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
	at java.lang.Thread.run(Thread.java:748)
Caused by: java.net.UnknownHostException: matrix: Name or service not known
	at java.net.Inet6AddressImpl.lookupAllHostAddr(Native Method)
	at java.net.InetAddress$2.lookupAllHostAddr(InetAddress.java:928)
	at java.net.InetAddress.getAddressesFromNameService(InetAddress.java:1323)
	at java.net.InetAddress.getLocalHost(InetAddress.java:1500)
	... 76 common frames omitted

```

### 问题解决

1.先查看linux系统的主机名称

```shell
cat /etc/hosts
[www@matrix logs]$ cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4 shqyh
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6 shqyh

```

2.发现主机名并不在 ，我们需要手动添加主机名到127.0.0.1上

```sh
vim /etc/hosts
[www@matrix wt_matr_platform]$ cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4 shqyh matrix
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6 shqyh

```

3.再次运行该应用，成功运行。并且不再提示上述错误。