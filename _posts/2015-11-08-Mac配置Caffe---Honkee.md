---
layout: post
title: "Mac配置Caffe - Honkee"
date: 2015-11-08 00:00:00 +0800
category: legacy
---

今天跟着caffe项目的官网向导去安装caffe，前面安装依赖库的时候多次出现下载失败的情况，但是最后在早上再次安装依赖库，貌似每一句都安装成功了。可是到了编译的时候，显示着找不到blas相关字眼的错误信息。 于是我就通过brew这个包管理器去安装blas。
    
    
    brew install blas
    

brew提示错误信息说找不到blas，但提供了相关的包
    
    
    pro:~ honkee$ brew install blas
    Error: No available formula with the name "blas" 
    ==> Searching for similarly named formulae...
    These similarly named formulae were found:
    homebrew/science/blasr                   homebrew/science/rmblast               
    homebrew/science/blast                   homebrew/science/samblaster            
    homebrew/science/clblas                  liblas                                 
    homebrew/science/jblas                   liblastfm                              
    homebrew/science/openblas (installed)    mp3blaster                             
    To install one of them, run (for example):
      brew install homebrew/science/blasr
    ==> Searching taps...
    This formula was found in a tap:
    Caskroom/cask/blast2go
    To install it, run:
      brew install Caskroom/cask/blast2go
    

我选择了openblas
    
    
    brew install openblas
    

安装完openblas之后，需要去修改Makefile.config文件
    
    
    42 # BLAS choice:
    43 # atlas for ATLAS (default)
    44 # mkl for MKL 
    45 # open for OpenBlas
    46 BLAS := open
    
    
    
    53 # Homebrew puts openblas in a directory that is not on the standard search p    ath
    54  BLAS_INCLUDE := $(shell brew --prefix openblas)/include
    55  BLAS_LIB := $(shell brew --prefix openblas)/lib
    

修改了这两处就可以去编译caffe了。 修改这两处的目的是让编译caffe的时候找到blas，还有说明我们用的是openblas。 如果没有说明我们用的是openblas会出现下述错误。
    
    
    caffe ld: framework not found vecLib
    

如果没有说明我们的blas库安装地址，就会显示一些头文件包含错误，找不到blas之类的。

* * *

## Comments

Please enable JavaScript to view the [comments powered by Disqus.](http://disqus.com/?ref_noscript) [comments powered by Disqus](http://disqus.com)
