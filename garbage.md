
# java 垃圾回收知识点(持续更新中)

参考：

[CMS](https://www.toutiao.com/i7026206728010121741/?tt_from=weixin&utm_campaign=client_share&wxshare_count=1&timestamp=1635994595&app=news_article&utm_source=weixin&utm_medium=toutiao_android&use_new_style=1&req_id=202111041056350101310761311BD182F1&share_token=0546fd54-a6a6-4e1f-a8cb-462596c4c1fa&group_id=7026206728010121741)


## 垃圾回收算法

引用计数         会出现循环引用问题
root searching 

## 10种垃圾回收器

| 回收器名称| 概述|
|----------|---------|
|Serial、Serial Old              | 会引起 STW ，分代                   |
|Parallel Scavenge、Parallel Old  |会引起STW 目前主要使用的是这种，分代  |
|ParNew、CMS                      |会短暂的引起STW ，分代，                |
|G1                               |逻辑上分代，                        |
|ZGC、...                         ||
 
## CMS 的四个阶段

初始标记，会引起STW
并发标记，不会STW
重新标记，会因为STW
并发清除，不会STW

## 回收算法

|算法名称  | 应用  |
|---------|-----  | 
|copy     | 年轻代 |
|标记清除  | 老年代 |
|标记压缩  |老年代  |

## 标记算法

三色标记法

## 分了几个代

年轻代，又分为eden，S1,S2, 8:1:1
年轻代老年代 1:3

## JMM
堆heap： 优点：运行时数据区，动态分配内存大小，有gc；,缺点：因为要在运行时动态分配，所以存取速度慢，对象存储在堆上，静态类型的变量跟着类的定义一起存储在堆上。
栈stack：存取速度快，仅次于寄存器，缺点：数据大小与生存期必须是确定的，缺乏灵活性，栈中主要存放基本类型变量（比如，int,shot,byte,char,double,foalt,boolean和对象句柄），jmm要求，调用栈和本地变量存放在线程栈上

当一个线程可以访问一个对象时，也可以访问对象的成员变量，如果有两个线程访问对象的成员变量，则每个线程都有对象的成员变量的私有拷贝，

