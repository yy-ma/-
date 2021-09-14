---
title: javaIO
date: 2021/9/14
categories: JAVA
---
## IO

### 文件

> 相关记录或放在一起的数据的集合

#### JAVA程序如何访问文件属性

```java
File file = new File(pathname);
```

- File类的常用方法

![image-20210914152444830](/image/javaIO/image-20210914152444830.png)
<!-- more -->
### 流的基本概念

> ​		流是指一连串流动的字符,是以先进先出方式发送信息的通道

![image-20210914152532501](/image/javaIO/image-20210914152532501.png)

- 输入/输出流与数据源 
- XXX->程序-->输入流

![image-20210914152630777](/image/javaIO/image-20210914152630777.png)

- 程序->XXX-->输出流

![image-20210914152712730](/image/javaIO/image-20210914152712730.png)

- 数据源

data source. 提供原始数据的原始媒介。常见的：数据库、文件、其他程序、内存、网络连接、IO设备。数据源就像水箱，流就像水管，中流着的水流，程序就是我们最终的用户。 流是一个抽象、动态的概念，是一连串连续动态的数据集合。

- Java流的分类

![image-20210914152944901](/image/javaIO/image-20210914152944901.png)

输入输出流是相对于计算机内存来说的,而不是相对于源和目标

![image-20210914153001590](/image/javaIO/image-20210914153001590.png)

字节流是 8 位通用字节流，字符流是 16 位 Unicode 字符流

- 功能不同

  – 节点流：可以直接从数据源或目的地读写数据。

  – 处理流（包装流）：不直接连接到数据源或目的地，是其他流进行封装。目 的主要是简化操作和提高性能。 

- 节点流和处理流的关系

  – 节点流处于io操作的第一线，所有操作必须通过他们进行

  – 处理流可以对其他流进行处理（提高效率或操作灵活性）

### 文件的读写

- 文本文件的读写

  – 用FileInputStream和FileOutputStream读写文本文件

  – 用BufferedReader和BufferedWriter读写文本文件

- 二进制文件的读写

  – 使用DataInputStream和DataOutputStream读写二进制文件以及 基本数据类型数据的读写

- 对象的读写

  – 使用ObjectInputStream和ObjectOutputStream读写对象(序列 化与反序列化)

### 使用FileInputStream 读文本文件

![image-20210914153555872](/image/javaIO/image-20210914153555872.png)

### 使用FileOutputStream 写文本文件

![image-20210914153639725](/image/javaIO/image-20210914153639725.png)

### 使用字符流读写文件文件

![image-20210914153710266](/image/javaIO/image-20210914153710266.png)

### 使用FileReader读取文件

![image-20210914153746669](/image/javaIO/image-20210914153746669.png)

### BufferedReader类

如何提高字符流读取文本文件的效率？ 

- 使用FileReader类与BufferedReader类

BufferedReader类是Reader类的子类 BufferedReader类带有缓冲区 按行读取内容的readLine()方法（BufferedReader类特有的方法）

### 使用 BufferedReader 读文本文件

![image-20210914153956831](/image/javaIO/image-20210914153956831.png)

- 通过字符流的方式读取文件，并使用缓冲区，提高读文本文件的效率

### 使用FileWriter写文件

![image-20210914154038829](/image/javaIO/image-20210914154038829.png)

### BufferedWriter类

- 如何提高字符流写文本文件的效率？ 

  ​	使用FileWriter类与BufferedWriter类

- BufferedWriter类是Writer类的子类 

- BufferedWriter类带有缓冲区

### 使用 BufferedWriter 写文件

![image-20210914154230144](/image/javaIO/image-20210914154230144.png)

### Reader不Writer的编码方式

- 获得当前开发环境的字符编码方式

- System.out.println(System.getProperty("file.encoding")); 
- 字符流的读写根据需要设置编码方式 
- 涉及到的类:

- 读:FileReader (File file) 
- 写:FileWriter(File file) 
- 加入缓冲区的读:BufferedReader(Reader fr) 
- 加入缓冲区的写:BufferedWriter(Writer bw)

![image-20210914154423104](/image/javaIO/image-20210914154423104.png)

调用顺序与编码顺序相反 ，所以创建类的依次顺序为 FileInputStream InputStreamReader BufferedReader

FileInputStream fis=new FileInputStream(“文件的路径”); 

InputStreamReader isr=new InputStreamReader(fis,”utf-8”); 

BufferedReader br=new BufferedReader(isr);

### 标准的输入输入出流System.in,System.out

- Scanner input=new Scanner(System.in);

![image-20210914154550959](/image/javaIO/image-20210914154550959.png)

### 操作对象的流

- 序列化对象:ObjectOutputStream 

- 反序列化对象:ObjectInputStream 

- 序列化:

  – ObjectOutputStream oos=new ObjectOutputStream(new FileOutputStream("obj.txt"));

  – oos.writeObject(new Person("张三",19));// 序列化

  – oos.close();

- 反序列化:

  – ObjectInputStream ois=new ObjectInputStream(new FileInputStream("obj.txt"));

  – Person p=(Person)ois.readObject();//反序列化

  – System.out.println(p);

### 常见问题

1、类必须实现Serializable接口 

2、给类加个序列化编号，给类定义一个标记，

新的修改后的类还可以操作曾经序列化的对象 

3、静态是丌能被序列化的，

序列化只能对堆中的进行序列化 ，不能对“方

法区”中的进行序列化 

4、不需要序列化的字段前加 transient

### 操作基本数据的流对象DataStream

写入数据

```java
DataOutputStream dos=new DataOutputStream(new FileOutputStream("data.txt")); 
dos.writeInt(234); 
dos.writeBoolean(false); 
dos.writeDouble(9943.00); 
dos.writeUTF("中国");
dos.close();
```

读取数据

```java
DataInputStream dis=new DataInputStream(new FileInputStream("data.txt")); 
int num=dis.readInt(); 
boolean isFind=dis.readBoolean(); 
double price=dis.readDouble(); 
String str=dis.readUTF();
System.out.println(num+"\t"+isFind+"\t"+price+"\t"+str);
```

### 总结

文本操作: FileReader, FileWriter 

字符操作: FileInputStream, FileOutputStream 

基本数据类型操作:DataInputStream, DataOutputStream 

操作对象: ObjectInputStream ,ObjectOutputStream

![image-20210914155005420](/image/javaIO/image-20210914155005420.png)