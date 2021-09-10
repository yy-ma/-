---
title: java异常处理
date: 2021/9/10
categories: JAVA
---
## 异常

> 异常是指在程序的运行过程中所发生的不正常的事件，它会中断 正在运行的程序
>
> Java编程语言使用异常处理机制为程序提供了错误处理的能力
<!-- more -->
### Java中如何进行异常处理

- Java的异常处理是通过5个关键字来实现的：try、catch、 finally、throw、throws

![image-20210910095942581](/image/java异常处理/image-20210910095942581.png)

- 使用try-catch块捕获异常，分为三种情况：

第一种情况 ：正常

```java
public void method(){

try { 
  // 代码段(此处不会产生异常) } 
catch (异常类型 ex) {
	// 对异常进行处理的代码段 
} 
  // 代码段
}
```

第二种情况：出现异常

```java
public void method(){
  try { 
    // 代码段 1 
    // 产生异常的代码段 2 
    // 代码段 3 
  } catch (异常类型 ex) {
  // 对异常进行处理的代码段4 
  } // 代码段5
}
```

第三种情况：异常类型不匹配

```java
public void method(){
try { 
  // 代码段 1
  // 产生异常的代码段 2 
  // 代码段 3 
} catch (异常类型 ex) {
// 对异常进行处理的代码段4 
}
// 代码段5
}
```

- 调用方法输出异常信息

![image-20210910101930409](/image/java异常处理/image-20210910101930409.png)

### 常见的异常类型

![image-20210910101957549](/image/java异常处理/image-20210910101957549.png)

### try-catch-finally

- 在try-catch块后加入finally块

  – 是否发生异常都执行

  – 不执行的唯一情况

![image-20210910102243113](/image/java异常处理/image-20210910102243113.png)

- 存在return的try-catch-finally块

![image-20210910102434659](/image/java异常处理/image-20210910102434659.png)

### 多重catch块

- 排列catch 语句的顺序：先子类后父类

- 发生异常时按顺序逐个匹配

- 只执行第一个不异常类型匹配的catch语句

```java
public void method(){
try { 
  // 代码段 
  // 产生异常(异常类型2) 
} catch (异常类型1 ex) {
// 对异常进行处理的代码段 
} catch (异常类型2 ex) {
// 对异常进行处理的代码段 
} catch (异常类型3 ex) {
// 对异常进行处理的代码段 
} // 代码段
}
```

### 声明异常

![image-20210910103442767](/image/java异常处理/image-20210910103442767.png)

### 抛出异常

![image-20210910103503921](/image/java异常处理/image-20210910103503921.png)

### 异常的分类

![image-20210910103547402](/image/java异常处理/image-20210910103547402.png)

### 自定义异常

- 当JDK 中的异常类型不能满足程序的需要时，可以自定义异常类 使用自定义异常的步骤

![image-20210910103616894](/image/java异常处理/image-20210910103616894.png)