---
title: java网络编程
date: 2021/9/17
categories: JAVA
---

### 网络的概念

- 网络：一组相互连接的计算机

  – 多台计算机组成

  – 使用物理线路进行连接

![image-20210917111609319](/image/java网络编程/image-20210917111609319.png)

<!-- more -->

### 网络编程的三要素

【1】IP地址:唯一标识网络上的每一台计算机两台计算机之间通信的必备要素 

【2】端口号 计算机中应用的标号(代表一个应用程序) 0-1024系统使用或保留端口 ， 有效端口0-65536 

【3】通信协议:通信的规则 TCP,UDP

![image-20210917111719532](/image/java网络编程/image-20210917111719532.png)

### 网络模型一

- OSI参考模式:开放系统互连参考模型（Open System Interconnect）

![image-20210917111902582](/image/java网络编程/image-20210917111902582.png)

- TCP/IP参考模型:传输控制/网际协议 Transfer Controln Protocol/Internet Protocol

![image-20210917112004534](/image/java网络编程/image-20210917112004534.png)

### IP地址的表示方法

- IP 地址：32位，由4个8位二进制数组成 

- IP表示方法：点分十进制

![image-20210917112038731](/image/java网络编程/image-20210917112038731.png)

- IP地址 = 网络ID +主机ID

  – 网络ID：标识计算机或网络设备所在的网段

  – 主机ID：标识特定主机或网络设备

### IP地址的分类

- 地址类用于指定网络 ID 并在网络 ID 和主机 ID 之间提供分隔方 法

- IANA 负责分配 A 、 B 、C 类网络地址， 具体主机地址由机构组织自行分配

![image-20210917112527205](/image/java网络编程/image-20210917112527205.png)

### 特殊的IP地址

- 0.0.0.0：本机 
- 127.0.0.1：本机回环地址，用于本机测试 
- 255.255.255.255：当前子网，一般用于向当前子网广播信息

### IP地址所对应的对象：InetAddress

![image-20210917112630819](/image/java网络编程/image-20210917112630819.png)

![image-20210917112644067](/image/java网络编程/image-20210917112644067.png)

获得百度的主机名

```java
InetAddress ia2=InetAddress.getByName("www.baidu.com"); 
System.out.println("其它主机名称:"+ia2.getHostAddress());
```

### 端口

- 端口:port

 端口是虚拟的概念，并不是说在主机上真的有若干个端口。通过端口，可以在一个主机上运行多个网络应用程序。

### 传输协议

**UDP**:相当于収短信（有字数限制），不需要建立连接， 数据报的大小限制在64k内, 效率较高,不安全，容易丢包 

**TCP**:相当于打电话，需要建立连接， 效率相对比较低，数据传输安全, 三次握手完成。 (点名 > 答到 > 确认)

### Socket套接字

- 网络上的两个程序通过一个双向的通信连接实现数据的交换，

- 这个连接的一端称为一个socket。

- Java中使用Socket完成TCP程序的开収，使用此类可以方便的建立可靠 的、双向的、持续性的、点对点的通讯连接

- 在Socket的程序开収中，服务器端使用ServerSocket等待客户端的连接，

- 对于java的网络程序来讲，每一个客户端都使用一个Socket对象表示

![image-20210917131728728](/image/java网络编程/image-20210917131728728.png)

### 基于TCP协议的Socket编程

- 进行网络通信时，Socket需要借助数据流来完成数据的传递工作

![image-20210917131758426](/image/java网络编程/image-20210917131758426.png)

![image-20210917131838725](/image/java网络编程/image-20210917131838725.png)

```java
// 实现单用户登录
Socket socket=new Socket("localhost",8800);

OutputStream os=socket.getOutputStream();

String info="用户名：Tom;用户密码：123456"; os.write(info.getBytes());
socket.shutdownOutput();

os.close(); 
socket.close();
```

![image-20210917131922700](/image/java网络编程/image-20210917131922700.png)

```java
ServerSocket server=new ServerSocket(8800);

Socket socket=server.accept();

InputStream is=socket.getInputStream(); 
byte[] buf=new byte[1024]; 
int len=is.read(buf); 
syso(new String(buf,0,len)) socket.shutdownInput();

is.close(); 
socket.close(); 
server.close();
```

### Socket中实现对象的传递

```java
String info="用户名：Tom;用户密码：123456"; os.write(info.getBytes());


User user=new User();//User是用户类
user.setLoginName("Tom"); 
user.setPwd("123456"); 
oos.writeObject(user);

```

### 基于UDP的网络编程

![image-20210917132125003](/image/java网络编程/image-20210917132125003.png)

![image-20210917132139738](/image/java网络编程/image-20210917132139738.png)