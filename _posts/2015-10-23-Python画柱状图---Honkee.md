---
layout: post
title: "Python画柱状图 - Honkee"
date: 2015-10-23 00:00:00 +0800
category: legacy
---

> 统计数组频数的方法
    
    
    import numpy as np
    def GetBarFrequency(arr, barTotal, minNum = None, maxNum = None):
        #没有自定义最大最小值则用数组计算最大最小值
        if not maxNum:
            maxNum = max(arr)
        if not minNum:
            minNum = min(arr)
        interval = (maxNum - minNum) / barTotal
        #定义多一个元素，后面就会发现它的作用
        barCntArr = np.zeros(barTotal + 1, dtype='int')
        for item in arr:
            barIndex = int((item - minNum) / interval)
            barCntArr[barIndex] += 1
        #我们肯定会有至少一个数刚好等于barTotal，所以数组会越界，上面数组定义了多一个元素，多出来的这个元素的统计值应该是归入第barTotal个元素即barCntArr[barTotal - 1]中
        barCntArr[barTotal - 1] += barCntArr[barTotal]
        #drop last one
        barCntArr = barCntArr[0: -1]
        coordinats = [minNum + i * interval for i in range(barTotal)]
        return (barCntArr, coordinats)
    

> 画柱状图

Matplotlib是一个Python的图形框架，类似于MATLAB和R语言。Matplotlib的官网地址是 http://matplotlib.org/
    
    
    import numpy as np
    import matplotlib.pyplot as plt
    
    barTotal = 7
    barCntArr1 = np.array([2, 3, 4, 1, 1, 2, 1])
    barCntArr2 = np.array([1, 2, 3, 1, 1, 3, 2])
    
    width = 0.35
    ind = np.arange(barTotal)
    fig, ax = plt.subplots()
    rects1 = ax.bar(ind, barCntArr1, width, color='r')
    rects2 = ax.bar(ind + width, barCntArr2, width, color='b')
    
    ax.set_ylabel('y_label')
    ax.set_title('title')
    ax.set_xlabel('x_label')
    ax.set_xticks(ind+width)
    interval = 1.1
    ax.set_xticklabels( [i * interval for i in range(7)] )
    ax.legend( (rects1[0], rects2[0]), ('red', 'blue') )
    
    plt.show()
    

运行上面代码，执行后如下图所示

![plot.png](/images/plot.png)

* * *

## Comments

Please enable JavaScript to view the [comments powered by Disqus.](http://disqus.com/?ref_noscript) [comments powered by Disqus](http://disqus.com)
