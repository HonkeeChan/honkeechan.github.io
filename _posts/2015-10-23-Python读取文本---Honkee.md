---
layout: post
title: "Python读取文本 - Honkee"
date: 2015-10-23 00:00:00 +0800
category: legacy
---

## 读取文件

Python 将文本文件的内容读入可以操作的字符串变量非常容易。文件对象提供了三个“读”方法： `.read()`，`.readline()` 和 `.readlines()`。

`.read()`和 `.readlines()`都是读取整个文件的，对于大文件来说，一次性将大文件放到内容比较吃力，可以用 `.readline()`一行一行的读入处理。

> code 1:
    
    
    f = open(filename)
    for line in f:
        print line
    

> code 2:
    
    
    f = open(filename)
    for line in f.readlines():
        print line
    

code 1，2都是一样的功能。 f就是一个文件，`print f`会输出`<open file 'test.txt', mode 'r' at 0x030908B8>`之类的信息，但是用for循环却可以得到这个文件的每一行元素。 `.readline()`是将文件的每一行作为一个字符串，作为数组的一个元素，整个文件就是一个字符串数组。

> code 3:
    
    
    f = open(filename)
    for line in f.read():
        print line
    

code 3是将整个文件读成一个字符串。

> code 4
    
    
    f = open(filename)
    line = f.readline()
    while line != "":
        print line
        line = f.readline()
    

code 4与code 1-2结果是一样的。

## 字符串处理

我们在读到的一行信息往往有些是我们不需要的信息。比如说最后的换行符'\n'我们不想要。那么我们可以用python自带的str函数来进行一些处理
    
    
    line = line.strip('\n')
    

这样就将最后的'\n'去掉了。或者我们想对我们的字符串进行分块,比如说我们用空格进行分块，我们得到的words是一个数组，每个元素就是由空格切开的一个字符串。
    
    
    line = 'i like using python'
    words = line.split(' ')
    

得到的words是一个4个单词的数组。这是一个比较简单的切割方法，如果line中含有两个空格，我们得到的words就不是我们想要的结果了。

## 字符串高级处理

* * *

## Comments

Please enable JavaScript to view the [comments powered by Disqus.](http://disqus.com/?ref_noscript) [comments powered by Disqus](http://disqus.com)
