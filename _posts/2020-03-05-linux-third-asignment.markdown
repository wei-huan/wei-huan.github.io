---
layout: post
title: linux third assignment 
date: 2020-03-05 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: how-to-start.jpg # Add image post (optional)
tags: [Programming, Learn] # add tag
---












## 概念理解



1.cpu:中央处理单元，由储存单元，算数逻辑单元（ALU），寄存器等封装组成的计算机运算中心，负责处理计算机指令，是计算机的大脑，核心 。

2.核心（kernel）：linux操作系统中负责管理内存资源，进程，权限，用户，文件等的一系列程序，是连通计算机的硬件及软件的核心部分。  。。。

3.超线程技术：英特尔开发的在一个单核心实体CPU中，提供两个逻辑线程，去模拟出双核心的环境的技术。该技术可以缩短流水线，提高操作系统的资源利用率。

4.进程：UNIX操作系统下运行的应用程序、服务器及其他程序都称为进程。

5.线程：是一种轻量式的进程，也可以是一个进程中特定的部分。在Linux内核中，线程和一般进程之间的差别不是那么刚性，这两个名词经常用 作同义词。

6.并行：并行是计算机系统中能同时执行两个或多个处理的一种计算方法。并行处理可同时工作于同一程序的不同方面。并行处理的主要目的是节省大型和复杂问题的解决时间。但有依赖关系的线程无法做到并行。

7.操作系统是如何进行进程切换的:进程的运行按时间片调度，分配给进程的时间片份额与 其相对重要性相当。系统中时间的流动对应于圆盘的转动，而CPU则由圆周旁的“扫描器”表示。 终效果是，尽管所有的进程都有机会运行，但重要的进程会比次要的得到更多的CPU时间。当一个进程处理时间达到时间片，会被操作系统暂停，收回控制权，其页表cpu寄存器内容和页表会被保存。在上下文切换时，cpu资源会提供给下一个进程，直到其cpu时间达到时间片，如此反复循环。这种方案也称为抢占式多任务处理。

8.让用户感觉多个任务是在”同时执行“的原理：这是通过以很短的间隔在系统运行 的应用程序之间不停切换而做到的。由于切换间隔如此之短，使得用户无法注意到短时间内的停滞， 从而在感观上觉得计算机能够同时做几件事情。

9.互斥：有些资源只能被一个进程，不能同时被多个进程访问，这种资源区域称为临界区域。访问两个或两个以上的进程，不能同时进入关于同一组共享变量的临界区域，否则可能发生与时间有关的错误，这种现象被称作进程互斥。比如说同时需要打印机打印的两个进程就会形成互斥。

10.加锁：有些文件资源被同时访问的进程数量有限制，加锁是防止多个进程同时访问一个资源的机制。

11.死锁：两个互相依赖的进程同时进入等待状态，无法被cpu处理，形成一个死循环的状态。

12.守护进程：守护进程是一个在后台运行并且不受任何终端控制的进程,其生命周期一般为系统启动到系统停止运行。





## 线程交互打印代码(C语言)

```c

```

\#include<pthread.h>

\#include<stdio.h>



void* printsingularnumber()         //打印单数天数线程

{

​    for (int i = 1; i < 50; i+=2)

​    {

​        printf("因疫情不能开学的第%d天\n",i);



​        sleep(2);               //让本线程睡眠挂起，交出cpu资源

​    }

​    

}



void* printevennumber()         //打印双数天数线程

{

​    for (int i = 2; i < 51; i+=2)

​    {

​        printf("因疫情不能开学的第%d天\n",i);



​        sleep(2);               //让本线程睡眠挂起，交出cpu资源

​    }

}



int main()

{

​    pthread_t id1,id2;          //定义两个线程的id

​    int i=0;

​    int ret=0;



​    ret=pthread_create(&id1,NULL,(void *)printsingularnumber,NULL);

​    if(ret)

​    {

​        printf("Create pthread error!\n");

​        return -1;

​    }



​    ret=pthread_create(&id2,NULL,(void *)printevennumber,NULL);

​    if(ret)

​    {

​        printf("Create pthread error!\n");

​        return  -1;

​    }



​    //检查线程是否创建成功



​    pthread_join(id1,NULL);

​    pthread_join(id2,NULL);



​    return 0;

}

```c

```



