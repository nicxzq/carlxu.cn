---
title: java学习笔记（1）
author: Carlxu
type: post
date: 2016-10-31T17:25:43+00:00
url: /201611/77/
categories:
  - JAVA
tags:
  - java
  - 个人博客

---
## 类加载

  * 当程序创建了第一个对类的静态成员的引用（如类的静态变量、静态方法、构造方法——构造方法也是静态的）时，才会加载该类。
  * RTTI 
      * 向上转型或向下转型（upcasting and downcasting），在java中，向下转型（父类转成子类）需要强制类型转换
      * Class对象（用了Class对象，不代表就是反射，如果只是用Class对象cast成指定的类，那就还是传统的RTTI）
      * instanceof或isInstance()

<!--more-->

  
&#8211; 反射  
&#8211; 在java的反射机制中，getDeclaredMethod得到的是本类的全部方法，getMethod得到的是本类及所有父类的公有方法；  
&#8211; 反射机制的setAccessible可能会破坏封装性，可以任意访问私有方法和私有变量；  
&#8211; setAccessible并不是将private改为public，事实上，public方法的accessible属性也是false的，setAccessible只是取消了安全访问控制检查，所以通过设置setAccessible，可以跳过访问控制检查，执行的效率也比较高。  
&#8211; RTTI与反射的区别：  
RTTI，编译器在编译时打开和检查.class文件，而反射，是运行时打开和检查.class文件

## 链接

将已经加载的java二进制代码组合到JVM运行状态中去  
验证、准备、解析

## 初始化

所有java虚拟机实现必须在每个类或接口被java程序首次主动使用时才初始化。主动使用有以下6种：  
1. 创建类的实例  
2. 访问某个类或者接口的静态变量，或者对该静态变量赋值（如果访问静态编译时常量(即编译时可以确定值的常量)不会导致类的初始化）  
3. 调用类的静态方法  
4. 反射（Class.forName(xxx.xxx.xxx)）  
5. 初始化一个类的子类（相当于对父类的主动使用），不过直接通过子类引用父类元素，不会引起子类的初始化（参见示例6）  
2. Java虚拟机被标明为启动类的类（包含main方法的）

类与接口的初始化不同，如果一个类被初始化，则其父类或父接口也会被初始化，但如果一个接口初始化，则不会引起其父接口的初始化。

## Java 动态代理。

  1. 通过实现 InvocationHandler 接口创建自己的调用处理器；
  2. 通过为 Proxy 类指定 ClassLoader 对象和一组 interface 来创建动态代理类；
  3. 通过反射机制获得动态代理类的构造函数，其唯一参数类型是调用处理器接口类型；
  4. 通过构造函数创建动态代理类实例，构造时调用处理器对象作为参数被传入。

<pre><code class="java">// 1. InvocationHandlerImpl 实现了 InvocationHandler 接口，并能实现方法调用从代理类到委托类的分派转发
// 其内部通常包含指向委托类实例的引用，用于真正执行分派转发过来的方法调用
InvocationHandler handler = new InvocationHandlerImpl(..); 

// 2.1 通过 Proxy 为包括 Interface 接口在内的一组接口动态创建代理类的类对象
Class clazz = Proxy.getProxyClass(classLoader, new Class[] { Interface.class, ... }); 

// 2.2 通过反射从生成的类对象获得构造函数对象
Constructor constructor = clazz.getConstructor(new Class[] { InvocationHandler.class }); 

// 2.3通过构造函数对象创建动态代理类实例
Interface Proxy = (Interface)constructor.newInstance(new Object[] { handler });

// 2 通过 Proxy 直接创建动态代理类实例
Interface proxy = (Interface)Proxy.newProxyInstance( classLoader, 
     new Class[] { Interface.class }, 
     handler );
</code></pre>