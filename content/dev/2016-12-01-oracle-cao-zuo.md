---
title: oracle释放锁操作
author: Carlxu
type: post
date: 2016-12-01T00:42:01+00:00
url: /201612/73/
categories:
  - Oracle
tags:
  - oracle
  - 个人博客

---
  1. 释放锁表
    
      * 查看锁表进程SQL语句1： 
    <pre><code class="language-sql">select sess.sid, 
   sess.serial#, 
   lo.oracle_username, 
   lo.os_user_name, 
   ao.object_name, 
   lo.locked_mode 
   from v$locked_object lo, 
   dba_objects ao, 
   v$session sess 
where ao.object_id = lo.object_id and lo.session_id = sess.sid; 
</code></pre>
    
      * 查看锁表进程SQL语句2： 
    <pre><code class="language-sql">select * from v$session t1, v$locked_object t2 where t1.sid = t2.SESSION_ID; 
</code></pre>
    
      * 杀掉锁表进程：  
        如有記錄則表示有lock，記錄下SID和serial# ，將記錄的ID替換下面的738,1429，即可解除LOCK  
        alter system kill session '738,1429';