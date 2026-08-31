---
layout: post
title: "VS插件-GetSet生成器 - Honkee"
date: 2015-11-06 00:00:00 +0800
category: legacy
---

Java，C#都有GetSet生成器的方法，而C++却没有这样的工具，即使是现在是有插件做到相应的功能，但是 这个要查一下！！！！！！ 现有的插件做得不够方便，所以我们就做了这个插件。 现在来讲讲这个插件的具体思路。

## 从选择文本中选择变量生成其GetSet方法

#### 文本分割

先将选中的文本分行，我们可以以‘\r\n’来分割。然后对每行进行分割。 我们一般定义变量都是每一行定义一个变量，以分号结束,所以我们可以得到一句中分号前面的那段字符串。 变量类型与变量名称之间隔着空格，所以我们可以用空格去分离变量类型与变量名称，考虑到指针类型（星号与类型之间可以有空格），所以我们的空格从后面开始找。就这样我们就可以将变量类型与变量名称分离出来。我们用得到的变量类型和变量名称就可以生成GetSet方法的字符串。

#### 找到插入点

为了找到GetSet方法的插入点，我们就要遍历整个文件，去寻找每个类对应的public域跟private域。

## 通过填写信息生成GetSet方法

这个要比上面的方法容易一点，我们只需要拼凑GetSet方法字符串，并且找到插入点就可以了。

## 如何去找到合适的插入点

* * *

## Comments

Please enable JavaScript to view the [comments powered by Disqus.](http://disqus.com/?ref_noscript) [comments powered by Disqus](http://disqus.com)
