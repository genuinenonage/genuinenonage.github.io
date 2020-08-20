---
<<<<<<< HEAD:new/JVM-更新中.md
title: JVM
date: 2020/08/12 18:59:00
tags:
- java
- JVM
categories:
- java
- JVM
=======
title: JVM简要笔记-更新中
date: 2020/08/12 18:59:00
tags:
- JVM
- Java
categories:
- JVM
- Java
>>>>>>> 2505c1cf5f2b1bf8f331c33ee7980e7845f37b81:source/_posts/JVM.md
---
## JVM  
java 跨平台语言就是因为JVM  
JVM 跨语言的平台：Kotlin,Clojure,Groovy(需各自的编译器)...  
趋向于 多语言混合编程  
如何搞懂JVM，自己动手编写一个JVM虚拟机。  

## 虚拟机  
虚拟机（Virtual Machine）虚拟的计算机，分为系统虚拟机和程序虚拟机（专门执行单个计算机程序而设计）。
## Java虚拟机    
Java技术的核心就是Java虚拟机（二进制字节码的运行环境）。  
特点： 
* 一次编译，到处运行  
* 自动内存管理  
* 自动垃圾回收功能  
### 
Java源文件 - 编译器 - 字节码文件 .class - 类加载器 - 字节码校验器 - 翻译字节码、JIT编译器（解释执行即时编译）  
### Java架构模型  
Java编译器上输入的指令流是基于栈的指令集架构。（另一种指令集架构是基于寄存器的指令集架构） 
跨平台性、指令集小、指令多；执行性能比寄存器差。 
### 反编译操作  
cd out/production/java  
javap -v StackStruTest.class    
### JVM的生命周期  
1. 启动：引导类加载器（bootstrap class loader）创建一个初始类（initial class）来完成。这个类有虚拟机的具体实现来指定的。  
2. 执行：执行Java，真正是执行程序jvm虚拟机的进程。（jps查看进程）  
3. 退出：程序正常执行结束；遇到异常或错误；线程盗用exit()或halt()方法（Runtime()是单例的）。  
### JVM的发展历程  
（san）classic VM 、 Exact VM 、 hotspot VM    
（BEA）JRockit：专注于服务器端，纯即时编译器  
（IBM）J9：IBM Technology for Java Virtual Machine 简称IT4J。  
KVM：面向更低端的设备（如：智能控制器，传感器）  
Azul VM和BEA Liquid VM 与特定硬件平台绑定、软硬件配合的专有虚拟机。  
Apache Harmony  
Microsoft JVM  
TaobaoJVM  
（非Java，应用Android系统）Dalvik VM  
（Oracle发展中 跨语言全栈虚拟机）Graal VM  
# 类加载器与类加载子系统  
类加载子系统 加载class文件，class文件在文件开头有特殊的标识。   
ClassLoader只负责class文件的加载，是否能运行有ExecutionEngine决定。  
加载的类信息存放于方法区的内存空间。方法去还有存放运行时常量池信息。  
### 类的加载过程  
开始 - 装载类HelloLoader - （是否装载顺利，否则抛出异常） - 链接 - 初始化HelloLoader - 调用 HelloLoader.main() - 结束  

1. 加载Loading：
	1. 通过类的全限定名获取此类的二进制字节流。
	2. 静态存储结构转化为方法区的运行时数据结构。
	3. 在内存中生成一个代表这个类的java.lang.Class对象，作为方法去这个类的各种数据的访问对象。
2. 链接Lingking：
	1. 验证Verify：确保class文件中的字节流中包含的信息符合当前虚拟机要求，保证被加载类的正确性。
		1. 主要四种验证：文件格式，元数据，字节码，符号引用验证。
	2. 准备Prepare：为类变量分配内存并赋值默认初始值，如零值。（后初始化）  
		1. 这里不包含final修饰的static，因为final在编译时就会分配，准备阶段会显式初始化；
		2. 不会为实例变量分配初始化。类变量会分配在方法区中，而实例变量会随着对象一起分配到Java堆中。
	3. 解析Resolve：符号引用转换为直接引用。
3. 初始化Initialization：
	1.  初始化阶段就是执行类构造器方法<clinit>()的过程。
	2.  不需定义，javac编译器自动收集类中的所有类变量的赋值动作和静态代码块中的语句合并而来。
	3.  构造器方法中指令按语句在源文件中出现的顺序执行。
	4.  <clinit>()不同于类的构造器。
	5.  类中有构造方法会出现<init>的结构
	6.  该类有父类，加载Father类，其次加载Son类。
	7.  虚拟机保证一个类的<clinit>()方法在多线程下被同步加锁（一个类只会被加载一次 ）。  
### 类加载器的分类
自定义类，系统类，扩展类，引导类加载器（四者是包含关系）
两种类型：  
	1. 引导类加载器（Java的核心类库使用引导类加载器进行加载的 .class.getClassLoader() 获取不到。C和C++编写的）
	2. 自定义类加载器（继承了ClassLoader的类，如系统，扩展类） 
1. 启动类加载器（引导类加载器，Bootstrap classLoader）  
	1. 没有父加载器
	2. 加载Java的核心库
	3. 加载扩展类和应用程序类加载器，并指定为他们的父类加载器。
	4. C/C++语言实现的，嵌套在JVM内部。
2. 扩展类加载器（Extension ClassLoader）
	1. Java语言编写，由sun.misc.Launcher$ExtClassLoader实现。

<<<<<<< HEAD:new/JVM-更新中.md
### 双亲委派机制  
有父类加载器向上委托。父类加载器失败交由子加载器自己处理。

优势：
	1. 避免类的重复加载。
	2. 保护程序安全，防止核心API被篡改。  

沙箱安全机制：保护引导类加载器不被破坏。

### 其他  
JVM中两个class对象是否一个类名：
	1. 类的完整类名一直，包括包名。  
	2. 加载这个类的ClassLoader必须相同。  

Java程序对类的使用方式：主动使用和被动使用   

被动使用：不会初始化。  

# 运行时数据区  
（run data area）方法区（堆外内存）、堆、虚拟机栈、本地方法栈、程序计数器。  
不同的JVM对内存的划分方式和管理机制存在部分差异。  
线程间共享：堆、堆外内存（永久代或元空间、代码缓存）。
每个线程：独立包括程序计数器、栈、本地栈。  
#### Class Runtime  
一个JVM对应着一个Runtime实例  
### 线程  
每个线程都与操作系统的本地线程直接映射。  
后台系统线程主要有：
* 虚拟机线程
* 周期任务线程
* GC线程
* 编译线程
* 信号调度线程  

### 程序计数器（PC寄存器）  
(Program Counter Register) ,类似CPU的寄存器。  
PC寄存器：用来存储指向下一条指令的地址。  
当前线程-Java栈-当前栈帧-局部变量表、操作数栈、动态链接、方法返回值。




=======
>>>>>>> 2505c1cf5f2b1bf8f331c33ee7980e7845f37b81:source/_posts/JVM.md
  
