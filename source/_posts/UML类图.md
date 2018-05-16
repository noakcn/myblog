---
title: UML类图
date: 2017-4-7 15:23:02
tags:
- java
- UML
categories:
- java
- 笔记
---

![](http://om8bq99t5.bkt.clouddn.com/17-4-7/3571155-file_1491549903483_13529.png)

![](http://om8bq99t5.bkt.clouddn.com/17-4-7/18431197-file_1491549915348_6a20.png)

#### 图例详解：

1.类

![](http://om8bq99t5.bkt.clouddn.com/17-4-7/69451581-file_1491550048531_74c5.png)



- 矩形框代表一个类`Class`
- 矩形框分三层
  - 第一层：类的名称，如果是抽象类，则用斜体显示
  - 第二层：类的特性，通常是字段和属性
  - 第三层：类的操作，通常为方法和行为



2.接口

![](http://om8bq99t5.bkt.clouddn.com/17-4-7/60280016-file_1491550242628_836e.png)

- 与类图的区别，顶端有个`<<interface>>`显示。
  - 第一层：接口名称
  - 第二层：接口方法
- 接口还有种棒棒糖表示方法，如图右：唐老鸭类实现了讲人话的接口

3.关系

![](http://om8bq99t5.bkt.clouddn.com/17-4-7/23877699-file_1491550629094_173ee.png)

- 继承关系用空闲三角形+实线来表示

![](http://om8bq99t5.bkt.clouddn.com/17-4-7/67834441-file_1491550804531_dc3d.png)

- 实现接口用空心三角形+虚线来表示

![](http://om8bq99t5.bkt.clouddn.com/17-4-7/86621049-file_1491550892688_12f6b.png)

- 关联关系用用实线箭头来表示，在代码中的表现如下：

```java
public class Penguin extends Bird{
  private Climate climate;//在Penguin（企鹅）中引用了Climate(气候)
}
```

![](http://om8bq99t5.bkt.clouddn.com/17-4-7/61952171-file_1491551309695_6d4d.png)

- 聚合关系用空心菱形+实线箭头
- 大雁是群居动物，每只大雁都属于雁群，一个雁群可以有多只大雁
- 聚合表示一种弱“拥有”关系，体现的是A对象可以包含B对象，但B对象不是A对象的一部分

```java
public class WideGooseAggregate{
  private WideGoose[] wideGooses; //雁群可以有多只大雁
}
```

![](http://om8bq99t5.bkt.clouddn.com/17-4-7/69279359-file_1491551842129_77bc.png)

- 合成关系用实心菱形+实线箭头
- 两端数字`1`,`2`表名这一端可以有几个实例，很显然一个鸟应该有2个翅膀（如果有无数个实例可以用`n`表示
- 合成（组合）是一种强“拥有”关系，体现了严格的部分和整体关系，部分和整体生命周期一样

```java
public class Bird{
  private Wing wing;
  public Bird(){
    wing = new Wing();//在鸟类初始化时，就实例化翅膀
  }
}
```

![](http://om8bq99t5.bkt.clouddn.com/17-4-7/7521905-file_1491553008076_43e2.png)

- 依赖关系，用虚线箭头表示
- 动物依赖氧气，水才能存活

```java
public abstract class Animal{
  public Metabolism(Oxygen oxygen,Water water){
    
  }
}
```



> 编程是一门技术，更加是一门艺术