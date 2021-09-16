
# java 垃圾回收知识点(持续更新中)
## 垃圾机制

引用计数         会出现循环引用问题
root searching 

## 10种垃圾回收器
| 回收器名称| 概述|
|----------|---------|
|Serial、Serial Old              | 会引起 STW ，分代                   |
|Parallel Scavenge、Parallel Old  |会引起STW 目前主要使用的是这种，分代  |
|ParNew、CMS                      |会短暂的引起STW ，分代                |
|G1                               |逻辑上分代，                        |
|ZGC、...                         ||
 

## 回收算法
|算法名称| 应用|
|--------|-----|
|copy | |
|标记清除||
|标记压缩||

## 标记算法

三色标记法
