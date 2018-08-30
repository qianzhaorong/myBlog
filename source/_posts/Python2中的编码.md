---
title: '''Python2中的编码'''
date: 2018-08-01 09:14:07
tags: Python
categories: 学习笔记
---
### 一、简介

- 字符编码总是Python2和Python3中老生常谈的话题，不管是在处理字符转码或是写爬虫的过程中都很有可能触碰这一雷区。今天来聊聊我对字符编码的理解。<!--more-->

### 二、字符和字节

- 在说编码问题之前，首先来了解一下字符和字节的区别。字符不同于字节，字符是人类能够识别的符号，而这些符号要保存到计算机中，就需要转化为字节形式，一个字符在内存中往往有多种表示方法，不同的表示方法会使用不同的字节数，这里的表示方法就是编码。

### 三、常用的几种编码

- ASCII编码：由美国国家标准学会（ANSI）制定的，使用7位或8位二进制的组合来表示128或256种可能的字符，能够处理所有的英文字母。

- GB2312编码：中国规定的汉字编码，也可以说是简体中文的字符集编码，两个字节编码字符

- GBK编码：是GB2312的扩展，还能显示繁体中文

- Unicode：把所有语言都统一到一套编码里，俗称万国码

- Utf-8编码：可变长的编码，把一个Unicode字符根据不同的数字大小编码成1-6个字节，常用的英文字母被编码成1个字节，汉字通常是3个字节。能够节省空间

### 四、Python2中的编码

```
a = '你好'
print a
```

上面这段代码在Pycharm中保存为test.py以python2.7来执行，会报如下错误：
![image](https://note.youdao.com/yws/api/personal/file/2A1C8338139348BF9D1232A89949D0D2?method=download&shareKey=e57bd80dd8d3cee69ccadfbd9c80c862)
为什么会出现这个错误呢？原因是代码中有中文字符，但是Python2解释器默认以ASCII来解释代码，所以没有办法解释中文。

如何解决这个问题呢？只需要在代码的第一行加上
```
# coding:utf-8
```

接着我们将加上了头部声明的test.py在windows终端下运行看看：
![image](https://note.youdao.com/yws/api/personal/file/C6E85D16EFAA41F2A0745BDF9AE6E3CA?method=download&shareKey=2863626e6224cbd04edf06e58bed591a)

竟然出现了乱码？？？为什么相同的代码在Pycharm中运行和在windows终端中运行不一样呢？

这就要从代码的执行过程说起：

    1.我们在写python代码时，这些代码会被转化为unicode字符串存放在内存中，而一旦我们保存，这些代码会以utf-8编码的方式转化为二进制存放的硬盘上。
    
    2.在执行保存的代码时，这一步在python2和python3中有很大的差异，在python3中，代码从硬盘到内存中运行会自动转为unicode，而在python2中，并不会转，也就是python2的解释器直接以声明的编码方式来解释代码。当遇到上面的代码中的赋值操作时，会将'你好'以头部声明的utf-8编码转化为字节串存储。
    
    3.当我们使用print语句时，如果遇到的是unicode字符串，会直接输出，而如果遇到的是字节串，则会自动以终端的编码方式解码成unicode后再输出。
    
所以上面代码在终端输出乱码的原因就是utf-8编码的'你好'在print时以gbk(windows默认编码)来解码了，所以出现了乱码。

当我们把头部的声明改为gbk，在win终端执行就正常了，但是在Pycharm中就乱码了，所以有没有好的解决方式呢？

既然我们知道python2并不会把代码转化为unicode再进行解释，那我们就自己转！

```
# coding:utf-8
a = '你好'
print a.decode('utf-8')
```

这下在输出之前，a这个变量的值已经是unicode了，不论是在Pycharm中还是在终端中都能够正常输出了。

关于Python2的基本编码解码的简单思路大致如上，再来总结一下：

    1.Python2的默认编码为ascii，默认编码的作用是python2的解释器默认以ascii的编码方式来解释代码，所以如果出现中文就没有办法解释，必须在头部声明其它编码方式。关于这里的编码还有另外一个作用，就是在解释代码时如果出现中文字符，会以声明的编码方式来将字符编码为字节存在内存中。
    
    2.windows终端的编码为gbk，Pycharm的编码为utf-8
    
    3.python2的字符串类型有两种：str和unicode，这里的str是字节串，而unicode才是真正的字符串。
    
    4.encode和decode之间的转化：
    
        unicode----encode------utf-8/gbk
        utf-8/gbk------decode-----unicode


### 五、Python3中的编码

因为Python2的编码让人头大，所以Python3在设计的时候就以utf-8为默认编码，这就解决了很多的问题，同时在python3中也没有了str和unicode这种让人不能理解的类型。在python3中，字符串默认都是str类型，而bytes类型就是二进制。


### 六、其它
在python2中都能遇到这样一个问题----打印出的列表或字典中中文是unicode类型，这里提供一个解决方法：

```
# coding:utf-8
a = [u'\u4f60\u597d']

print a

b = str(a).decode('unicode-escape')

print b
```

