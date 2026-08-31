---
layout: post
title: "Python小技巧 - Honkee"
date: 2015-10-27 00:00:00 +0800
category: legacy
---

## 创建目录
    
    
    os.mkdir( path [,mode] )
    

作用：创建一个目录，可以是相对或者绝对路径，mode的默认模式是0777。 如果目录有多级，则创建最后一级。如果最后一级目录的上级目录有不存在的，则会抛出一个`OSError`。
    
    
    os.makedirs( path [,mode] )
    

作用： 创建递归的目录树，可以是相对或者绝对路径，mode的默认模式也是0777。 如果子目录创建失败或者已经存在，会抛出一个`OSError`的异常，Windows上Error 183即为目录已经存在的异常错误。如果path只有一级，与mkdir一样。
    
    
    try:
            os.makedirs(path)
    except OSError as exc:  
            if exc.errno == errno.EEXIST and os.path.isdir(path):
                pass
            else:
                raise
    

## 遍历目录

os.listdir()不能对文件名进行筛选，只能在获取文件之后再对其进行筛选

### glob模块

glob模块是最简单的模块之一，内容非常少。用它可以查找符合特定规则的文件路径名。跟使用windows下的文件搜索差不多。查找文件只用到三个匹配符：” _”, “?”, “[]“。”_ ”匹配0个或多个字符；”?”匹配单个字符；”[]“匹配指定范围内的字符，如：[0-9]匹配数字。
    
    
    import glob
    print glob.glob(r"E:/Picture/*/*.jpg")
    

## 参数编程

### argparse

看我另一篇博文

## 匿名函数lambda
    
    
    In [5]: points = [ (1,2), (2,3)]
    
    In [6]: min(points, key=lambda (x, y): (x*x + y*y))
    Out[6]: (1, 2)
    
    
    
    >>> min(points, key=lambda p: p[0]*p[0] + p[1]*p[1])
    (1, 2)
    

## map

map(function, sequence[, sequence, ...]) -> list

Return a list of the results of applying the function to the items of the argument sequence(s). If more than one sequence is given, the function is called with an argument list consisting of the corresponding item of each sequence, substituting None for missing values when not all sequences have the same length. If the function is None, return a list of the items of the sequence (or a list of tuples if more than one sequence).
    
    
    points = [ (1,2), (2,3), (5,6)]
    
    
    
    In [12]: map(lambda p: (p[0], p[1]), points)
    Out[12]: [(1, 2), (2, 3), (5, 6)]
    
    
    
    In [13]: map(lambda p: [p[0], p[1]], points)
    Out[13]: [[1, 2], [2, 3], [5, 6]]
    
    
    
    In [15]: map(lambda p: [p[0]< p[1]], points)
    Out[15]: [[True], [True], [True]]
    

## zip

zip(seq1 [, seq2 [...]]) -> [(seq1[0], seq2[0] ...), (...)]

Return a list of tuples, where each tuple contains the i-th element from each of the argument sequences. The returned list is truncated in length to the length of the shortest argument sequence.
    
    
    In [31]: threepoint1
    Out[31]: [(1, 2, 3), (4, 5, 6), (7, 8, 9), (10, 11)]
    
    In [32]: zip(*threepoint1)
    Out[32]: [(1, 4, 7, 10), (2, 5, 8, 11)]
    
    
    
    In [28]: threepoint = [(1,2,3),(4,5,6),(7,8,9),(10,11,12)]
    
    In [29]: zip(*threepoint)
    Out[29]: [(1, 4, 7, 10), (2, 5, 8, 11), (3, 6, 9, 12)]
    

不明白这个为什么
    
    
    In [30]: zip(threepoint)
    Out[30]: [((1, 2, 3),), ((4, 5, 6),), ((7, 8, 9),), ((10, 11, 12),)]
    

* * *

## Comments

Please enable JavaScript to view the [comments powered by Disqus.](http://disqus.com/?ref_noscript) [comments powered by Disqus](http://disqus.com)
