# 进程、线程 相关知识，待补充......
## 概念
什么是进程，exe load 到内存，分配资源使用 **分配资源的最小单元**

什么是线程，动态的，共享资源，**是CPU 调度的最小单元**

## 为什么存在缓存
CPU 构造 问题 CPU  AUL  REGISTER  PC cache L1 L2 L3 

## 缓存行概念
  一次读取64byte 数据到CPU 缓存中，大小为64byte，可用于优化。

## CPU 乱序执行的证明
通过代码证明，待补充

## 单例 DCL方式，为什么使用 volatile
对象实例化过程，指令重排会导致拿到初始化到一半儿的对象

## volatile 为什么能防止指令重排
内存屏障概念，读屏障，写屏障，
volatile 前后增加了写屏障，在其后面加了读屏障

## 线程池拒绝策略
四种，待补充


## 线程，纤程（用户级别的线程）

## syncronized 锁的升级过程
普通对象（无锁态），偏向锁(百分之七八十的时间都是一个线程在使用) ，轻量级锁（有竞争力，撤销偏向锁，省级为自旋锁），重量级锁（重度竞争，升级为重量级锁，放入队列，自旋锁10次，或者竞争数量超过CPU 核数1/2,AQS）

## 启动偏向锁为什么延迟4s

## 自旋锁一定比重量级锁效率高么？不一定,当某个线程持续拥有锁时，其他线程会耗CPU。

## CAS 乐观锁，通过版本号解决ABA 问题

## 如何保证CAS 原子性？汇编层支持LOCK_IF_MP  lock_cmpxchg原语支持，锁总线。

## new 一个对象由几部分构成（JOL）？ 由四部分构成，markword,class ponitor,instance data,padding。

## markword 中存储的是啥？锁信息，GC 信息，hashcode。

## synchronized 是可重入锁
 CAS  用户态，内核态
0X80 问题

## 启动线程池的三种方式  1. thread 2. runnable 3. 线程池Executors.newCache 4. lamada 表达式

## 线程的状态， https://www.bilibili.com/video/BV1Ph411v71Y?p=18&spm_id_from=pageDriver

## 异常跟锁，出现异常，释放锁

加锁： synchronized  volatile  atomic  increment  longAdder
新类型锁：  reentrantLock  CountDoenLatch   CyclicBarrier Pahser ReadWriteLock Semaphore Exchaner 


# 线程池
参考: 

[Java-五种线程池，四种拒绝策略，三种阻塞队列](https://www.bbsmax.com/A/D854Dvap5E/)

[JAVA_线程池—7个参数-4种拒绝策略](https://www.freesion.com/article/5194525291/)

[java线程池的拒绝策略](https://www.jianshu.com/p/f0506e098c5b)

[Java多线程面试题](https://www.jianshu.com/p/2078db07e0c9)

[juc](https://www.jianshu.com/p/1f19835e05c0)

Thread的.start()与.run()的区别

三种阻塞队列：
    BlockingQueue<Runnable> workQueue = null;
    workQueue = new ArrayBlockingQueue<>(5);//基于数组的先进先出队列，有界
    workQueue = new LinkedBlockingQueue<>();//基于链表的先进先出队列，无界
    workQueue = new SynchronousQueue<>();//无缓冲的等待队列，无界
四种拒绝策略：
    RejectedExecutionHandler rejected = null;
    rejected = new ThreadPoolExecutor.AbortPolicy();//默认，队列满了丢任务抛出异常
    rejected = new ThreadPoolExecutor.DiscardPolicy();//队列满了丢任务不异常
    rejected = new ThreadPoolExecutor.DiscardOldestPolicy();//将最早进入队列的任务删，之后再尝试加入队列
    rejected = new ThreadPoolExecutor.CallerRunsPolicy();//如果添加到线程池失败，那么主线程会自己去执行该任务
五种线程池：
    ExecutorService threadPool = null;
    threadPool = Executors.newCachedThreadPool();//有缓冲的线程池，线程数 JVM 控制
    threadPool = Executors.newFixedThreadPool(3);//固定大小的线程池
    threadPool = Executors.newScheduledThreadPool(2);
    threadPool = Executors.newSingleThreadExecutor();//单线程的线程池，只有一个线程在工作
    threadPool = new ThreadPoolExecutor();//默认线程池，可控制参数比较多
