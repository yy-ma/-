---
title: Java Stream API
date: 2021/9/17
categories: JAVA
---

### Stream

> A sequence of elements supporting sequential and parallel aggregate operations
>
> Stream是一组用来处理数组、集合的API

- Java 8之所以费这么大功夫引入函数式编程，原因有二：

  – 代码简洁函数式编程写出的代码简洁且意图明确，使用stream接口让你从 此告别for循环。

  – 多核友好，Java函数式编程使得编写并行程序从未如此简单，你需要的全部 就是调用一下parallel()方法。

<!-- more -->

### Stream特性

1：不是数据结构，没有内部存储 

2：不支持索引访问 

3：延迟计算 

4：支持并行 

5：很容易生成数组或集合（List，Set） 

6：支持过滤，查找，转换，汇总，聚合等操作

### Stream运行机制

Stream分为 源source，中间操作，终止操作 

流的源可以是一个数组、一个集合、一个生成器方法，一个I/O通 道等等。 

一个流可以有零个和或者多个中间操作，每一个中间操作都会返回 一个新的流，供下一个操作使用。一个流只会有一个终止操作 

Stream只有遇到终止操作，它的源才开始执行遍历操作

### Stream的创建

1、通过数组 

2、通过集合来 

3、通过Stream.generate方法来创建 

4、通过Stream.iterate方法来创建 

5、其他API创建

### Stream常用API

- 中间操作

过滤 filter 

去重 distinct 

排序 sorted 

截取 limit、skip 

转换 map/flatMap 

其他 peek

- 终止操作

循环 forEach 

计算 min、max、count、 average 

匹配 anyMatch、 allMatch、 noneMatch、 findFirst、 findAny 

汇聚 reduce 

收集器 toArray collect