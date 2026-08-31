---
layout: post
title: "Python命令行编程库——argparse - Honkee"
date: 2015-10-28 00:00:00 +0800
category: legacy
---

这篇文章是基本上是Python Doc[https://docs.python.org/2/howto/argparse.html#id1]的翻译与总结

## 添加参数

#### 定位参数(position argument)
    
    
    import argparse
    parser = argparse.ArgumentParser()
    parser.add_argument("echo")
    args = parser.parse_args()
    print args.echo
    

就是通过`add_argument()`来添加参数 输入的参数默认是字符串，如果你输入的是数字，想解释为数字，那么你就需要在`add_argument()`那里添加一个`type`的参数
    
    
    parser.add_argument("square", help="display a square of a given number",
                        type=int)
    

#### 可选参数

上面那些没有带`--`的参数是必须带有的，在不带那些参数运行不了的。带`--`那些参数则是可选的。 这些不带`--`的参数是，命令行中第几个没有`--`的参数就对应到第几个添加的定位参数。带`--`的参数可以放到任何一个位置。
    
    
    parser.add_argument("--verbosity", help="increase output verbosity")
    
    
    
    parser.add_argument("--verbose", help="increase output verbosity",
                        action="store_true")
    

函数参数那里加了`action="store_true"`这代表着如果添加这个参数代表打开这个开关，不添加这个参数代表关闭这个开关。

#### 可选参数的简单模式
    
    
    parser.add_argument("-v"<center></center>, "--verbose", action="store_true",
                        help="increase output verbosity")
    

#### 参数计数
    
    
    parser.add_argument("-v", "--verbosity", action="count", default=0,
                        help="increase output verbosity")
    

`action="count"`就是用来判断这个参数出现的次数。 我们可以这样使用
    
    
    import argparse
    parser = argparse.ArgumentParser()
    parser.add_argument("square", type=int,
                        help="display a square of a given number")
    parser.add_argument("-v", "--verbosity", action="count",
                        help="increase output verbosity")
    args = parser.parse_args()
    answer = args.square**2
    
    # bugfix: replace == with >=
    if args.verbosity >= 2:
        print "the square of {} equals {}".format(args.square, answer)
    elif args.verbosity >= 1:
        print "{}^2 == {}".format(args.square, answer)
    else:
        print answer
    
    
    
    $ python prog.py 4 -vvv
    the square of 4 equals 16
    $ python prog.py 4 -vvvv
    the square of 4 equals 16
    

#### 高级应用
    
    
    import argparse
    parser = argparse.ArgumentParser()
    parser.add_argument("x", type=int, help="the base")
    parser.add_argument("y", type=int, help="the exponent")
    parser.add_argument("-v", "--verbosity", action="count", default=0)
    args = parser.parse_args()
    answer = args.x**args.y
    if args.verbosity >= 2:
        print "Running '{}'".format(__file__)
    if args.verbosity >= 1:
        print "{}^{} ==".format(args.x, args.y),
    print answer
    

Outut:
    
    
    $ python prog.py 4 2
    16
    $ python prog.py 4 2 -v
    4^2 == 16
    $ python prog.py 4 2 -vv
    Running 'prog.py'
    4^2 == 16
    

## 互斥参数

`parser.add_mutually_exclusive_group()`
    
    
    import argparse
    
    parser = argparse.ArgumentParser()
    group = parser.add_mutually_exclusive_group()
    group.add_argument("-v", "--verbose", action="store_true")
    group.add_argument("-q", "--quiet", action="store_true")
    parser.add_argument("x", type=int, help="the base")
    parser.add_argument("y", type=int, help="the exponent")
    args = parser.parse_args()
    answer = args.x**args.y
    
    if args.quiet:
        print answer
    elif args.verbose:
        print "{} to the power {} equals {}".format(args.x, args.y, answer)
    else:
        print "{}^{} == {}".format(args.x, args.y, answer)
    

Output:
    
    
    $ python prog.py 4 2
    4^2 == 16
    $ python prog.py 4 2 -q
    16
    $ python prog.py 4 2 -v
    4 to the power 2 equals 16
    $ python prog.py 4 2 -vq
    usage: prog.py [-h] [-v | -q] x y
    prog.py: error: argument -q/--quiet: not allowed with argument -v/--verbose
    $ python prog.py 4 2 -v --quiet
    usage: prog.py [-h] [-v | -q] x y
    prog.py: error: argument -q/--quiet: not allowed with argument -v/--verbose
    

* * *

## Comments

Please enable JavaScript to view the [comments powered by Disqus.](http://disqus.com/?ref_noscript) [comments powered by Disqus](http://disqus.com)
