---
layout: post
title: "OpenCV图片处理 - Honkee"
date: 2015-11-11 00:00:00 +0800
category: legacy
---

## opencv读取图片
    
    
    import cv2
    img = cv2.imread('/path/to/image')
    img.shape()
    

out:(heigh,width,color)

## opencv截取图片

图片存储的第一维是图片的高度，第二维是图片的宽度，第三维是图片的颜色维度。所以我们去寻址的时候先对行寻址，再对列寻址。
    
    
    cropImg = img[t:b, l:r]
    

## opencv通道分离、合并

### 分离
    
    
    b, g, r = cv2.split(img)
    

或者用numpy的数组
    
    
    b = np.zeros((img.shape[0],img.shape[1]), dtype=img.dtype)  
    g = np.zeros((img.shape[0],img.shape[1]), dtype=img.dtype)  
    r = np.zeros((img.shape[0],img.shape[1]), dtype=img.dtype)  
    b[:,:] = img[:,:,0]  
    g[:,:] = img[:,:,1]  
    r[:,:] = img[:,:,2]  
    

### 合并
    
    
    nerged = cv2.merge([b, g, r])
    

或者numpy的方法
    
    
    mergedByNp = np.dstack([b, g, r])
    

网上说numpy的组合方法不能用于opencv的其他函数，因为他们的组合方法不一样。[点击这里](http://blog.csdn.net/sunny2038/article/details/9080047 "Title")

但是我做过一个试验显示这两种方法合并得到的结果是一样的。
    
    
    mergedByNp.strides
    out: (1920, 3, 1)
    merged.strides
    out: (1920, 3, 1)
    

* * *

## Comments

Please enable JavaScript to view the [comments powered by Disqus.](http://disqus.com/?ref_noscript) [comments powered by Disqus](http://disqus.com)
