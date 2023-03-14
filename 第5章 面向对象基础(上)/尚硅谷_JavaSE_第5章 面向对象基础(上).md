# JavaSE_第5章 面向对象基础(上)

## 学习目标

- [ ] 初步了解面向对象的思想
- [ ] 理解类与对象的概念和关系
- [ ] 能够掌握类的定义格式
- [ ] 能够掌握创建对象格式
- [ ] 理解包的作用
- [ ] 掌握包的声明和导入
- [ ] 掌握实例变量的声明和使用
- [ ] 掌握实例方法的声明和调用
- [ ] 理解实例变量与局部变量的区别
- [ ] 理解方法的调用执行机制
- [ ] 理解方法的参数传递机制
- [ ] 掌握方法的可变参数的使用
- [ ] 掌握方法的重载的使用
- [ ] 了解命令行参数
- [ ] 了解方法的递归调用
- [ ] 应用对象数组解决问题
- [ ] 掌握二维数组的声明、初始化、使用

## 5.1 面向对象编程

### 5.1.1 面向对象编程思想概述

#### 1、编程语言概述

Java是一种计算机程序设计语言。所有的计算机程序一直都是围绕着两件事在进行的，程序设计就是用某种语言编写代码来完成这两件事，所以程序设计语言又称为编程语言（编写程序的语言）。

1. 如何表示和存储数据
   - 基本数据类型的常量和变量：表示和存储一个个独立的数据
   - 对象：表示和存储与某个具体事物相关的多个数据（例如：某个学生的姓名、年龄、联系方式等）
   - 数据结构：表示和存储一组对象，数据结构有数组、链表、栈、队列、散列表、二叉树、堆......
2. 基于这些数据都有什么操作行为，其实就是实现什么功能
   - 数据的输入和输出
   - 基于一个或两个数据的操作：赋值运算、算术运算、比较运算、逻辑运算等
   - 基于一组数据的操作：统计分析、查找最大值、查找元素、排序、遍历等

#### 2、程序设计方法

C语言是一种面向过程的程序设计语言，因为C语言是在面向过程思想的指引下去设计、开发计算机程序的。

Java语言是一种面向对象的程序设计语言，因为Java语言是在面向对象思想的指引下去设计、开发计算机程序的。

其中面向对象和面向过程都是一种编程思想，基于不同的思想会产生不同的程序设计方法。

1. 面向过程的程序设计思想（Process-Oriented Programming），简称POP

   - 关注的焦点是过程：过程就是操作数据的步骤，如果某个过程的实现代码在很多地方重复出现，那么就可以把这个过程抽象为一个函数，这样就可以大大简化冗余代码，也便于维护。

   - 代码结构：以函数为组织单位。独立于函数之外的数据称为全局数据，在函数内部的称为局部数据。

     ![](imgs\1111.png)

2. 面向对象的程序设计思想（ Object Oriented Programming），简称OOP

   - 关注的焦点是类：面向对象思想就是在计算机程序设计过程中，参照现实中事物，将事物的属性特征、行为特征抽象出来，用类来表示。某个事物的一个具体个体称为实例或对象。
   
   - 代码结构：以类为组织单位。每种事物都具备自己的**属性**（即表示和存储数据，在类中用成员变量表示）和**行为/功能**（即操作数据，在类中用成员方法表示）。
   
     ![](imgs\111.jpg)

### 5.1.2 类和对象

#### 1、什么是类

**类**是一类具有相同特性的事物的抽象描述，是一组相关**属性**和**行为**的集合。

* **属性**：就是该事物的状态信息。
* **行为**：就是在你这个程序中，该状态信息要做什么操作，或者基于事物的状态能做什么。

#### 2、什么是对象

**对象**是一类事物的一个具体个体（对象并不是找个女朋友）。即对象是类的一个**实例**，必然具备该类事物的属性和行为。

#### 3、类与对象的关系

- 类是对一类事物的描述，是**抽象的**。
- 对象是一类事物的实例，是**具体的**。
- **类是对象的模板，对象是类的实体**。

![](imgs/1.jpg) 

![](imgs\wps1.jpg)

### 5.1.3 如何定义类

#### 1、类的定义格式

关键字：class（小写）

```java
【修饰符】 class 类名{

}
```

类的定义格式举例：

```java
public class Student{
    
}
```

#### 2、对象的创建

关键字：new

```java
new 类名()//也称为匿名对象

//给创建的对象命名
//或者说，把创建的对象用一个引用数据类型的变量保存起来，这样就可以反复使用这个对象了
类名 对象名 = new 类名();
```

那么，对象名中存储的是什么呢？答：对象地址

```java
public class TestStudent{
    public static void main(String[] args){
        System.out.println(new Student());//Student@7852e922

        Student stu = new Student();
        System.out.println(stu);//Student@4e25154f
        
        int[] arr = new int[5];
		System.out.println(arr);//[I@70dea4e
    }
}
```

发现学生对象和数组对象类似，直接打印对象名和数组名都是显示“类型@对象的hashCode值"，所以说类、数组都是引用数据类型，引用数据类型的变量中存储的是对象的地址，或者说指向堆中对象的首地址。

那么像“Student@4e25154f”是对象的地址吗？不是，因为Java是对程序员隐藏内存地址的，不暴露内存地址信息，所以打印对象时不直接显示内存地址，而是JVM帮你调用了对象的toString方法，将对象的基本信息转换为字符串并返回，默认toString方法返回的是“对象的运行时类型@对象的hashCode值的十六进制值”，程序员可以自己改写toString方法的代码（后面会讲如何改写）。

![1561597909862](imgs/1561597909862.png)

## 5.2 包

### 5.2.1 包的作用

（1）可以避免类重名：有了包之后，类的全名称就变为：包.类名

（2）可以控制某些类型或成员的可见范围

如果某个类型或者成员的权限修饰缺省的话，那么就仅限于本包使用。

（3）分类组织管理众多的类

例如：

* java.lang----包含一些Java语言的核心类，如String、Math、Integer、 System和Thread等，提供常用功能
* java.net----包含执行与网络相关的操作的类和接口。
* java.io ----包含能提供多种输入/输出功能的类。
* java.util----包含一些实用工具类，如集合框架类、日期时间、数组工具类Arrays，文本扫描仪Scanner，随机值产生工具Random。
* java.text----包含了一些java格式化相关的类
* java.sql和javax.sql----包含了java进行JDBC数据库编程的相关类/接口
* java.awt和java.swing----包含了构成抽象窗口工具集（abstract window toolkits）的多个类，这些类被用来构建和管理应用程序的图形用户界面(GUI)。

### 5.2.2 如何声明包

关键字：package

```java
package 包名;
```

> 注意：
>
> (1)必须在源文件的代码首行
>
> (2)一个源文件只能有一个声明包的package语句

包的命名规范和习惯：
（1）所有单词都小写，每一个单词之间使用.分割
（2）习惯用公司的域名倒置开头

例如：com.atguigu.xxx;

> 建议大家取包名时不要使用“java.xx"包

### 5.2.3 如何跨包使用类

==注意：==只有public的类才能被跨包使用

（1）使用类型的全名称

例如：java.util.Scanner input = new java.util.Scanner(System.in);

（2）使用import 语句之后，代码中使用简名称

import语句告诉编译器到哪里去寻找类。

import语句的语法格式：

```java
import 包.类名;
import 包.*;
```

> 注意：
>
> 使用java.lang包下的类，不需要import语句，就直接可以使用简名称
>
> import语句必须在package下面，class的上面
>
> 当使用两个不同包的同名类时，例如：java.util.Date和java.sql.Date。一个使用全名称，一个使用简名称

示例代码：

```java
package com.atguigu.test02.pkg;

import com.atguigu.test01.oop.Student;

import java.util.Date;
import java.util.Scanner;

public class TestPackage {
    public static void main(String[] args) {
/*        java.util.Scanner input = new java.util.Scanner(System.in);
        com.atguigu.test01.oop.Student stu = new com.atguigu.test01.oop.Student();*/

        Scanner input = new Scanner(System.in);
        Student student = new Student();

        Date d1 = new Date();
        java.sql.Date d2 = new java.sql.Date(0);
    }
}
```

## 5.3 成员变量

### 5.3.1 如何声明成员变量

```java
【修饰符】 class 类名{
    【修饰符】 数据类型  成员变量名; 
}
```

示例：

```java
public class Person{
	String name;
    char gender;
    int age;
}
```

位置要求：必须在类中，方法外

类型要求：可以是Java的任意类型，包括基本数据类型、引用数据类型（类、接口、数组等）

修饰符：成员变量的修饰符有很多，例如：public、protected、private、static、volatile、transient、final等，后面会一一学习。

其中static可以将成员变量分为两大类，静态变量和非静态变量。其中静态变量又称为类变量，非静态变量又称为实例变量或者属性。==接下来先学习实例变量。==

### 5.3.2 对象的实例变量

#### 1、实例变量的特点

（1）实例变量的值是属于某个对象的

- 必须通过对象才能访问实例变量
- 每个对象的实例变量的值是独立的

（2）实例变量有默认值

| 分类     | 数据类型                       | 默认值   |
| -------- | ------------------------------ | -------- |
| 基本类型 | 整数（byte，short，int，long） | 0        |
|          | 浮点数（float，double）        | 0.0      |
|          | 字符（char）                   | '\u0000' |
|          | 布尔（boolean）                | false    |
|          | 数据类型                       | 默认值   |
| 引用类型 | 数组，类，接口                 | null     |

#### 2、实例变量的访问

```java
对象.实例变量
```

例如：

```java
public class TestPerson {
    public static void main(String[] args) {
        Person p1 = new Person();
        p1.name = "张三";
        p1.age = 23;
        p1.gender = '男';

        Person p2 = new Person();
        /*
        （1）实例变量的值是属于某个对象的
        - 必须通过对象才能访问实例变量
        - 每个对象的实例变量的值是独立的
        （2）实例变量有默认值
         */
        System.out.println("p1对象的实例变量：");
        System.out.println("p1.name = " + p1.name);
        System.out.println("p1.age = " + p1.age);
        System.out.println("p1.gender = " + p1.gender);

        System.out.println("p2对象的实例变量：");
        System.out.println("p2.name = " + p2.name);
        System.out.println("p2.age = " + p2.age);
        System.out.println("p2.gender = " + p2.gender);
    }
}
```

#### 3、实例变量的内存分析

内存是计算机中重要的部件之一，它是与CPU进行沟通的桥梁。其作用是用于暂时存放CPU中的运算数据，以及与硬盘等外部存储器交换的数据。只要计算机在运行中，CPU就会把需要运算的数据调到内存中进行运算，当运算完成后CPU再将结果传送出来。我们编写的程序是存放在硬盘中的，在硬盘中的程序是不会运行的，必须放进内存中才能运行，运行完毕后会清空内存。Java虚拟机要运行程序，必须要对内存进行空间的分配和管理，每一片区域都有特定的处理数据方式和内存管理方式。

JVM的运行时内存区域分为：方法区、堆、虚拟机栈、本地方法栈、程序计数器几大块。

![1561465258546](imgs/1561465258546.png)

| 区域名称   | 作用                                                         |
| ---------- | ------------------------------------------------------------ |
| 程序计数器 | 程序计数器是CPU中的寄存器，它包含每一个线程下一条要执行的指令的地址 |
| 本地方法栈 | 当程序中调用了native的本地方法时，本地方法执行期间的内存区域 |
| 方法区     | 存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。 |
| 堆内存     | 存储对象（包括数组对象），new来创建的，都存储在堆内存。      |
| 虚拟机栈   | 用于存储正在执行的每个Java方法的局部变量表等。局部变量表存放了编译期可知长度的各种基本数据类型、对象引用，方法执行完，自动释放。 |

Java对象保存在内存中时，由以下三部分组成：

- 对象头
  - Mark Word：记录了和当前对象有关锁状信息,GC信息，。（后面再讲）
  - 指向类的指针：每一个对象需要记录它是由哪个类创建出来的，而Java对象的类数据保存在方法区，指向类的指针就是记录创建该对象的类数据在方法区的首地址。该指针在32位JVM中的长度是32bit，在64位JVM中长度是64bit。
  - 数组长度（只有数组对象才有）
- 实例数据
  - 即实例变量的值
- 对齐填充
  - 因为JVM要求Java对象占的内存大小应该是8byte的倍数，如果不满足该大小，则需要补齐至8字节的倍数，没有特别的功能。

![image-20211226153433712](imgs/image-20211226153433712.png)

## 5.4 方法

### 5.4.1 方法的概念

方法也叫函数，是一组代码语句的封装，从而实现代码重用，从而减少冗余代码，通常它是一个独立功能的定义，方法是一个类中最基本的功能单元。

```java
Math.random()的random()方法
Math.sqrt(x)的sqrt(x)方法
System.out.println(x)的println(x)方法

Scanner input = new Scanner(System.in);
input.nextInt()的nextInt()方法
```

### 5.4.2  方法的特点

（1）必须先声明后使用

>  类，变量，方法等都要先声明后使用

（2）不调用不执行，调用一次执行一次。

### 5.4.3 如何声明方法

#### 1、声明方法的位置

声明方法的位置==必须在类中方法外==，即不能在一个方法中直接定义另一个方法。

声明位置示例：

```java
类{
    方法1(){
        
    }
    方法2(){
        
    }
}
```

错误示例：

```java
类{
    方法1(){
        方法2(){  //位置错误
        
   		}
    }
}
```

#### 2、声明方法的语法格式

```java
【修饰符】 返回值类型 方法名(【形参列表 】)【throws 异常列表】{
        方法体的功能代码
}
```

（1）一个完整的方法 = 方法头 + 方法体。

- 方法头就是 【修饰符】 返回值类型 方法名(【形参列表 】)【throws 异常列表】，也称为方法签名，通常调用方法时只需要关注方法头就可以，从方法头可以看出这个方法的功能和调用格式。
- 方法体就是方法被调用后要指定的代码，也是完成方法功能的具体实现代码，对于调用者来说，不了解方法体如何实现的，并影响方法的使用。

（2）方法头可能包含5个部分，但是有些部分是可能缺省的

- 修饰符：可选的。方法的修饰符也有很多，例如：public、protected、private、static、abstract、native、final、synchronized等，后面会一一学习。其中根据是否有static，可以将方法分为静态方法和非静态方法。其中静态方法又称为类方法，非静态方法又称为实例方法。==接下来咱们先学习实例方法==。

返回值类型： 表示方法运行的结果的数据类型，方法执行后将结果返回到调用者
- 基本数据类型
- 引用数据类型
- 无返回值类型：void

方法名：给方法起一个名字，见名知意，能准确代表该方法功能的名字

参数列表：表示完成方法体功能时需要外部提供的数据列表
- 无论是否有参数，()不能省略
- 如果有参数，每一个参数都要指定数据类型和参数名，多个参数之间使用逗号分隔，例如：
  - 一个参数： (数据类型  参数名)
  - 二个参数： (数据类型1  参数1,  数据类型2  参数2) 
- 参数的类型可以是基本数据类型、引用数据类型

- throws 异常列表：可选，在异常章节再讲

（3）方法体：方法体必须有{}括起来，在{}中编写完成方法功能的代码

关于方法体中return语句的说明：

- return语句的作用是结束方法的执行，并将方法的结果返回去

- 如果返回值类型不是void，方法体中必须保证一定有 return 返回值; 语句，并且要求该返回值结果的类型与声明的返回值类型一致或兼容。
- 如果返回值类型为void时，方法体中可以没有return语句，如果要用return语句提前结束方法的执行，那么return后面不能跟返回值，直接写return ; 就可以。
- return语句后面就不能再写其他代码了，否则会报错：Unreachable code

示例：

```java
/**
 * 方法定义案例演示
 */
public class MethodDefineDemo {
    /**
     * 无参无返回值方法的演示
     */
    void sayHello(){
        System.out.println("hello");
    }

    /**
     * 有参无返回值方法的演示
     * @param length int 第一个参数，表示矩形的长
     * @param width int 第二个参数，表示矩形的宽
     * @param sign char 第三个参数，表示填充矩形图形的符号
     */
    void printRectangle(int length, int width, char sign){
        for (int i = 1; i <= length ; i++) {
            for(int j=1; j <= width; j++){
                System.out.print(sign);
            }
            System.out.println();
        }
    }

    /**
     * 无参有返回值方法的演示
     * @return
     */
    int getIntBetweenOneToHundred(){
        return (int)(Math.random()*100+1);
    }
    
    /**
     * 有参有返回值方法的演示
     * @param a int 第一个参数，要比较大小的整数之一
     * @param b int 第二个参数，要比较大小的整数之二
     * @return int 比较大小的两个整数中较大者的值
     */
    int max(int a, int b){
        return a > b ? a : b;
    }
}

```

### 5.4.4 如何调用实例方法

#### 1、方法调用语法格式

```java
对象.非静态方法(实参列表)
```

例如：

```java
/**
 * 方法调用案例演示
 */
public class MethodInvokeDemo {
    public static void main(String[] args) {
        //创建对象
        MethodDefineDemo md = new MethodDefineDemo();

        System.out.println("-----------------------方法调用演示-------------------------");

        //调用MethodDefineDemo类中无参无返回值的方法sayHello
        md.sayHello();
        md.sayHello();
        md.sayHello();
        //调用一次，执行一次，不调用不执行

        System.out.println("------------------------------------------------");
        //调用MethodDefineDemo类中有参无返回值的方法printRectangle
        md.printRectangle(5,10,'@');

        System.out.println("------------------------------------------------");
        //调用MethodDefineDemo类中无参有返回值的方法getIntBetweenOneToHundred
        md.getIntBetweenOneToHundred();//语法没问题，就是结果丢失

        int num = md.getIntBetweenOneToHundred();
        System.out.println("num = " + num);

        System.out.println(md.getIntBetweenOneToHundred());
        //上面的代码调用了getIntBetweenOneToHundred三次，这个方法执行了三次

        System.out.println("------------------------------------------------");
        //调用MethodDefineDemo类中有参有返回值的方法max
        md.max(3,6);//语法没问题，就是结果丢失
        
        int bigger = md.max(5,6);
        System.out.println("bigger = " + bigger);

        System.out.println("8,3中较大者是：" + md.max(8,9));
    }
}

```

回忆之前的代码：

```java
//1、创建Scanner的对象
Scanner input = new Scanner(System.in);//System.in默认代表键盘输入

//2、提示输入xx
System.out.print("请输入一个整数："); //对象.非静态方法(实参列表)

//3、接收输入内容
int num = input.nextInt();  //对象.非静态方法()
```

#### 2、形参和实参

* 形参（formal parameter）：在定义方法时方法名后面括号中声明的变量称为形式参数（简称形参）即形参出现在方法定义时。
* 实参（actual parameter）：调用方法时方法名后面括号中的使用的值/变量/表达式称为实际参数（简称实参）即实参出现在方法调用时。
* 调用时，实参的个数、类型、顺序顺序要与形参列表一一对应。如果方法没有形参，就不需要也不能传实参。
* 无论是否有参数，声明方法和调用方法是==()都不能丢失==

#### 3、返回值问题

方法调用表达式是一个特殊的表达式：

- 如果被调用方法的返回值类型是void，调用时不需要也不能接收和处理（打印或参与计算）返回值结果，即方法调用表达式==只能==直接加;成为一个独立语句。
- 如果被调用方法有返回值，即返回值类型不是void，
  - 方法调用表达式的结果可以作为赋值表达式的值，
  - 方法调用表达式的结果可以作为计算表达式的一个操作数，
  - 方法调用表达式的结果可以作为另一次方法调用的实参，
  - 方法调用表达式的结果可以不接收和处理，方法调用表达式直接加;成为一个独立的语句，这种情况，返回值丢失。

```java
public class MethodReturnValue {
    public static void main(String[] args) {
        //创建对象
        MethodDefineDemo md = new MethodDefineDemo();

        //无返回值的都只能单独加;成一个独立语句
        //调用MethodDefineDemo类中无参无返回值的方法sayHello
        md.sayHello();
        //调用MethodDefineDemo类中有参无返回值的方法printRectangle
        md.printRectangle(5,10,'@');

        //有返回值的
        //(1)方法调用表达式可以作为赋值表达式的值
        int bigger = md.max(7,3);
        System.out.println("bigger = " + bigger);

        //(2)方法调用表达式可以作为计算表达式的一个操作数
        //随机产生两个[1,100]之间的整数，并求和
        int sum = md.getIntBetweenOneToHundred() + md.getIntBetweenOneToHundred();
        System.out.println("sum = " + sum);

        //(3)方法调用表达式可以作为另一次方法调用的实参
        int x = 4;
        int y = 5;
        int z = 2;
        int biggest = md.max(md.max(x,y),z);
        System.out.println("biggest = " + biggest);

        //(4)方法调用表达式直接加;成为一个独立的语句，这种情况，返回值丢失
        md.getIntBetweenOneToHundred();
    }
}
```

### 5.4.5 实例方法使用当前对象的成员

在实例方法中还可以使用当前对象的其他成员。在Java中当前对象用this表示。

- this：在实例方法中，表示调用该方法的对象

- 如果没有歧义，完全可以省略this。

#### 1、使用this.

案例：矩形类

```java
public class Rectangle {
    int length;
    int width;

    int area() {
        return this.length * this.width;
    }

    int perimeter(){
        return 2 * (this.length + this.width);
    }

    void print(char sign) {
        for (int i = 1; i <= this.width; i++) {
            for (int j = 1; j <= this.length; j++) {
                System.out.print(sign);
            }
            System.out.println();
        }
    }

    String getInfo(){
        return "长：" + this.length + "，宽：" + this.width +"，面积：" + this.area() +"，周长：" + this.perimeter();
    }
}
```

测试类

```java
public class TestRectangle {
    public static void main(String[] args) {
        Rectangle r1 = new Rectangle();
        Rectangle r2 = new Rectangle();

        System.out.println("r1对象：" + r1.getInfo());
        System.out.println("r2对象：" + r2.getInfo());

        r1.length = 10;
        r1.width = 2;
        System.out.println("r1对象：" + r1.getInfo());
        System.out.println("r2对象：" + r2.getInfo());

        r1.print('#');
        System.out.println("---------------------");
        r1.print('&');

        System.out.println("---------------------");
        r2.print('#');
        System.out.println("---------------------");
        r2.print('%');
    }
}
```

#### 2、省略this.

```java
public class Rectangle {
    int length;
    int width;

    int area() {
        return length * width;
    }

    int perimeter(){
        return 2 * (length + width);
    }

    void print(char sign) {
        for (int i = 1; i <= width; i++) {
            for (int j = 1; j <= length; j++) {
                System.out.print(sign);
            }
            System.out.println();
        }
    }

    String getInfo(){
        return "长：" + length + "，宽：" + width +"，面积：" + area() +"，周长：" + perimeter();
    }
}
```

### 5.4.6 方法调用内存分析

方法不调用不执行，调用一次执行一次，每次调用会在栈中有一个入栈动作，即给当前方法开辟一块独立的内存区域，用于存储当前方法的局部变量的值，当方法执行结束后，会释放该内存，称为出栈，如果方法有返回值，就会把结果返回调用处，如果没有返回值，就直接结束，回到调用处继续执行下一条指令。

栈结构：先进后出，后进先出。

```java
public class MethodMemory {
    public static void main(String[] args) {
        Rectangle r1 = new Rectangle();
        Rectangle r2 = new Rectangle();
        r1.length = 10;
        r1.width = 2;
        r1.print('#');
        System.out.println("r1对象：" + r1.getInfo());
        System.out.println("r2对象：" + r2.getInfo());
    }
}
```

![image-20211228115855484](imgs/image-20211228115855484.png)

### 5.4.7 实例变量与局部变量的区别

1、声明位置和方式
（1）实例变量：在类中方法外
（2）局部变量：在方法体{}中或方法的形参列表、代码块中

2、在内存中存储的位置不同
（1）实例变量：堆
（2）局部变量：栈

3、生命周期
（1）实例变量：和对象的生命周期一样，随着对象的创建而存在，随着对象被GC回收而消亡，
			而且每一个对象的实例变量是独立的。
（2）局部变量：和方法调用的生命周期一样，每一次方法被调用而在存在，随着方法执行的结束而消亡，
			而且每一次方法调用都是独立。

4、作用域
（1）实例变量：通过对象就可以使用，本类中“this.，没有歧义还可以省略this.”，其他类中“对象.”
（2）局部变量：出了作用域就不能使用

5、修饰符（后面来讲）
（1）实例变量：public,protected,private,final,volatile,transient等
（2）局部变量：final

6、默认值
（1）实例变量：有默认值
（2）局部变量：没有，必须手动初始化。其中的形参比较特殊，靠实参给它初始化。

## 5.5 参数问题

### 5.5.1 特殊参数之一：可变参数

在**JDK1.5**之后，当定义一个方法时，形参的类型可以确定，但是形参的个数不确定，那么可以考虑使用可变参数。可变参数的格式：

```
【修饰符】 返回值类型 方法名(【非可变参数部分的形参列表,】参数类型... 形参名){  }
```

可变参数的特点和要求：

（1）一个方法最多只能有一个可变参数

（2）如果一个方法包含可变参数，那么可变参数必须是形参列表的最后一个

（3）在声明它的方法中，可变参数当成数组使用

（4）其实这个书写“≈”

```
【修饰符】 返回值类型 方法名(【非可变参数部分的形参列表,】参数类型[] 形参名){  }
```

只是后面这种定义，在调用时必须传递数组，而前者更灵活，既可以传递数组，又可以直接传递数组的元素，这样更灵活了。

#### 1、方法只有可变参数

案例：求n个整数的和

```java
public class NumberTools {
    int total(int[] nums){
        int he = 0;
        for (int i = 0; i < nums.length; i++) {
            he += nums[i];
        }
        return he;
    }

    int sum(int... nums){
        int he = 0;
        for (int i = 0; i < nums.length; i++) {
            he += nums[i];
        }
        return he;
    }
}
```

```java
public class TestVarParam {
    public static void main(String[] args) {
        NumberTools tools = new NumberTools();

        System.out.println(tools.sum());//0个实参
        System.out.println(tools.sum(5));//1个实参
        System.out.println(tools.sum(5,6,2,4));//4个实参
        System.out.println(tools.sum(new int[]{5,6,2,4}));//传入数组实参

        System.out.println("------------------------------------");
        System.out.println(tools.total(new int[]{}));//0个元素的数组
        System.out.println(tools.total(new int[]{5}));//1个元素的数组
        System.out.println(tools.total(new int[]{5,6,2,4}));//传入数组实参
    }
}
```

#### 2、方法包含非可变参数和可变参数

- 非可变参数部分必须传入对应类型和个数的实参；
- 可变参数部分按照可变参数的规则传入0~n个对应类型的实参或传入1个对应类型的数组实参；

案例：

n个字符串进行拼接，每一个字符串之间使用某字符进行分割，如果没有传入字符串，那么返回空字符串""

```java
public class StringTools {
    String concat(char seperator, String... args){
        String str = "";
        for (int i = 0; i < args.length; i++) {
            if(i==0){
                str += args[i];
            }else{
                str += seperator + args[i];
            }
        }
        return str;
    }
}
```

```java
public class StringToolsTest {
    public static void main(String[] args) {
        StringTools tools = new StringTools();

        System.out.println(tools.concat('-'));
        System.out.println(tools.concat('-',"hello"));
        System.out.println(tools.concat('-',"hello","world"));
        System.out.println(tools.concat('-',"hello","world","java"));
    }
}
```

### 5.5.2 方法的参数传递机制

方法的参数传递机制：实参给形参赋值，那么反过来形参会影响实参吗？

* 方法的形参是基本数据类型时，形参值的改变不会影响实参；
* 方法的形参是引用数据类型时，形参地址值的改变不会影响实参，但是形参地址值里面的数据的改变会影响实参，例如，修改数组元素的值，或修改对象的属性值。
  * 注意：String、Integer等特殊类型容易错

#### 1、形参是基本数据类型

案例：编写方法，交换两个整型变量的值

```java
public class PrimitiveTypeParam {
    void swap(int a, int b){//交换两个形参的值
        int temp = a;
        a = b;
        b = temp;
    }

    public static void main(String[] args) {
        PrimitiveTypeParam tools = new PrimitiveTypeParam();
        int x = 1;
        int y = 2;
        System.out.println("交换之前：x = " + x +",y = " + y);//1,2
        tools.swap(x,y);//实参x,y是基本数据类型，给形参的是数据的“副本”，调用完之后，x与y的值不变
        System.out.println("交换之后：x = " + x +",y = " + y);//1,2
    }
}
```

#### 2、形参是引用数据类型

```java
public class ReferenceTypeParam {
    void swap(MyData my){//形参my是引用数据类型，接收的是对象的地址值，形参my和实参data指向同一个对象
        //里面交换了对象的两个实例变量的值
        int temp = my.x;
        my.x = my.y;
        my.y = temp;
    }

    public static void main(String[] args) {
        ReferenceTypeParam tools = new ReferenceTypeParam();
        MyData data = new MyData();
        data.x = 1;
        data.y = 2;
        System.out.println("交换之前：x = " + data.x +",y = " + data.y);//1,2
        tools.swap(data);//实参是data，给形参my的是对象的地址值，调用完之后，x与y的值交换
        System.out.println("交换之后：x = " + data.x +",y = " + data.y);//2,1
    }

}
```

```java
public class MyData{
    int x;
    int y;
}
```

#### 3、形参是数组

```java
public class ArrayTypeParam {
    void sort(int[] arr){//给数组排序，修改了数组元素的顺序，这里对arr数组进行排序，就相当于对nums数组进行排序
        for (int i = 1; i < arr.length; i++) {
            for (int j = 0; j < arr.length - i; j++) {
                if(arr[j] > arr[j+1]){
                    int temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
        }
    }

    void iterate(int[] arr){//输出数组的元素，元素之间使用空格分隔，元素打印完之后换行
        					//这个方法没有修改元素的值
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i]+" ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        ArrayTypeParam tools = new ArrayTypeParam();

        int[] nums = {4,3,1,6,7};
        System.out.println("排序之前：");
        tools.iterate(nums);//实参nums把数组的首地址给形参arr，这个调用相当于输出nums数组的元素
        					//对数组的元素值没有影响

        tools.sort(nums);//对nums数组进行排序

        System.out.println("排序之后：");
        tools.iterate(nums);//输出nums数组的元素
        //上面的代码，从头到尾，堆中只有一个数组，没有产生新数组，无论是排序还是遍历输出都是同一个数组
    }
}
```

#### 4、形参指向新对象

```java
public class AssignNewObjectToFormalParam {
    void swap(MyData my){
        my = new MyData(); //这里让my形参指向了新对象，此时堆中有两个MyData对象，和main中的data对象无关
        int temp = my.x;
        my.x = my.y;
        my.y = temp;
     
    }

    public static void main(String[] args) {
        //创建这个对象的目的是为了调用swap方法
        AssignNewObjectToFormalParam tools = new AssignNewObjectToFormalParam();
        
        MyData data = new MyData();
        data.x = 1;
        data.y = 2;
        System.out.println("交换之前：x = " + data.x +",y = " + data.y);//1,2
        tools.swap(data);//调用完之后，x与y的值交换？
        System.out.println("交换之后：x = " + data.x +",y = " + data.y);//1,2
    }
}
```

## 5.6 方法的重载

- **方法重载**：指在同一个类中，允许存在一个以上的同名方法，只要它们的参数列表不同即可，与修饰符和返回值类型无关。
- 参数列表：数据类型个数不同，数据类型不同（按理来说数据类型顺序不同也可以，但是很少见，也不推荐，逻辑上容易有歧义）。
- 重载方法调用：JVM通过方法的参数列表，调用匹配的方法。
  - 先找个数、类型最匹配的
  - 再找个数和类型可以兼容的，如果同时多个方法可以兼容将会报错

案例，用重载实现：

（1）定义方法求两个整数的最大值

（2）定义方法求三个整数的最大值

（3）定义方法求两个小数的最大值

（4）定义方法求n个整数最大值

```java
public class MathTools {
    //求两个整数的最大值
    public int max(int a,int b){
        return a>b?a:b;
    }

    //求两个小数的最大值
    public double max(double a, double b){
        return a>b?a:b;
    }

    //求三个整数的最大值
    public int max(int a, int b, int c){
        return max(max(a,b),c);
    }

    //求n整数的最大值
    public int max(int... nums){
        int max = nums[0];//如果没有传入整数，或者传入null，这句代码会报异常
        for (int i = 1; i < nums.length; i++) {
            if(nums[i] > max){
                max = nums[i];
            }
        }
        return max;
    }
}
```

### 1、找最匹配的

```java
public class MethodOverloadMosthMatch {
    public static void main(String[] args) {
        MathTools tools = new MathTools();

        System.out.println(tools.max(5,3));
        System.out.println(tools.max(5,3,8));
        System.out.println(tools.max(5.7,2.5));
    }
}
```

### 2、找唯一可以兼容的

```java
public class MethodOverloadMostCompatible {
    public static void main(String[] args) {
        MathTools tools = new MathTools();

        System.out.println(tools.max(5.7,9));
        System.out.println(tools.max(5,6,8,3));
//        System.out.println(tools.max(5.7,9.2,6.9)); //没有兼容的
    }
}
```

### 3、多个方法可以匹配或兼容

```java
package com.atguigu.test06.overload;

public class MathTools {
    //求两个整数的最大值
    public int max(int a,int b){
        return a>b?a:b;
    }

    //求两个小数的最大值
    public double max(double a, double b){
        return a>b?a:b;
    }

    //求三个整数的最大值
    public int max(int a, int b, int c){
        return max(max(a,b),c);
    }

    //求n整数的最大值
    public int max(int... nums){
        int max = nums[0];//如果没有传入整数，或者传入null，这句代码会报异常
        for (int i = 1; i < nums.length; i++) {
            if(nums[i] > max){
                max = nums[i];
            }
        }
        return max;
    }

/*    //求n整数的最大值
    public int max(int[] nums){  //编译就报错，与(int... nums)无法区分
        int max = nums[0];//如果没有传入整数，或者传入null，这句代码会报异常
        for (int i = 1; i < nums.length; i++) {
            if(nums[i] > max){
                max = nums[i];
            }
        }
        return max;
    }*/

/*    //求n整数的最大值
    public int max(int first, int... nums){  //当前类不报错，但是调用时会引起多个方法同时匹配
        int max = first;
        for (int i = 0; i < nums.length; i++) {
            if(nums[i] > max){
                max = nums[i];
            }
        }
        return max;
    }*/
}
```

### 4、方法的重载和返回值类型无关

```java
public class MathTools {
    public int getOneToHundred(){
    	return (int)(Math.random()*100);
    }
    
    public double getOneToHundred(){
    	return Math.random()*100;
    }
}
//以上方法不是重载
```

## 5.7 方法的递归调用

**递归调用**：方法自己调用自己的现象就称为递归。

**递归的分类:**

* 递归分为两种，直接递归和间接递归。
* 直接递归称为方法自身调用自己。
* 间接递归可以A方法调用B方法，B方法调用C方法，C方法调用A方法。

**注意事项**：

* 递归一定要有条件限定，保证递归能够停止下来，否则会发生栈内存溢出。
* 在递归中虽然有限定条件，但是递归深度不能太深，否则效率低下，或者也会发生栈内存溢出。

  * 能够使用循环代替的，尽量使用循环代替递归

案例：计算斐波那契数列（Fibonacci）的第n个值，斐波那契数列满足如下规律，

```java
1,1,2,3,5,8,13,21,....
```

即从第三个数开始，一个数等于前两个数之和。假设f(n)代表斐波那契数列的第n个值，那么f(n)满足：

f(n) = f(n-2) + f(n-1); 

```java
public class FibonacciTest {
    public static void main(String[] args) {
        FibonacciTest t = new FibonacciTest();
        //创建FibonacciTest的对象，目的是为了调用f方法

        for(int i=1; i<=10; i++){
            System.out.println("斐波那契数列第" +i +"个数:" + t.f(i));
        }

        System.out.println(t.f(20));//6765

        System.out.println("-----------------------------");
        for(int i=1; i<=10; i++){
            System.out.println("斐波那契数列第" +i +"个数:" + t.fValue(i));
        }

        System.out.println(t.fValue(20));//6765
    }

    //使用递归的写法
    int f(int n){//计算斐波那契数列第n个值是多少
        if(n<1){//负数是返回特殊值1，表示不计算负数情况
            return 1;
        }
        if(n==1 || n==2){
            return 1;
        }
        return f(n-2) + f(n-1);
    }

    //不用递归
    int fValue(int n){//计算斐波那契数列第n个值是多少
        if(n<1){//负数是返回特殊值1，表示不计算负数情况
            return 1;
        }
        if(n==1 || n==2){
            return 1;
        }
        //从第三个数开始，  等于 前两个整数相加
        int beforeBefore = 1; //相当于n=1时的值
        int before = 1;//相当于n=2时的值
        int current = beforeBefore + before; //相当于n=3的值
        //再完后
        for(int i=4; i<=n; i++){
            beforeBefore = before;
            before = current;
            current = beforeBefore + before;
            /*
            假设i=4
                beforeBefore = before; //相当于n=2时的值
                before = current; //相当于n=3的值
                current = beforeBefore + before; //相当于n = 4的值
            假设i=5
                beforeBefore = before; //相当于n=3的值
                before = current; //相当于n = 4的值
                current = beforeBefore + before; //相当于n = 5的值
                ....
             */
        }
        return current;
    }
}
```

## 5.8  对象数组

数组是用来存储一组数据的容器，一组基本数据类型的数据可以用数组装，那么一组对象也可以使用数组来装。

即数组的元素可以是基本数据类型，也可以是引用数据类型。当元素是引用数据类型是，我们称为对象数组。

> 注意：对象数组，首先要创建数组对象本身，即确定数组的长度，然后再创建每一个元素对象，如果不创建，数组的元素的默认值就是null，所以很容易出现空指针异常NullPointerException。

### 5.8.1 对象数组的声明和使用

案例：

（1）定义矩形类，包含长、宽属性，area()求面积方法，perimeter()求周长方法，String getInfo()返回圆对象的详细信息的方法

（2）在测试类中创建长度为5的Rectangle[]数组，用来装3个矩形对象，并给3个矩形对象的长分别赋值为10,20,30，宽分别赋值为5,15,25，遍历输出

```java
package com.atguigu.test08.array;

public class Rectangle {
    double length;
    double width;

    double area(){//面积
        return length * width;
    }

    double perimeter(){//周长
        return 2 * (length + width);
    }

    String getInfo(){
        return "长：" + length +
                "，宽：" + width +
                "，面积：" + area() +
                "，周长：" + perimeter();
    }
}
```

```java
package com.atguigu.test08.array;

public class ObjectArrayTest {
    public static void main(String[] args) {
        //声明并创建一个长度为3的矩形对象数组
        Rectangle[] array = new Rectangle[3];

        //创建3个矩形对象，并为对象的实例变量赋值，
        //3个矩形对象的长分别是10,20,30
        //3个矩形对象的宽分别是5,15,25
        //调用矩形对象的getInfo()返回对象信息后输出
        for (int i = 0; i < array.length; i++) {
            //创建矩形对象
            array[i] = new Rectangle();

            //为矩形对象的成员变量赋值
            array[i].length = (i+1) * 10;
            array[i].width = (2*i+1) * 5;

            //获取并输出对象对象的信息
            System.out.println(array[i].getInfo());
        }
    }
}
```

### 5.8.2 对象数组的内存图分析

对象数组中数组元素存储的是元素对象的首地址。

![image-20211228153827819](imgs/image-20211228153827819.png)

