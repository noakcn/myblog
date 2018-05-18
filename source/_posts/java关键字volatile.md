---
title: java关键字volatile
date: 2018-05-17 14:22:15
tags:
- java
- 高并发
- CAS
categories:
- 笔记
- 学习
---

### 现象
在java中有这样一个关键字``volatile``，他是JVM提供一种轻量级的同步机制。很多人在使用的时候经常以为用上这个关键词就可以保证多线程下的数据安全。
其实不然。
例如：20条线程每条线程对sum做1w次的累加
```
public class VolatileTest {

    private static volatile int sum;
    private static Logger log = LoggerFactory.getLogger(VolatileTest.class);

    public static void increate() {
        sum++;
    }

    public static void main(String[] args) {

        for (int i = 0; i < 20; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    for (int j = 0; j < 10000; j++) {
                        increate();
                    }
                }
            }).start();

        }
        while (Thread.activeCount() > 1) { //保证前面的线程都执行完
            Thread.yield();
        }

        log.info("sum经过多个线程的累加后结果为 [sum = {}]", sum);
    }


}
```
输出
```
VolatileTest - sum经过多个线程的累加后结果为 [sum = 160353]
```
我们发现，其结果不是我们期望的``200000``，且每次运行结果不同。

那么为什么会这样呢。

### 内存可见性

``volatile``其实只能保证内存可见性，即一个线程对变量的修改，能够及时的被其他线程看到。但JVM仅仅只是保证可见性，不保证原子性。

### 原因

``sum++``我们都知道，其执行实际分为3个步骤
- 1.取值
- 2.将取出来的值+1
- 3.将计算后的值赋值给sum

而``volatile``可以让我们在执行1的时候看到的肯定是最新值，但是在执行2，3的时候，可能sum已经被别的线程更新了，这个时候赋值就不是正确的值了。

### 原理
``volatile``实现内存可见性是通过store和load指令完成的；也就是对``volatile``变量执行写操作时，会在写操作后加入一条store指令，即强迫线程将最新的值刷新到主内存中；而在读操作时，会加入一条load指令，即强迫从主内存中读入变量的值。但``volatile``不保证``volatile``变量的原子性。