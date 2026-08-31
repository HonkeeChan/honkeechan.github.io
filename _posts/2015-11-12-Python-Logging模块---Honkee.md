---
layout: post
title: "Python Logging模块 - Honkee"
date: 2015-11-12 00:00:00 +0800
category: legacy
---

### logger的Level
    
    
    logger.setLevel()
    

设置logger的level，level有以下几个级别 NOTSET < DEBUG < INFO < WARNING < ERROR < CRITICAL 如果把looger的级别设置为INFO， 那么小于INFO级别的日志都不输出， 大于等于INFO级别的日志都输出

### logger的处理器
    
    
    logger.addHandler()
    

logger可以雇佣handler来帮它处理日志， handler主要有以下几种：

  * StreamHandler: 输出到控制台
  * FileHandler: 输出到文件



handler还可以设置自己的level以及输出格式。

### 将logger封装起来方便使用

这个logger类具有控制台，文件同时输出的功能，使用方法如下
    
    
    import logging
    
    class MyLogging:
        def __init__(self, loggerName = 'mylog', fileName = 'log.txt'):
            self.logger = logging.getLogger(loggerName)  
            self.logger.setLevel(logging.DEBUG)         
            # 创建一个handler，用于写入日志文件  
            fh = logging.FileHandler(fileName)  
            fh.setLevel(logging.DEBUG)  
            # 再创建一个handler，用于输出到控制台  
            ch = logging.StreamHandler()  
            ch.setLevel(logging.DEBUG)          
            # 定义handler的输出格式  
            formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')  
            fh.setFormatter(formatter)  
            ch.setFormatter(formatter)          
            # 给logger添加handler  
            self.logger.addHandler(fh)  
            self.logger.addHandler(ch) 
    if __name__ == '__main__':
        logger = MyLogger('hello_log', 'main.log').logger
        logger.info('info message')
        logger.debug('debug message')
        logger.warning('warning message')
        logger.critical('critical message')
    

* * *

## Comments

Please enable JavaScript to view the [comments powered by Disqus.](http://disqus.com/?ref_noscript) [comments powered by Disqus](http://disqus.com)
