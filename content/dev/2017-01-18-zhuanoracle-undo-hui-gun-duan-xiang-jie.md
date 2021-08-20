---
title: （转）oracle undo回滚段详解
author: Carlxu
type: post
date: 2017-01-18T01:52:13+00:00
url: /201701/260/
categories:
  - Oracle
tags:
  - oracle

---
[原文链接][1]

## **1.Undo****是干嘛用的？   ** {#toc_0}

在介绍undo之前先说一下另外一个东西 transaction ，翻译成交易或事务。我们在进行一个事务的过程中需要申请许多资源，一个复杂的事务也需要很多步来完成。那么一个复杂的事务是只有两个结果，要么成功，要么失败（相当于从来没发生过）。  
<!--more-->

> 　　一个很典型的列子，银行转账，其实其需要两步操作，第一步先将你账户上的钱减去，第二步把被转账户的钱加上，（先减后加，出了问题银行不吃亏。呵呵！）这样就是一个完整的事务。如果执行了一半，你的钱减了，被转账户的钱没加上，这个时候事务就要回滚，回滚到原始状态。也就是在转账之前，需要先记录你和被转账户上的金额。这就样能保证，一旦事务失败就回滚到事务的发生之前的状态。

为那保证一个事务的原始性和完整性，就引这入undo 的概念。Undo就是用来记录保存事务操作过程中的数据，如果事务发生错误，可以之前的数据进行填补。

### **Undo Segment 还原段** {#toc_1}

![oracle undo回滚段详解][2] 

从上面的视图，我们就可以很清晰的看出，我们要对表（table）中的一个数据进行修改，在修改之前，先把老的映像（old image）放到undo 上面。然后再在table中放入new image 。假如过程失败，我们还可以把undo 上的old image 再拿回来放在原先的位置，从而使这件事儿看起来像没发生过一样。

Undo segment 是保存在表空间上的。Undo 大小是固定的，既然是固定的也就是有限的。如果保存的记录非常多，那么它就会被占满，新记录的数据会覆盖掉最早的数据。所以用一个圆形的盘片能更加形象的表示。数据从一个位置开始写入，当写满一圈后，最新的数据就会覆盖最早写入的数据。

**

**

## **2.undo****可以干啥？ ** {#toc_2}

![oracle undo回滚段详解][3] 

### **   1. Transaction rollback  事务回退** {#toc_3}

**   2. Transaction recovery 事务恢复**

**   3. Read consistency  读一致性**

>     事务回退与事务恢复的效果是一样的。事务反转是人主动去做的，人在操作的过程中反悔了，相当于我在写文档时按个ctrl+z 。事务恢复是机器自动完成的，比如在事务进行过程中简拼突然断电了，下次重启服务之后，系统自动回滚。
> 
> Read consistency  读一致性。读一致性对于多用户操作是非常重要的。如果你在多人开发中使用过版本控制工具（git/cvs/svn）的话，下面的概念你将很容易理解。

下面重点讲一致性

### **Oracle 读一致性概念  ** {#toc_4}

我知道oracle允许可以由多个用户对数据库进行操作，当你执行一个查询几百万条记录的操作时，这个过程可能需要几分钟。在这个过程中其它用户对你查询的数据时行了修改。这里就要保证你查询的结果是被修改之前的（也就是你查询开始那个时刻的结果）。

这里明确一个概念，事务的开始，在我们执行一条（更新、修改、删除）语句时；事务的结束，必须执行提交动作（执行commit或 rollback 命令）

![][4]  
我们从上面的流程图来理解一下oracle是如何保证读一致性的。

当我们执行一个事务的时候，oracle会分配一个SCN编号，这个编号是递增的。下一个事务的编号一定比当前事务的编号大。

上图中执行第一个事务分配的编号为10023，在这个事务执行的过程中，另一事务对SCN 编号为10008和10021的数据块进行了修改。用来替换的数据块SCN编号为10024 ，而被替换掉的数据块会被保存到undo 上面。当第一个事务执行到被修改过的数据块时，发现10024比10023大，这个时候就会到undo segment上找比自己SCN号小的数据块进行读，于是发找到了SCN号为10008和10021两个块。这样就有效的保证了读一致性。

当然，会有一种特殊情况，也就是undo segment 太小，最多放100条数据，可一下子来了120条数据，那么最先写入的20条数据被最后写入的20条数据覆盖。这个时候就会报错，这也是为什么要对数据据进行调优的原因。

## ** 3.Redo or undo 区别     ** {#toc_5}

### **什么是Redo** {#toc_6}

Redo记录transaction logs，分为online和archived。以恢复为目的。

比如，机器停电，那么在重起之后需要online redo logs去恢复系统到失败点。

比如，磁盘坏了，需要用archived redo logs和online redo logs区恢复数据。

### **什么是Undo** {#toc_7}

Redo 是为了重新实现你的操作，而Undo相反，是为了撤销你做的操作。Undo更像常使用的ctrl+z ,撤销到上一步的状态。而Redo 是也就会记录undo 的操作。

![oracle undo回滚段详解][5] 

当我们插入一条数据时，首先这个动作会被记录到redo log 中，操作也会被记录到到undo ，undo本身的动作也会做为一条数据被记录到redo log ，插入一条数据，索引（indexes）会发生变化，索引的变化也会做一条数据被记录到redo log 。Redo 记录着一个操作所有相关的信息，这样才能完整的保证场景的重现。

需要说明的是在上面的图表中，不管是undo 还是redo都是写在内存里的，一旦断电，所有信息将会消失。是redo log 的信息先写到磁盘上的，在实例进行恢复的时候首先进行前滚（redo），将undo的内容也会前滚回去，然后再根据undo里的内容进行回滚（undo）。

## **4. 如何配置使用undo？       ** {#toc_8}

要想使用undo 首先需要创建undo表空间。我们可以创建多个undo表空间，但只能有一个undo表空间是处于使用状态。

查看undo配置信息：

> SQL> show parameter undo
> 
> NAME                           TYPE                VALUE
> 
> ———————————— —————————————————-
> 
> undo_management                 string            AUTO
> 
> undo_retention                   integer           900
> 
> undo_tablespace                  string           UNDOTBS1

Undo配置参数含义

-DNDO_MANAGEMENT     undo的管理模式，分自动和手动

-UNDO_TABLESPACE      当前正在被使用的undo表

-UNDO_RETENTION        规定多长时间内，数据不能被覆盖。

—————————————–

AUTO             表示undo为自动管理模式。

900               表示在900秒内，undo上的数据不能被覆盖。

UNDOTBS1    是当前正在使用的undo表空间。

创建undo表空间，与创建一般的表空间类似，命令如下：

> SQL> create undo tablespace myundotbs
> 
> 2  datafile ‘/ora10/product/oradata/ora10/myundotbs1.dbf‘ size 10M;
> 
> Tablespace created.

查看新创建的undo表空间

> SQL>  select tablespace\_name,contents from dba\_tablespaces;
> 
> TABLESPACE_NAME                    CONTENTS
> 
> ———————————————————— ——————
> 
> SYSTEM                                 PERMANENT
> 
> UNDOTBS1                               UNDO  　　//老的undo表空间
> 
> SYSAUX                                 PERMANENT
> 
> TEMP                                    TEMPORARY
> 
> USERS                                  PERMANENT
> 
> PAUL                                   PERMANENT
> 
> MYUNDOTBS                              UNDO   //新创建的undo表空间
> 
> SQL> show parameter undo      再次查看当前使用的表空间
> 
> NAME                           TYPE          VALUE
> 
> ———————————— —————————————————-
> 
> undo_management                 string            AUTO
> 
> undo_retention                   integer             900
> 
> undo_tablespace                  string           UNDOTBS1

切换undo表空间：

> SQL> alter system set undo_tablespace=myundotbs;
> 
> System altered.

**注意：只能在Automatic Undo Management mode下修改**

**修改管理模式：SQL> alter system set undo_management=‘manual‘ scope=spfile;（需重启数据库）**

> SQL> show parameter undo   再次查看当前使用的表空间
> 
> NAME                           TYPE               VALUE
> 
> ———————————— —————————————————-
> 
> undo_management                 string            AUTO
> 
> undo_retention                   integer          900
> 
> undo_tablespace                  string           MYUNDOTBS    //已经切换的了undo表空间

**删除undo表空间：**

> SQL> drop tablespace myundotbs;
> 
> Tablespace dropped.

Drop一个undo表空间后，在磁盘上还是存在的，我们需要通过操作系统层面用rm命令将文件删除。

> 　表空间的切换、删除命令非常简单，但这里我们需要思考一下实际切换场景。当我们执行一个事务时，事务执行了一半还没有提交，这个时候进行切换undo表空间是否可以成功? 理论上undo表空间正在使用中，是不允许切换的。但实际上undo表空间在使用中是可以切换的，但切换之后立刻删除，系统会提示错误。把事务提交后再删除，系统依然提示错误。这里只有将替换掉的undo表空间切换到使用状态，再切换到废弃状态才能被删除。上面的情况，有兴趣有同学可以验证一下。

Undo调优

Undo的设置取决于我们实际的生产系统。如何设置undo更合理地为我们工作呢？

Undo表空间的大小：

我们在创建一个undo表空间的使用，就指定了它的大小，这个大小一旦创建是不可变更的。设置过大，是一种浪费，设置过小，例如删除100万条记录，这些删除的记录都要临时存放到undo表空间中，如果undo的大小不能存储100万条记录，那么就会出问题。

Undo数据的存放时间：

也就是undo_retention 参数所对应的时间，undo上有数据存放时间与undo大小的密切关系。存放时间越长，需要的表空间越大。

Undo表空间的历史信息：

如何合理设置undo表空间的大小和存放时间呢？那么就需要参考历史记录

![][6] 

这个数据每隔10分钟采集一次，结束时间减去开始时间，在这段时间内使用了多少个undo数据块。

计算每秒钟使用数据块的多少？

求最大值：

> SQL> select max(undoblks / ((end\_time-begin\_time)_24_3600)) from v$undostat;
> 
> MAX(UNDOBLKS/((END\_TIME-BEGIN\_TIME)_24_3600))
> 
> ———————————————
> 
> 14.15833333

求平均值：

> SQL>  select sum(undoblks)/sum((end\_time – begin\_time)_24_3600) from v$undostat;
> 
> SUM(UNDOBLKS)/SUM((END\_TIME-BEGIN\_TIME)_24_3600)
> 
> ————————————————
> 
> 4.122282389

 [1]: http://codecloud.net/133317.html
 [2]: https://www.carlxu.cn/wp-content/uploads/2017/01/14847043875430.png
 [3]: https://www.carlxu.cn/wp-content/uploads/2017/01/14847044428155.png
 [4]: https://www.carlxu.cn/wp-content/uploads/2017/01/14847044769838.png
 [5]: https://www.carlxu.cn/wp-content/uploads/2017/01/14847045262106.png
 [6]: https://www.carlxu.cn/wp-content/uploads/2017/01/14847045793957.png