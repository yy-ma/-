---
title: java数组
date: 2021/9/8
categories: JAVA

---



### 概述

> 1.一维数组入门
>
> ​	①数组定义、特点、内存分配 
>
> ​	②使用一维数组存储数据
>
> ​	③for-each循环 
>
> 2.一维数组的应用
>
> ​	①查询元素
>
> ​	②数组类型做形参 
>
> ​	③查询最大值最小值 
>
> ​	④添加元素或删除元素
>
> ​	⑤冒泡排序 
>
> ​	⑥Arrays工具类 
>
> ​	⑦理解main（String args[]） 
>
> ​	⑧可变参数
>
> 3.二维数组：二维数组含义、特点、内存分配、举例
<!-- more -->
### 数组概述

- 数组是相同类型数据的有序集合.

  – 相同类型的若干个数据,按照一定先后次序排列组合而成。

  – 其中,每一个数据称作一个数组元素

  – 每个数组元素可以通过一个下标来访问它们.

- 数组特点:

  – 其长度是确定的。数组一旦被创建，它的大小就是不可以改变的。

  – 其元素必须是相同类型,不允许出现混合类型。

  – 数组中的元素可以是任何数据类型，包括基本类型和引用类型。

- 数组属引用类型

  – length, elements of the array

- 数组是一个变量，存储相同数据类型的一组数据

![image-20210908164301017](/image/java数组/image-20210908164301017.png)

- 数组只有一个名称，即标识符

- 元素下标标明了元素在数组中的位置，从0开始

- 数组中的每个元素都可以通过下标来访问

- 数组长度固定不变，避免数组越界

![image-20210908164508793](/image/java数组/image-20210908164508793.png)



### 使用数组

▪ 使用数组四步走：

![image-20210908164633217](/image/java数组/image-20210908164633217.png)

### 声明数组

- 声明数组: 告诉计算机数据类型是什么

![image-20210908164706626](/image/java数组/image-20210908164706626.png)

- 分配空间: 告诉计算机分配几个连续的空间

![image-20210908164827268](/image/java数组/image-20210908164827268.png)

![image-20210908164903395](/image/java数组/image-20210908164903395.png)

### 数组赋值

- 赋值：向分配的格子里放数据

![image-20210908164930738](/image/java数组/image-20210908164930738.png)

- 方法1: 边声明边赋值

  int[ ] score = {89, 79, 76};

  int[ ] score = new int[ ]{89, 79, 76};

- 方法2：动态地从键盘录入信息并赋值

```java
Scanner input = new Scanner(System.in); 
for(int i = 0; i < 30; i ++){ 
	score[i] = input.nextInt(); 
}
```

### 处理数据

#### 使用数组求平均分

![image-20210908165631437](/image/java数组/image-20210908165631437.png)

#### 常见错误

![image-20210908165656514](/image/java数组/image-20210908165656514.png)

![image-20210908165704118](/image/java数组/image-20210908165704118.png)

![image-20210908165716273](/image/java数组/image-20210908165716273.png)

### 一维数组声明

- 一维数组的声明方式有两种：

```java
type[] arr_name;
type arr_name[];
```

- 例如：

```java
int[] intArrays; 
int intArrays[]; 
double[] doubleArrays; 
Person[] pArrays; 
String[] strArrays;
```

### 创建数组

- Java中使用关键字new 创建数组对象 

- 创建基本数据类型一维数组对象演示

```java
public class Test{ 
  public static void main(String args[]){ 
    int[] s = null; // 状态1（下图见）
    s = new int[10]; // 状态2（下图见）
    for ( int i=0; i<10; i++ ) { 
      s[i] =2*i+1; 
      System.out.println(s[i]); 
    } 
  } // 状态3（下图见）
}
```



状态1

![image-20210908170525216](/image/java数组/image-20210908170525216.png)

状态2

![image-20210908170537326](/image/java数组/image-20210908170537326.png)

状态3

![image-20210908170550210](/image/java数组/image-20210908170550210.png)

###  数组初始化

- 动态初始化

- 数组定义与为数组元素分配空间并赋值的操作分开进行

```java
int a[] = null; 
a = new int[3]; 
a[0] = 3; 
a[1] = 9; 
a[2] = 8;
```

- 静态初始化：

- 除了用new关键字来产生数组以外,还可以直接在定义数组的同时 就为数组元素分配空间并赋值。
- 数组名 = {元素1[, 元素2 ……]}; 
- int [] a = {1, 2, 3, 4, 5};

```java
public class Test { 
  public static void main(String args[]) { 
    int [] a = { 3, 5, 7 }; } 
}
```

- 数组是引用类型，它的元素相当于类的实例变量，因此数组一经 分配空间，其中的每个元素也被按照实例变量同样的方式被隐式 初始化。

```java
public class ArrayTest3 {
  public static void main(String args[]) { 
    int a[] = new int[2]; 
    boolean [] b = new boolean[2]; 
    String[] s = new String[2]; 
    for(int i = 0; i < 2; i++)
        System.out.println(a[i]); 
    for(int i = 0; i < 2; i++) 
      System.out.println(b[i]);
    for(int i = 0; i < 2; i++)
      System.out.println(s[i]);
  }
}
```

```java
0 
0 
false
false 
null 
null
```

### 数组的界限

- 定义并用运算符new为之分配空间后，才可以引用数组中的每个元素； ▪数组元素的引用方式：arrayName[index]

  ​	- index为数组元素下标，可以是整型常量或整型表达式。如a[3] , b[i] , c[6*i]; 

  ​	- 数组元素下标从0开始；长度为n的数组合法下标取值范围： 0 ~ n-1；

- 每个数组都有一个属性length指明它的长度，例如：a.length 指明数组a的长度 (元素个数)；

  ​	- 数组的长度: 数组名.length

- 起点和终点

  ​	- 起点: 数组名[0] 

  ​	- 终点: 数组名[length-1]

### 二维数组

- 二维数组举例：

​	`int [][] a = {{1,2},{3,4,0,9},{5,6,7}};`

​	Java中多维数组不必须是规则矩阵形式

![image-20210908171312656](/image/java数组/image-20210908171312656.png)

- 二维数组可以看成以数组为元素的数组。例如：

  `int[][] a= {{1,2},{3,4,5,6},{7,8,9}};`

- Java中多维数组的声明 和初始化应按从高维到 低维的顺序进行，例如：

  ```java
  int [][] a= new int[3][]; 
  a[0] = new int[2]; 
  a[1] = new int[4]; 
  a[2] = new int[3]; 
  int t1[][] = new int[][4]; //非法
  ```

### 二维数组初始化

```java
Ø Declare, create and initiate in the same time ：

int intA[][] = {{1,2},{2,3},{3,4,5}}; 
int intB[3][2] = {{1,2},{2,3},{4,5}};//非法

Ø Declare, create and initiate separately ：

int a[][] = new int[3][5]; 
int b[][] = new int[3][] ; 
b[0] = new int[2]; 
b[1] = new int[3]; 
b[2] = new int[5];
```

### 数组拷贝

```java
Ø 使用java.lang.System类的静态方法

public static void arraycopy (Object src,int srcPos,Object dest, int destPos,int length)

Ø 可以用于数组src从第srcPos项元素开始的length个元素拷贝到目 标数组从destPos项开始的length个位置。
Ø 如果源数据数目超过目标数组边界会抛出 
  IndexOutOfBoundsException 异常。
```

```java
public class ArrayTest7 {

public static void main(String args[]) { 
  String[] s = {"Mircosoft","IBM","Sun","Oracle","Apple"}; 		String[] sBak = new String[6]; 					 System.arraycopy(s,0,sBak,0,s.length); 
  for(int i=0;i<sBak.length;i++){ 
    System.out.print(sBak[i]+" "); 
  } 
  System.out.println(); 
  int[][] intArray = {{1,2},{1,2,3},{3,4}}; 
  int[][] intArrayBak = new int[3][];
  	System.arraycopy(intArray,0,intArrayBak,0,intArray.length); intArrayBak[2][1] = 100; 
  for(int i = 0;i<intArray.length;i++){ for(int j =0;j<intArray[i].length;j++){
    	System.out.print(intArray[i][j]+" "); 
  	} 
		System.out.println(); 
		}
	}
}
```

### 命令行参数

- JAVA应用程序的主方法(程序的入口)

–public static void main (String args[]) {…}

–public static void main (String[] args) {…}

- 命令行参数

–在启动Java应用程序时可以一次性地向应用程序中传递0~多个参数----命令行参数

–命令行参数使用格式：

​	java ClassName lisa "bily" "Mr Brown“ 由参数args接收

–空格将参数分开

–若参数包含空格，用双引号引起来

- 命令行参数用法举例

```java
public class Test {
	public static void main(String[] args) { 
		for ( int i = 0; i < args.length; i++ ) { 
			System.out.println("args[" + i + "] = " + args[i]); 
		}
	}
} 
```

//运行程序 

java Test lisa "bily" "Mr Brown" //输出结果：

//输出结果：

– args[0] = lisa

– args[1] = bily

– args[2] = Mr Brown

### Java.uitl.Arrays

- 该类提供了关于数组操作的API.

  – 打印数组----toString方法。

  – 比较两个数组是否相同----equals方法。

  – 数组排序----sort方法。

  – 数组查找----binarySearch 方法