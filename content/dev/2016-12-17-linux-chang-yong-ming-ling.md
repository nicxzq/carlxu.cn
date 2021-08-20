---
title: Linux常用命令
author: Carlxu
type: post
date: 2016-12-16T08:51:40+00:00
url: /201612/161/
categories:
  - 专业笔记
tags:
  - Linux
  - 命令

---
## 非常常用 {#toc_0}

  * ls
  * cd
  * opt

<!--more-->

## mkdir {#toc_1}

`mkdir [选项] 目录…`

> linux mkdir 命令用来创建指定的名称的目录，要求创建目录的用户在当前目录中具有写权限，并且指定的目录名不能是当前目录中已有的目录。 

**主要参数**：  
-m, &#8211;mode=模式，设定权限<模式> (类似 chmod)，而不是 rwxrwxrwx 减 umask  
-p, &#8211;parents 可以是一个路径名称。此时若路径中的某些目录尚不存在,加上此选项后,系统将自动建立好那些尚不存在的目录,即一次可以建立多个目录;  
-v, &#8211;verbose 每次创建新目录都显示信息

**实例**：

    mkdir -p test2/test22
    mkdir -m 777 test3
    # 一个命令创建项目的目录结构
    mkdir -vp scf/{lib/,bin/,doc/{info,product},logs/{info,product},service/deploy/{info,product}}
    

## rm {#toc_2}

`rm [选项] 文件…`

> 删除一个目录中的一个或多个文件或目录，如果没有使用- r选项，则rm不会删除目录。如果使用 rm 来删除文件，通常仍可以将该文件恢复原状。 

**主要参数**：  
-f, &#8211;force 忽略不存在的文件，从不给出提示。  
-i, &#8211;interactive 进行交互式删除  
-r, -R, &#8211;recursive 指示rm将参数中列出的全部目录和子目录均递归地删除。  
-v, &#8211;verbose 详细显示进行的步骤

**实例**：

    # 删除以-f开头的文件
    rm -- -f
    # 自定义回收站功能
    myrm(){ D=/tmp/$(date +%Y%m%d%H%M%S); mkdir -p $D; mv "$@" $D && echo "moved to $D ok"; }
    

## cat {#toc_3}

`cat [选项] [文件]…`

> 1.一次显示整个文件:cat filename  
> 2.从键盘创建一个文件:cat > filename 只能创建新文件,不能编辑已有文件.  
> 3.将几个文件合并为一个文件:cat file1 file2 > file 

**主要参数**：  
-A, &#8211;show-all 等价于 -vET  
-b, &#8211;number-nonblank 对非空输出行编号

-e 等价于 -vE  
-E, &#8211;show-ends 在每行结束处显示 $

-n, &#8211;number 对输出的所有行编号,由1开始对所有输出的行数编号  
-s, &#8211;squeeze-blank 有连续两行以上的空白行，就代换为一行的空白行

-t 与 -vT 等价  
-T, &#8211;show-tabs 将跳格字符显示为 <sup>I</sup>

-u (被忽略)  
-v, &#8211;show-nonprinting 使用 ^ 和 M- 引用，除了 LFD 和 TAB 之外

**实例**：

    # tac 是将 cat 反写过来，所以他的功能就跟 cat 相反， cat 是由第一行到最后一行连续显示在萤幕上，而 tac 则是由最后一行到第一行反向在萤幕上显示出来
    

## more \[-dlfpcsu \] \[-num \] \[+/ pattern\] \[+ linenum\] [file … ] {#toc_4}

more命令和cat的功能一样都是查看文件里的内容，但有所不同的是more可以按页来查看文件的内容，还支持直接跳转行等功能。  
`<br />
Enter    向下n行，需要定义。默认为1行<br />
Ctrl+F   向下滚动一屏<br />
空格键  向下滚动一屏<br />
Ctrl+B  返回上一屏<br />
=       输出当前行的行号<br />
:f     输出文件名和当前行的行号<br />
V      调用vi编辑器<br />
!命令   调用Shell，并执行命令<br />
q       退出more<br />
`