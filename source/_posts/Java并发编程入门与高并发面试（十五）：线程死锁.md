---
title: Java并发编程入门与高并发面试（十五）：线程死锁
categories:
  - 高并发
abbrlink: 11129fd3
date: 2018-09-14 22:30:33
tags:
---

摘要：如题。

<!--more-->

------

### 什么是死锁？

通俗的说，死锁就是两个或者多个线程，相互占用对方需要的资源，而都不进行释放，导致彼此之间都相互等待对方释放资源，产生了无限制等待的现象。死锁一旦发生，如果没有外力介入，这种等待将永远存在，从而对程序产生严重影响。 
用来描述死锁的问题最有名的场景就是“哲学家就餐问题”。哲学家就餐问题可以这样表述：假设有五位哲学家围坐在一张圆形餐桌旁，做以下两件事之一：吃饭或者思考。吃东西的时候他们就停止思考，思考的时候也停止吃东西。餐桌中间有一大碗意大利面，每两个哲学家之间有一只餐叉。因为只用一只餐叉很难吃到意大利面，所以假设哲学家必须用两只餐叉吃东西。他们只能使用自己左右手边的那两只餐。哲学家从来不交谈，这就跟危险，可能产生死锁，每个哲学家都拿着左手的餐叉永远等右边的餐叉（或者相反）….

### 死锁产生的必要条件

- 互斥条件：进程对锁分配的资源进行排他性使用
- 请求和保持条件：线程已经保持了一个资源，但是又提出了其他请求，而该资源已被其他线程占用
- 不剥夺条件：在使用时不能被剥夺，只能自己用完释放
- 环路等待条件：资源调用是一个环形的链

### 死锁示例

```
@Slf4j
public class DeadLock implements Runnable {
    public int flag = 1;
    //静态对象是类的所有对象共享的
    private static Object o1 = new Object(), o2 = new Object();

    @Override
    public void run() {
        log.info("flag:{}", flag);
        if (flag == 1) {
            synchronized (o1) {
                try {
                    Thread.sleep(500);
                } catch (Exception e) {
                    e.printStackTrace();
                }
                synchronized (o2) {
                    log.info("1");
                }
            }
        }
        if (flag == 0) {
            synchronized (o2) {
                try {
                    Thread.sleep(500);
                } catch (Exception e) {
                    e.printStackTrace();
                }
                synchronized (o1) {
                    log.info("0");
                }
            }
        }
    }

    public static void main(String[] args) {
        DeadLock td1 = new DeadLock();
        DeadLock td2 = new DeadLock();
        td1.flag = 1;
        td2.flag = 0;
        //td1,td2都处于可执行状态，但JVM线程调度先执行哪个线程是不确定的。
        //td2的run()可能在td1的run()之前运行
        new Thread(td1).start();
        new Thread(td2).start();
    }
}12345678910111213141516171819202122232425262728293031323334353637383940414243444546
```

上述代码出现死锁原因：

- 当DeadLock类的对象flag==1时（td1），先锁定o1,睡眠500毫秒
- 而td1在睡眠的时候另一个flag==0的对象（td2）线程启动，先锁定o2,睡眠500毫秒
- td1睡眠结束后需要锁定o2才能继续执行，而此时o2已被td2锁定；
- td2睡眠结束后需要锁定o1才能继续执行，而此时o1已被td1锁定；
- td1、td2相互等待，都需要得到对方锁定的资源才能继续执行，从而死锁。

### 确认死锁

在真实的环境中，我们发现程序无法执行，并且CPU占用为0，这样就有理由怀疑产生了死锁，但是光怀疑是不行的，我们需要一个实际的验证方法。接下来我们使用jdk提供的工具来检测是否真正发生了死锁。 
运行上述的代码，并在windows系统中使用cmd进入控制台，输入以下命令：

```
jps1
```

可见控制台输出：我们上边运行的类的类名以及对应的进程ID 
![这里写图片描述](https://img-blog.csdn.net/20180508114816478?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2plc29uam9rZQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70) 
接下来使用命令获取进程对应线程的堆栈信息：

```
jstack 9284 1
```

分析堆栈信息（提取有用的部分） 
![这里写图片描述](https://img-blog.csdn.net/20180508115133940?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2plc29uam9rZQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
两个线程都进行了加锁操作（如上图） 
![这里写图片描述](https://img-blog.csdn.net/20180508115247704?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2plc29uam9rZQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70) 
系统发现了一个Java-level的线程死锁。ok，确认无疑是发生了死锁现象。

### 避免死锁

- 注意加锁顺序（这个很好理解，就像上边的例子）
- 加锁时限（超过时限放弃加锁） 
  实现方式–使用重入锁。关于重入锁可以见我之前的博客：[并发容器J.U.C – AQS组件 锁：ReentrantLock、ReentrantReadWriteLock、StempedLock](https://blog.csdn.net/jesonjoke/article/details/80058631)
- 死锁检测（较难，就像分析上边的线程情况）

经作者授权转载，原文地址：https://blog.csdn.net/jesonjoke/article/details/80233899