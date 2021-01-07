---
title: 第15章 Java 高级编程 -反射
date: 2021-11-27 04:58:02
tags: 
- java
- 反射
categories:
- Java基础

---

<center>总体来说，没有什么迫在眉睫一定要得到的东西。这一路上也不曾感觉有所失去。所以，我是一个幸福的人!</center>

<!--more-->

## 15.1 ：Java反射机制概述

### 15.1.1 反射的概述

​		反射是被视为**动态语言**的关键，是因为 Java 文件要进行两个阶段的“洗礼”，第一个编译阶段是生成  .java 文件编译为 .class 文件，此时还不能确定某一类的对象，只有在运行时才能确定是哪个。体现了动态性。

![image-20201124193827032](https://gitee.com/dlutlgy/window_typora/raw/master/images/image-20201124193827032.png)

反射的意思就是 通过类的对象，能了解到类的信息。就是反射。

![image-20201127142743534](https://gitee.com/dlutlgy/window_typora/raw/master/images/image-20201127142743534.png)



### 15.1.2 动态语言 与 静态语言

**动态语言**：在运行时可以改变其结构的语言，例如新的函数、对象、甚至代码可以 被引进，已有的函数可以被删除或是其他结构上的变化。通俗点说就是**在运行时代码可以根据某些条件改变自身结构。** 

**静态语言**：运行时结构不可改变，如Java、C、 C++。

虽然Java不是动态语言，但是Java可以成为“**准动态语言**”，也就是说它有动态性，可以利用反射的机制来体现。



### 15.1.3 Java反射机制研究与应用

反射可以干什么？

+ 在运行时判断任意一个对象所属的类 
+ 在运行时构造任意一个类的对象 
+ 在运行时判断任意一个类所具有的成员变量和方法 
+ 在运行时获取泛型信息 
+ 在运行时调用任意一个对象的成员变量和方法 
+ 在运行时处理注解 
+ 生成动态代理

总之一句话：就是可以获取类的任何信息。

关于反射相关的API

+ java.lang.Class:代表一个类
+ java.lang.reflect.Method:代表类的方法
+ java.lang.reflect.Field:代表类的成员变量
+ java.lang.reflect.Constructor:代表类的构造器

## 15.2 理解Class类并获取Class实例

### 15.2.1 Class类

Class是用来描述类的类，比如每个类都有属性，都有方法等等，所以又抽象出一个类。Class类是反射的源头。

<img src="https://gitee.com/dlutlgy/window_typora/raw/master/images/image-20201127144332468.png" alt="image-20201127144332468" style="zoom: 80%;" />

因为 Object 类是所有类的父类，要想得到每个类的信息，getClass()方法就声明在了 Object 类中。

​		对象照镜子后可以得到的信息：某个类的属性、方法和构造器、某个类到底实现了哪些接口。对于每个类而言，JRE 都为其保留一个不变的 Class 类型的对象。一个 Class 对象包含了特定某个结构的有关信息。

+ Class本身也是一个类 
+ Class 对象只能由系统建立对象 
+  一个加载的类在 JVM 中只会有一个Class实例 
+  一个Class对象对应的是一个加载到JVM中的一个.class文件 
+  每个类的实例都会记得自己是由哪个 Class 实例所生成 
+  通过Class可以完整地得到一个类中的所有被加载的结构 
+  Class类是Reflection的根源，针对任何你想动态加载、运行的类，唯有先获得相应的 Class对

### 15.2.2 获取Class类的实例 （四种方法）

获取Class类的实例的四种方法，其中前三种方法比较重要，经常用到，最后一种不需要掌握。

 方式一：调用运行时类的属性：.class

```java
Class clazz1 = Person.class;
System.out.println(clazz1);
```

方式二：通过运行时类的对象,调用getClass()

```java
Person p1 = new Person(); // 此时Person类为运行时类
Class clazz2 = p1.getClass();//.getclass 是在object里面造的
System.out.println(clazz2);
```

方式三：调用Class的 静态方法 ：forName(String classPath)。这里必须写 类的全类名，因为同一个module下可能有多个person。

```java
Class clazz3 = Class.forName("com.atguigu.java.Person");
System.out.println(clazz3+"打印3");
```

方式四：使用类的加载器：ClassLoader  (了解)

```java
ClassLoader classLoader = ReflectionTest.class.getClassLoader();
Class clazz4 = classLoader.loadClass("com.atguigu.java.Person");
System.out.println(clazz4);
```



## 15.3 类的加载 与ClassLoader的理解（了解）

### 15.3.1 类的加载过程 （了解）

当程序主动使用某个类时，如果该类还未被加载到内存中，则系统会通过 如下三个步骤来对该类进行初始化。

![image-20201127152144541](https://gitee.com/dlutlgy/window_typora/raw/master/images/image-20201127152144541.png)

+ 加载：将class文件字节码内容加载到内存中，并将这些静态数据转换成方法区的运行时 数据结构，然后生成一个代表这个类的java.lang.Class对象，作为方法区中类数据的访问 入口（即引用地址）。所有需要访问和使用类数据只能通过这个Class对象。这个加载的 过程需要类加载器参与。
+ 链接：将Java类的二进制代码合并到JVM的运行状态之中的过程。
  + 验证：确保加载的类信息符合JVM规范，例如：以cafe开头，没有安全方面的问题 
  + 准备：正式为类变量（static）分配内存并设置类变量默认初始值的阶段，这些内存 都将在方法区中进行分配。 
  + 解析：虚拟机常量池内的符号引用（常量名）替换为直接引用（地址）的过程。
+ 初始化
  + 执行类构造器<clinit>()方法的过程。类构造器<clinit>()方法是由编译期自动收集类中 所有类变量的赋值动作和静态代码块中的语句合并产生的。（类构造器是构造类信息的，不是构造该类对象的构造器）。
  + 当初始化一个类的时候，如果发现其父类还没有进行初始化，则需要先触发其父类 的初始化。
  + 虚拟机会保证一个类的<clinit>()方法在多线程环境中被正确加锁和同步。



![image-20201125121333135](https://gitee.com/dlutlgy/window_typora/raw/master/images/image-20201125121333135.png)

类加载器的作用： 

+ 类加载的作用：将class文件字节码内容加载到内存中，并将这些静态数据转换成方 法区的运行时数据结构，然后在堆中生成一个代表这个类的java.lang.Class对象，作为 方法区中类数据的访问入口。 
+  类缓存：标准的 JavaSE 类加载器可以按要求查找类，但一旦某个类被加载到类加载器 中，它将维持加载（缓存）一段时间。不过 JVM 垃圾回收机制可以回收这些Class对象。



## 15.4 创建运行时类对象

```java
//1.根据全类名获取对应的Class对象 
String name = “atguigu.java.Person"; 
Class clazz = null; clazz = Class.forName(name); 
//2.调用指定参数结构的构造器，生成Constructor的实例 
Constructor con = clazz.getConstructor(String.class,Integer.class); 
//3.通过Constructor的实例创建对应类的对象，并初始化类属性 
Person p2 = (Person) con.newInstance("Peter",20); 
System.out.println(p2);
```

## 15.5 获取运行时类的完整结构

具体内容在代码中体现。