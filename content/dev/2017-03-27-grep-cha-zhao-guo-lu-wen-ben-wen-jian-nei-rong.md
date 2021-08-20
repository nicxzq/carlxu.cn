---
title: grep 查找过滤文本文件内容
author: Carlxu
type: post
date: 2017-03-27T06:55:48+00:00
draft: true
private: true
url: /201703/294/
categories:
  - 专业笔记
tags:
  - Linux

---
grep是Linux命令行下常用于查找过滤文本文件内容的命令。最简单的用法是：

> grep apple fruitlist.txt 

<!--more-->

如果想忽略大小写，可以用-i参数：

> grep -i apple fruitlist.txt 

如果想搜索目录里所有文件，包括子目录的话，并且在结果中显示行号，可以用以下命令：

> grep -nr apple * 

grep的语法支持正则表达式，正则表达式有些复杂，以后再讲解。下面是一些有用的参数：

  * -A num, &#8211;after-context=num: 在结果中同时输出匹配行之后的num行
  * -B num, &#8211;before-context=num: 在结果中同时输出匹配行之前的num行，有时候我们需要显示几行上下文。
  * -i, &#8211;ignore-case: 忽略大小写
  * -n, &#8211;line-number: 显示行号
  * -R, -r, &#8211;recursive: 递归搜索子目录
  * -v, &#8211;invert-match: 输出没有匹配的行

我们可以通过管道操作来让grep变得更强大，管道操作就是把前面一条命令的输出作为后面一条命令的输入，从而把很多简单的命令组合起来完成复杂的功能。例如，如果我们想查找包含apple的行，但又想过滤掉pineapple，可以用下面的命令：

> grep apple fruitlist.txt | grep -v pineapple 

如果我们想把搜索结果保存起来，那么可以把命令的标准输出重定向到文件：

> grep apple fruitlist.txt | grep -v pineapple > apples.txt 

重定向符号>和管道操作符号|的区别是，重定向后面接的是一个文件，它后面不能再接任何文件或命令了；而管道操作后面接的是命令，可以无限地接下去。如果想以追加方式写到文件，可以用>>。管道操作是Linux命令行的一种哲学，它是计算机技术中少有的能沿用几十年的技术之一。通过管道操作，一行命令可以完成Windows下上千行程序也不能完成的文本处理功能。