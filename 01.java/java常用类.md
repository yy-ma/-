---
title: java常用类
date: 2021/9/10
categories: JAVA

---

## 常用类

### 包装类

> ​		包装类是将基本类型封装到一个类中包含属性和方法，方便对象操作 包装类位于java.lang包中

![image-20210910114032713](/image/java常用类/image-20210910114032713.png)
<!-- more -->
### 包装类和基本类型

- 基本数据类型转换为包装类

```java
Integer intValue = new Integer(21); 
Integer intValue = new Integer("21"); 
Integer intValue = Integer.valueOf("21");
```

- 包装类转换成基本类型

```java
Integer integerId=new Integer(25); 
int intId=integerId.intValue();
```

- 基本类型和包装类的自动转换

```java
Integer intObject = 5; 
int intValue = intObject;
```

### 自动装箱和自动拆箱 (auto-boxing & unboxing)

- 自动装箱

  – 基本类型就自动地封装到与它相同类型的包装中，如：

  – Integer i = 100;

  – 本质上是，编译器编译时为我们添加了：

  – Integer i = Integer.valueOf(100);

- 自动拆箱

  – 包装类对象自动转换成基本类型数据。如：

  – int a = new Integer(100);

  – 本质上，编译器编译时为我们添加了：

  – int a = new Integer(100).intValue();

### 字符串

- 使用String对象存储字符串

```java
String s = "Hello World";
String s = new String();
String s = new String("Hello World");
```

- String类位于java.lang包中，具有丰富的方法

  – 计算字符串的长度、比较字符串、连接字符串、提取字符串

### String

- Java字符串就是Unicode字符序列，例如串“Java”就是4个 Unicode字符J,a,v,a组成的。

- Java允许使用符号"+"把两个字符串连接起来

  – String s1 = “Hello”;String s2 = “World!”;

  – String s = s1 + s2; //HelloWorld!

### String类的常用方法

- char charAt(int index)

  ​	返回字符串中第index个字符。 

- boolean equals(String other) 如果字符串与other相等，返回true

- boolean equalsIgnoreCase(String other) 如果字符串与other相等（忽略大小写），则返回true 

- int indexOf(String str) lastIndexOf(String str,int idx)

- int length() 返回字符串的长度。 

- String replace(char oldChar,char newChar)

  ​	返回一个新串，它是通过用 newChar 替换此字符串中出现的所有oldChar 而生成的

- boolean startsWith(String prefix)

  如果字符串以prefix开始，则返回true

- boolean endsWith(String prefix)

  如果字符串以prefix结尾，则返回true

- String substring(int beginIndex) String substring(int beginIndex,int endIndex)

  返回一个新字符串，该串包含从原始字符串beginIndex到串尾戒endIndex-1的所有字符

- String toLowerCase()

  返回一个新字符串，该串将原始字符串中的所有大写字母改成小写字母

- String toUpperCase()

  返回一个新字符串，该串将原始字符串中的所有小写字母改成大写字母

- String trim()

  返回一个新字符串，该串删除了原始字符串头部和尾部的空格

### 字符串比较

- equals判断字符串值相等，==判断字符串对象引用相等！

```java
public class StringTest3 {

public static void main(String[] args) { String s1 = "abc"; String s2 = "abc"; String s3 = new String("abc"); String s4 = new String("abc"); System.out.println(s1==s2);//true
                                        System.out.println(s1==s3);//false
                                        System.out.println(s3==s4);//false

  

}

}
```

- 内存结构

  ![image-20210910144615836](/image/java常用类/image-20210910144615836.png)

### 字符串连接

- 方法1：使用“+”

- 方法2：使用String类的concat()方法

```java
String s = new String("你好，"); 
String name = new String("张三！"); 
String sentence = s.concat(name); System.out.println(sentence);
```

### 字符串常用提取方法

- 常用提取方法举例

![image-20210910150552292](/image/java常用类/image-20210910150552292.png)

![image-20210910150618459](/image/java常用类/image-20210910150618459.png)

### 字符串拆分

- 有一段歌词，每句都以空格“ ”结尾，请将歌词每句按行输出 

- String 类提供了 split() 方法 ， 将一个字符串分割为子字符串 ， 结 果作为字符串数组返回

### StringBuffer类与StringBuilder类

StringBuffer：String增强版 ，字符串缓冲区，是一个容器

- StringBuffer声明

```java
StringBuffer sb = new StringBuffer(); 
StringBuffer sb = new StringBuffer("aaa");
sb.toString();//转化为String类型
```

- StringBuffer的使用

```java
sb.append("**"); //追加字符串
```

### StringBuffer类

- 利用StringBuffer类的length()和insert ()方法实现需求 

- 将一个数字字符串转换成逗号分隔的数字串，即从右边 开始每三个数字用逗号分隔

![image-20210910150925271](/image/java常用类/image-20210910150925271.png)

```java
public class TestInsert {

public static void main(String[] args) { 
  Scanner input = new Scanner(System.in); System.out.print("请输入一串数字： "); 
  String nums = input.next(); 
  StringBuffer str=new StringBuffer(nums); 
  for(int i=str.length()-3;i>0;i=i-3){ str.insert(i,','); 
                                     } 
  System.out.print(str);

}

}
```

### 字符串选用

- String：不可变字符序列 

- StringBuilder：可变字符序列、效率高、线程不安全 

- StringBuffer：可变字符序列、效率低、线程安全 

- String使用陷阱：

  – string s="a"; //创建了一个字符串 s=s+"b"; //实际上原来的"a"字符串对象已经丢弃了，现在又产生了一个字符串 s+"b"。如果多次执行这些改变串内容的操作，会导致大量副本字符串对象存留在内存中，降低效率。如果这样的操作放到循环中，会极大影响程序的性能。

### 时间处理相关类

![image-20210910151239234](/image/java常用类/image-20210910151239234.png)

### Date时间类( java.util.Date)

- Date类：表示日期和时间 

  提供操作日期和时间各组成部分的方法 

- DateFormat类 与 SimpleDateFormat类

  用于定制日期时间的格式

```java
Date date = new Date(); //创建日期对象 
SimpleDateFormat formater = new SimpleDateFormat("yyyyMM-dd HH:mm:ss");//定制日期格式 
String now = formater.format(date); System.out.println(now);
```

### Calendar

- Calendar类：

  抽象类 用于设置和获取日期/时间数据的特定部分 Calendar类提供一些方法和静态字段来操作日历

![image-20210910151507124](/image/java常用类/image-20210910151507124.png)

### Math类

- 包含了常见的数学运算函数。 

- random()生成[0,1)之间的随机浮点数 

- 生成：0-10之间的任意整数：

  – int a = (int)(10*Math.random());

- 生成：20-30之间的任意整数：

  – int b = 20 + (int)(10*Math.random());

### 枚举

```java
[Modifier] enum enumName{ 
  enumContantName1[， 
  enumConstantName2...[;]] 
    //[field，method] 
}
```

```java
public enum Genders{ 
	Male,Female
-------------------
public class Student{
	public Genders sex;
-------------------
Student stu=new Student(); 
stu.sex=Genders.Male;
```

- 枚举类型

1. 只能够取特定值中的一个

2. 使用enum关键字

3. 所有的枚举类型隐性地继承自 java.lang.Enum。（枚举实质上还是类！ 而每个被枚举的成员实质就是一个枚举类型的实例，他们默认都是publi c static final的。可以直接通过枚举类型名直接使用它们。）

4. 强烈建议当你需要定义一组常量时，使用枚举类型