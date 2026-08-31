---
layout: post
title: "dlib to face align using python - Honkee"
date: 2015-10-27 00:00:00 +0800
category: legacy
---

## 人脸特征点检测
    
    
    predictor_path = 'path/to/shape_predictor_68_face_landmarks.dat'
    img = 'the/face/you/want/to/predict'
    
    detector = dlib.get_frontal_face_detector()
    predictor = dlib.shape_predictor(predictor_path)
    
    dets = detector(img, 1)
    shape = predictor(img, d)
    

> get_frontal_face_detector

detector返回的dets是识别出人脸区域对应的矩形。 第二个参数1，表示将图片放大（upsample）1倍，这是为了使图片中的东西更大，更利于我们检测人脸

> shape_predictor

predictor的输入参数d是代表从d这个矩形范围内找landmark。 predictor返回的shape就是检测出的68个特征点(face_landmarks)，我们可以调用shape.part(0) ... shape.part(67)得到每一个特征点对应的坐标。

## Affine Transform

![](/images/Affine_Transform_Matrix.png) ![](/images/Warp_Affine_Tutorial_Theory.jpg) 通过函数getAffineTransform得到A状态到B状态的转换矩阵 再调用warpAffine将图片做Affine Transform.
    
    
    statusA = [(beforeA.x, beforeA.y),(beforeB.x, beforeB.y),(beforeC.x, beforeC.y)]
    statusB = [(afterA.x, afterA.y),(afterB.x,afterB.y),(afterC.x, afterC.y)]
    
    H = cv2.getAffineTransform(stautsA, stautsB)
    warpedImg = cv2.warpAffine(img, H, np.shape(img)[0:2])
    

还有`cv2.getRotationMatrix2D(center, angle, scale)`是得到一个旋转angle度的Affine Transform Matrix。

## openface的face align

Github上有一个实现FaceNet的开源代码openface，它是先face align，然后用对齐后的人脸输入FaceNet得到特征，然后求其欧式距离得到两张图片的差异。 其中人脸对齐部分代码的思想是：  
1.得到face landmark  
2.将眼睛，鼻尖这三点通过Affine Transform映射到三个点，然后对整张图片进行Affine Transform.  
3.再计算face landmark，求face landmark的所有点的外接矩形为裁剪后的对齐人脸。  


* * *

## Comments

Please enable JavaScript to view the [comments powered by Disqus.](http://disqus.com/?ref_noscript) [comments powered by Disqus](http://disqus.com)
