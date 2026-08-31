---
layout: post
title: "Face Landmark Lib - Honkee"
date: 2015-11-09 00:00:00 +0800
category: legacy
---

最近在刷微博的时候发现了一个人脸特征点检测的库——CLM Framework，之前用过Dlib做人脸特征点检测，觉得准确率还是相当可观的。现在找到CLM Framework这个库，感觉准确率应该也不错，它还提供认的头部朝向，感觉应用它的地方会更广。

### CLM Framework

**function:** face landmark and head pose estimation

C++开发的，[Github](https://github.com/TadasBaltrusaitis/CLM-framework "Title")上有个VS项目。

### Dlib

**function:** face landmark 

C++写的库，有C++接口和Python接口。

### Application

  * 化妆

通过获得face landmark，对眼睛附近区域和嘴唇附近区域进行一些颜色的处理，就相当于后期化妆~ ![alt text](/images/taaz-before-after.jpg)

  * 换人脸

  * 人脸特征检测和人脸追踪
  * 人脸对齐



通过Affine Transform将人脸的多个特征点映射到一个固定的地方，这样做有利于提高人脸识别的准确率。

通过Delaunay triangulation和Voronoi Diagram对识别出来的特征点进行分割，我还不知道这个有什么用。

![alt text](/images/opencv-delaunay-vornoi-subdiv-example.jpg) Figure 1. Left : Image of President Obama with landmarks detected using dlib. Center : Delaunay triangulation of the landmarks. Right : Corresponding Voronoi Diagram.

* * *

## Comments

Please enable JavaScript to view the [comments powered by Disqus.](http://disqus.com/?ref_noscript) [comments powered by Disqus](http://disqus.com)
