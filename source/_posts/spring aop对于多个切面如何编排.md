---
title: spring aop对于多个切面如何编排
date: 2018-5-18 10:32:16
tags: 
- spring
- aop
categories:
- 笔记
- 原理
---

### 背景

spring aop是个很好用的功能，我们在代码中经常用到的事务注解`@Transaction`就是基于aop实现的。同时，我们也会自己定义一些aop来用。

那么，当一个方法上有多个aop，这些aop的执行顺序是怎么确定的？

### 理论
Spring AOP 采用和 AspectJ 一样的优先顺序来织入增强处理：在进入切入点时，高优先级的增强处理将先被织入；在退出切入点时，高优先级的增强处理会后被织入。

当不同的切面里的两个增强处理需要在同一个切入点被织入时，Spring AOP将以随机的顺序来织入这两个增强处理。

### 实现

要被加AOP的方法
```
@Component
public class MultiAop {

    private Logger log = LoggerFactory.getLogger(getClass());

    public void doSomething() {
        log.info("开始做方法里的事情");
    }
}
```
编写2个切面类(未指定顺序)
```

@Aspect
@Component
public class AspectFirst {

    private Logger log = LoggerFactory.getLogger(getClass());

    @Pointcut("execution(* com.noak..*.*(..))")
    private void pointcutFirst() {
    }

    @Before("pointcutFirst()")
    public void before(JoinPoint point) {
        log.info("执行{}切面的before，未指定顺序", AspectFirst.class.getName());
    }

    @After("pointcutFirst()")
    public void after(JoinPoint point) {
        log.info("执行{}切面的after，未指定顺序", AspectFirst.class.getName());
    }
}


@Aspect
@Component
public class AspectSecond {

    private Logger log = LoggerFactory.getLogger(getClass());

    @Pointcut("execution(* com.noak..*.*(..))")
    private void pointcutSecond() {
    }

    @Before("pointcutSecond()")
    public void before(JoinPoint point) {
        log.info("执行{}切面的before，未指定顺序",AspectSecond.class.getName());
    }

    @After("pointcutSecond()")
    public void after(JoinPoint point) {
        log.info("执行{}切面的after，未指定顺序",AspectSecond.class.getName());
    }
}
```
编写测试类
```
@RunWith(SpringRunner.class)
@SpringBootTest
public class MultiAopTest {

    private Logger log = LoggerFactory.getLogger(getClass());

    @Autowired
    private MultiAop multiAop;

    @Test
    public void test() {
        log.info("开始运行测试类");
        multiAop.doSomething();
        log.info("测试类运行结束");
    }

}
```

输出
```
: 开始运行测试类
: 执行com.noak.myblogexample.part2.aspect.AspectFirst切面的before，未指定顺序
: 执行com.noak.myblogexample.part2.aspect.AspectSecond切面的before，未指定顺序
: 开始做方法里的事情
: 执行com.noak.myblogexample.part2.aspect.AspectSecond切面的after，未指定顺序
: 执行com.noak.myblogexample.part2.aspect.AspectFirst切面的after，未指定顺序
: 测试类运行结束
```

看上去先织入了AspectFirst,然后AspectSecond ，别被名字欺骗咯。

我们改下AspectFirst的名字为ZAspectFirst，再次运行

```
: 开始运行测试类
: 执行com.noak.myblogexample.part2.aspect.AspectSecond切面的before，未指定顺序
: 执行com.noak.myblogexample.part2.aspect.ZAspectFirst切面的before，未指定顺序
: 开始做方法里的事情
: 执行com.noak.myblogexample.part2.aspect.ZAspectFirst切面的after，未指定顺序
: 执行com.noak.myblogexample.part2.aspect.AspectSecond切面的after，未指定顺序
: 测试类运行结束
```

可以发现AspectSecond先别织入，然后是AspectFirst。

由此可以得出，切面在未指定织入顺序的时候，其是随机织入的。并没有特定的顺序。

### 实现带顺序的织入

> Spring提供了如下两种解决方案
> - 切面类实现org.springframework.core.Ordered接口，实现该接口只需实现一个int getOrder( )方法，该方法返回值越小，则优先级越高
> - 直接使用@Order注解来修饰一个切面类，使用 @Order 时可指定一个int型的value属性，该属性值越小，则优先级越高。

修改代码：
```
@Aspect
@Component
@Order(2)
public class AspectFirst {

    private Logger log = LoggerFactory.getLogger(getClass());

    @Pointcut("execution(* com.noak..*.*(..))")
    private void pointcutFirst() {
    }

    @Before("pointcutFirst()")
    public void before(JoinPoint point) {
        log.info("执行{}切面的before，我的顺序是2", AspectFirst.class.getName());
    }

    @After("pointcutFirst()")
    public void after(JoinPoint point) {
        log.info("执行{}切面的after，我的顺序是2", AspectFirst.class.getName());
    }
}


@Aspect
@Component
@Order(1)
public class AspectSecond {

    private Logger log = LoggerFactory.getLogger(getClass());

    @Pointcut("execution(* com.noak..*.*(..))")
    private void pointcutSecond() {
    }

    @Before("pointcutSecond()")
    public void before(JoinPoint point) {
        log.info("执行{}切面的before，我的顺序是1",AspectSecond.class.getName());
    }

    @After("pointcutSecond()")
    public void after(JoinPoint point) {
        log.info("执行{}切面的after，我的顺序是1",AspectSecond.class.getName());
    }
}
```
运行后的结果
```
: 开始运行测试类
: 执行com.noak.myblogexample.part2.aspect.AspectSecond切面的before，我的顺序是1
: 执行com.noak.myblogexample.part2.aspect.AspectFirst切面的before，我的顺序是2
: 开始做方法里的事情
: 执行com.noak.myblogexample.part2.aspect.AspectFirst切面的after，我的顺序是2
: 执行com.noak.myblogexample.part2.aspect.AspectSecond切面的after，我的顺序是1
: 测试类运行结束
```

和第一次运行对比，我们成功的修改了切面织入的顺序。


