---
title: java多线程
date: 2021/9/15
categories: JAVA
---

### 线程的概念

▪ 程序:Program,是一个指令的集合 

▪ 进程:Process,(正在执行中的程序)是一个静态的概念

​	 进程是程序的一次静态态执行过程, 占用特定的地址空间. 

​	 每个进程都是独立的，由3部分组成cpu,data,code

​	 缺点：内存的浪费，cpu的负担 
<!-- more -->
▪ 线程:是进程中一个“单一的连续控制流程” (a single sThread,equential flow of control)/执行路径 

​	 线程又被称为轻量级进程(lightweight process)。 

​	 Threads run at the same time, independently of one another  一个迚程可拥有多个并行的(concurrent)线程 

​	 一个迚程中的线程共享相同的内存单元/内存地址空间  可以访问相同的 变量和对象，而且它们从同一堆中分配对象 

​	 通信、数据交换、同步操 作 

​	 由于线程间的通信是在同一地址空间上迚行的，所以不需要额外的通信机制，这就使得通信更简便而且信息传递的速度也更快。

### 进程与线程

![image-20210915154526411](/image/java多线程/image-20210915154526411.png)

### Javac不java

- Java虚拟机启动的时候会有一个迚程java.exe,该迚程中 至少有一个线程，在负责java程序的执行。而且这个线程 运行的代码存在于main方法中,该线程称之为主线程。

- 一个进程中的线程共享代码和数据空间

- 线程结束，迚程未毕结束，但进程结束，线程一定结束 。

- 进程中包含线程，线程是迚程的一部分

### 线程与进程的区别

![image-20210915154706074](/image/java多线程/image-20210915154706074.png)

### JAVA中实现多线程（一）

- 在Java中负责线程的这个功能的是Java.lang.Thread 这个类

- 可以通过创建 Thread 的实例来创建新的线程。

- 每个线程都是通过某个特定Thread对象所对应的方法run( )来完 成其操作的，方法run( )称为线程体。 

- 通过调用Thead类的start()方法来启动一个线程。

### 创建线程的方式一 > 继承Thread类

操作步骤： 

【1】继承Thread类 

【2】重写run方法 

【3】创建对象，调用start()方法 启动线程

```java
public class ThreadDemo01 extends Thread { 
  //重写父为的run方法 
  @Override 
  public void run() { 
    for(int i=0;i<10;i++){ System.out.println("第"+i+"次threadrun........"); } } 
  public static void main(String[] args) { 
    //创建对象,就创建好一个线程 
    ThreadDemo01 d=new ThreadDemo01(); //d.run();//启动线程使用start方法 
    d.start(); 
    for(int i=0;i<5;i++){
      System.out.println("main-->"+i); 
		}
}
}
```

### 线程的执行

![image-20210915155112915](/image/java多线程/image-20210915155112915.png)

### 创建线程的方式二 > 实现Runnable接口

操作步骤： 

【1】实现Runnable接口 

【2】重写run方法 

【3】创建对象，调用start()方法启动线程

```java
public class RunableDemo implements Runnable { @Override 
public void run() { 
  for(int i=0;i<10;i++){ System.out.println("第"+i+"次threadrun........"); } } 
  public static void main(String[] args) { 
    //创建对象,就创建好一个线程 
    RunableDemo rd=new RunableDemo(); 
    Thread t=new Thread(rd); 
    t.start(); 
    for(int i=0;i<5;i++){
      System.out.println("main-->"+i); 
    }
} 
}
```

### JAVA中实现多线程（二）

- 继承Thread类方式的缺点：那就是如果我们的类已经从一个类继 承（如小程序必须继承自 Applet 类），则无法再继承 Thread 类

- 通过Runnable接口实现多线程 

- 优点：可以同时实现继承。实现Runnable接口方式要通用一些。

  1)避免单继承 

  2)方便共享资源 同一份资源 多个代理访问

### 线程状态

![image-20210916170320735](/image/java多线程/image-20210916170320735.png)

- 新生状态

  – 用new关键字建立一个线程后，该线程对象就处亍新生状态。

  – 处于新生状态的线程有自己的内存空间，通过调用start()方法迚入就绪状态。 

- 就绪状态

  – 处于就绪状态线程具备了运行条件，但还没分配到CPU，处亍线程就绪队列，等待系统为其分 配CPU。

  – 当系统选定一个等待执行的线程后，它就会从就绪状态迚入执行状态，该动作称为“CPU调度”。 

- 运行状态

  – 在运行状态的线程执行自己的run方法中代码,直到等待某资源而阻塞戒完成任何而死亡。

  – 如果在给定的时间片内没有执行结束，就会被系统给换下来回到等待执行状态。 

- 阻塞状态

  – 处与运行状态的线程在某些情况下，如执行了sleep(睡眠)方法，戒等待I/O设备等资源，将让 出CPU并暂时停止自己运行，进入阻塞状态。

  – 在阻塞状态的线程丌能迚入就绪队列。只有当引起阻塞的原因消除时，如睡眠时间已到，或等待的I/O设备空闲下来，线程便转入就绪状态，重新到就绪队列中排队等待，被系统选中后从 原来停止的位置开始继续执行。 

- 死亡状态

  – 死亡状态是线程生命周期中的最后一个阶段。线程死亡的原因有三个，一个是正常运行 的线程完成了它的全部工作；另一个是线程被强制性地终止，如通过stop方法来终止一个 线程【不推荐使用】；三是线程抛出未捕获的异常。

### 线程操作的相关方法

![image-20210916170625562](/image/java多线程/image-20210916170625562.png)

### 阻塞状态(sleep/yield/join方法)

- 有三种方法可以暂停Thread执行：

1. sleep： 不会释放锁，Sleep时别的线程也丌可以访问锁定对象。

2. yield:让出CPU的使用权，从运行态直接迚入就绪态。让CPU 重新挑选哪一个线程迚入运行状态。

3. join:当某个线程等待另一个线程执行结束后，才继续执行时， 使调用该方法的线程在此之前执行完毕，也就是等待调用该 方法的线程执行完毕后再往下继续执行

### 线程的同步与死锁

![image-20210916170750385](/image/java多线程/image-20210916170750385.png)

- 同步代码块

```java
public void run() { 
  while(true){ 
    synchronized (this) {//通常将当前对象作为同步对象 
      if (tick>0) { 
        Thread.sleep(10);    System.out.println(Thread.currentThread().getName()+"卖 票:"+tick--);
			}
		}
	}

}
```

### 使用同步解决线程的安全性问题

- 同步的前提

 (1)必须有两个或两个以上的线程 

 (2)必须是多个线程使用同一资源 

 (3)必须保证同步中只能有一个线程在运行

- 将需要同步的代码放到方法中

```java
public void run() { while(true){ sale(); } } 
public synchronized void sale(){ //通常将当前对象作为同步对象 
  if (tick>0) { Thread.sleep(10); System.out.println(Thread.currentThread().getName()+"卖票:"+tick--); } 
}
```

### 线程同步总结

- 同步监视器

  – synchronized(obj){}中的obj称为同步监视器

  – 同步代码块中同步监视器可以是任何对象，但是推荐使用共享资源作为同步监 视器

  – 同步方法中无需指定同步监视器，因为同步方法的监视器是this，也就是该对象 本身 

- 同步监视器的执行过程

  – 第一个线程访问，锁定同步监视器，执行其中代码

  – 第二个线程访问，发现同步监视器被锁定，无法访问

  – 第一个线程访问完毕，解锁同步监视器

  – 第二个线程访问，发现同步监视器未锁，锁定并访问

### 死锁

- 同步可以保证资源共享操作的正确性，但是过多同步也会产生死锁

![image-20210916171246727](/image/java多线程/image-20210916171246727.png)

- 死锁一般情况下表示互相等待，是程序运行时出现的一种问题

### 线程通信

- Java提供了3个方法解决线程之间的通信问题

![image-20210916171345678](/image/java多线程/image-20210916171345678.png)

注意事项：以上方法都只能在同步方法或者同步代码块中使用，否则会抛出异常

### Object 类中的等待不唤醒

![image-20210916171431383](/image/java多线程/image-20210916171431383.png)

### 总结

【1】程序、进程、线程 

【2】线程的创建方式，实现Runnable接口或继承Thread类 

【3】线程状态：创建，新绪，运行，阻塞，消亡 

【4】线程冻结的几种情况

​		该线程对象的wait方法

​		该线程本身调用sleep方法

​		该线程一另一个线程的join在一起 

【5】解冻，使用线程进入阻塞的几种情况

​		该线程对象的nofity唤醒sleep方法，休眠时间到了 

【6】run方法执行结束，线程进入消亡状态 

【7】当多个对象操纵同一共享资源时，要使用同步方法或同步代码块来 进行资源的同步处理 

【8】过多的同步将产生死锁 

【9】生产者与消费者问题（同步，等待与唤醒）
