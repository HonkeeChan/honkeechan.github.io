---
layout: post
title: "Python Thread - Honkee"
date: 2015-11-13 00:00:00 +0800
category: legacy
---

今天看到这篇文章，关于多线程编程的，感觉这篇文章讲得挺好的。[文章在这里](http://segmentfault.com/a/1190000000414339#articleHeader3)

这篇文章一开始讲了一个生产者消费者的多线程的模型，生产者往队列里添加任务，消费者从队列里取出任务去执行。多线程就相当于多个消费者同时从这个队列里取出任务去完成。

这篇文章讲到了用线程池
    
    
    from multiprocessing import Pool
    pool = Pool()
    pool.map(urllib2.urlopen, urls)
    pool.close()
    pool.join()
    
    
    
    from multiprocessing.dummy import Pool as ThreadPool
    pool = ThreadPool(4) 
    results = pool.map(urllib2.urlopen, urls)
    pool.close() 
    pool.join() 
    

[IBM的一篇关于Python多线程的文章](http://www.ibm.com/developerworks/aix/library/au-threadingpython/) 当线程涉及到共享数据时，我们就可以考虑使用 信号量，条件变量，事件， 锁（semaphores, condition variables, events, and locks）

队列的设计模式使线程编程变得更加简单。使用一个线程安全的队列Queue，我们就可以用多个线程从这个队列中取出任务去完成了。

这篇文章先讲了一个用for循环去打开网址的例子，再用多线程去取得队列打开网址。最后一个例子是通过多线程去打开网址，并将获得的内容放到另一个队列里，供另一个用途（数据挖掘）。

对于线程后面都需要用join去等待线程完成我理解得还不是很清楚。

### 总结

虽然多线程能充分的利用处理器的资源，但是线程的数量对效率的影响也是比较大得。对于计算密集型程序，线程数量不宜太多，这种程序太多的线程会造成过多的线程切换，浪费太多的时间。对于IO密集型程序，线程数量则应该多一些。

* * *

## Comments

Please enable JavaScript to view the [comments powered by Disqus.](http://disqus.com/?ref_noscript) [comments powered by Disqus](http://disqus.com)
