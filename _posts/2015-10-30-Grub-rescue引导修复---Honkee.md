---
layout: post
title: "Grub rescue引导修复 - Honkee"
date: 2015-10-30 00:00:00 +0800
category: legacy
---

我电脑上装着3个系统，一个windows 7，一个Kali linux，一个Ubuntu 14.04。今天将Kali linux删了，系统就进不去了。百度了一阵才能将系统找回来。 首先ls查看一下自己硬盘上的分区。因为我删了Kali linux的分区，所以现在剩下两个分区，这两个分区是Windows的C盘，Ubuntu的根目录. 第二句是设置根目录， 第三句是告诉grub，grub2在哪个位置 第四句是加载normal.mod这个模块，这个模块就是正常启动的模块，里面的菜单项就是grub.cfg（在/boot/grub/grub.cfg）。 第五句就可以出现正常启动的菜单了。
    
    
    grub rescure>ls
    (hd0)(hd0,msdos1)(hd0,msdos2) ...
    grub rescure>set root=(hd0,msdos2)
    grub rescure>set prefix=/boot/grub
    grub rescure>insmod /boot/grub/i386-pc/normal.mod
    grub rescure>normal
    

这样是可以进入grub的菜单选选择了，可是还没有将引导写到MBR上，所以下次启动还会进入grub rescue。所以还要将引导写到MBR上。 那我们既然有Ubuntu就不需要Ubuntu的安装盘了，我们先由上面进入的引导菜单项进入Ubuntu了。 具体的可以看我的一篇CSDN博客有写。[点击这里](http://blog.csdn.net/honkee_/article/details/39933115)

* * *

## Comments

Please enable JavaScript to view the [comments powered by Disqus.](http://disqus.com/?ref_noscript) [comments powered by Disqus](http://disqus.com)
