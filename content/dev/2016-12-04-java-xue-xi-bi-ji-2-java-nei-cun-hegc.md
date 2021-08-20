---
title: java学习笔记（2） java内存和GC
author: Carlxu
type: post
date: 2016-12-04T01:26:30+00:00
url: /201612/112/
categories:
  - JAVA
tags:
  - java

---
## 背景知识 {#toc_0}

> Java GC（Garbage Collection，垃圾收集，垃圾回收）机制：  
> 1. 确定哪些内存需要回收，确定什么时候需要执行GC，如何执行GC。  
> 2. 该机制对JVM（Java Virtual Machine）中的内存进行标记，并确定哪些内存需要回收，根据一定的回收策略，自动的回收内存，永不停息（Nerver Stop）的保证JVM中的内存空间，防止出现内存泄露和溢出问题。
> 
> 关于JVM，需要说明一下的是，目前使用最多的Sun公司的JDK中，自从1999年的JDK1.2开始直至现在仍在广泛使用的JDK6，其中默认的虚拟机都是HotSpot。2009年，Oracle收购Sun，加上之前收购的EBA公司，Oracle拥有3大虚拟机中的两个：JRockit和HotSpot，Oracle也表明了想要整合两大虚拟机的意图，但是目前在新发布的JDK7中，默认的虚拟机仍然是HotSpot，因此本文中默认介绍的虚拟机都是HotSpot，相关机制也主要是指HotSpot的GC机制。 

<!--more-->

## java GC {#toc_1}

### 内存是如何分配的； {#toc_2}

JVM管理的内存区域分为下图几个模块：  
![][1] 

  1. 程序计数器（Program Counter Register） 
      * 线程私有
      * 程序计数器只是记录当前指令地址，所以不存在内存溢出的情况，因此，程序计数器也是所有JVM内存区域中唯一一个没有定义OutOfMemoryError的区域
  2. 虚拟机栈（JVM Stack） 
      * 栈帧（Statck Frame）
      * 局部变量表
      * 两类异常：StatckOverFlowError（栈溢出），OutOfMemoryError（内存溢出）
  3. 本地方法栈（Native Method Statck） 
      * 同虚拟机栈，不同的是 虚拟机栈是执行Java方法的，而本地方法栈是用来执行native方法的
  4. 堆区（Heap） 
      * 所有线程共享
      * 存储对象实例
      * OutOfMemoryError:Java heap space
  5. 方法区（Method Area） 
      * 方法区是各个线程共享的区域，用于存储已经被虚拟机加载的类信息（即加载类时需要加载的信息，包括版本、field、方法、接口等信息）、final常量、静态变量、编译器即时编译的代码等。
      * 包含 运行时常量池（Runtime Constant Pool）
      * OutOfMemoryError:PermGen space
  6. 直接内存（Direct Memory） 
      * 非jvm占用的宿主内存

#### 内存分配机制 {#toc_3}

`分代分配，分代回收。`

对象将根据存活的时间被分为：年轻代（Young Generation）、年老代（Old Generation）、永久代（Permanent Generation，也就是方法区）  
![][2] 

### 如何保证内存不被错误回收（即：哪些内存需要回收）； {#toc_4}

分代收集

  1. 年轻代  
    年轻代可以分为3个区域：Eden区（伊甸园，亚当和夏娃偷吃禁果生娃娃的地方，用来表示内存首次分配的区域，再贴切不过）和两个存活区（Survivor 0 、Survivor 1）  
![][3] 

“停止-复制（Stop-and-copy）”清理法（将Eden区和一个Survivor中仍然存活的对象拷贝到另一个Survivor中）  
停止会停止所有线程的执行，比较低效

在Eden区，HotSpot虚拟机使用了两种技术来加快内存分配。分别是bump-the-pointer和TLAB（Thread-Local Allocation Buffers）

-XX:MaxTenuringThreshold survivor0/1切换次数

  1. 老年代

标记-整理算法，即：标记出仍然存活的对象（存在引用的），将所有存活的对象向一端移动，以保证内存的连续。

可能存在年老代对象引用新生代对象的情况，如果需要执行Young GC，则可能需要查询整个老年代以确定是否可以清理回收，这显然是低效的。解决的方法是，年老代中维护一个512 byte的块——”card table“

Minor GC时，虚拟机会检查每次晋升进入老年代的大小是否大于老年代的剩余空间大小，如果大于，则直接触发一次Full GC，否则，就查看是否设置了-XX:+HandlePromotionFailure（允许担保失败），如果允许，则只会进行MinorGC，此时可以容忍内存分配失败；如果不允许，则仍然进行Full GC（这代表着如果设置-XX:+Handle PromotionFailure，则触发MinorGC就会同时触发Full GC，哪怕老年代还有很多内存，所以，最好不要这样做）。

-XX:+UseAdaptiveSizePolicy 否采用动态控制策略  
-XX:PretenureSizeThreshold

  1. 方法区（永久代）

常量池中的常量，无用的类信息

-Xnoclassgc进行控制  
-verbose，-XX:+TraceClassLoading、-XX:+TraceClassUnLoading可以查看类加载和卸载信息  
-verbose、-XX:+TraceClassLoading可以在Product版HotSpot中使用；  
-XX:+TraceClassUnLoading需要fastdebug版HotSpot支持

### 在什么情况下执行GC以及执行GC的方式； {#toc_5}

不同垃圾收集器机制不一样

  * Serial收集器：新生代收集器
  * ParNew收集器：新生代收集器，使用停止复制算法，Serial收集器的多线程版
  * Parallel Scavenge 收集器：新生代收集器，使用停止复制算法，关注CPU吞吐量，即运行用户代码的时间/总时间
  * Serial Old收集器：老年代收集器，单线程收集器，串行，使用标记整理（整理的方法是Sweep（清理）和Compact（压缩），清理是将废弃的对象干掉，只留幸存的对象，压缩是将移动对象，将空间填满保证内存分为2块，一块全是对象，一块空闲）算法
  * Parallel Old收集器：老年代收集器，多线程，并行，多线程机制与Parallel Scavenge差不多
  * CMS（Concurrent Mark Sweep）收集器，老年代收集器，致力于获取最短回收停顿时间（即缩短垃圾回收的时间）

### 如何监控和优化GC机制。 {#toc_6}

JVM监控与调优

### 文中并发（Concurrent）和并行（Parallel）的区别： {#toc_7}

    并发是指用户线程与GC线程同时执行（不一定是并行，可能交替，但总体上是在同时执行的），
    不需要停顿用户线程（其实在CMS中用户线程还是需要停顿的，只是非常短，GC线程在另一个CPU上执行）；
         并行收集是指多个GC线程并行工作，但此时用户线程是暂停的；
         所以，Serial是串行的，Parallel收集器是并行的，而CMS收集器是并发的.

 [1]: http://www.carlxu.cn/wp-content/uploads/2016/12/14807575246906.jpg
 [2]: http://www.carlxu.cn/wp-content/uploads/2016/12/14809191546791.jpg
 [3]: http://www.carlxu.cn/wp-content/uploads/2016/12/14809192393902.jpg