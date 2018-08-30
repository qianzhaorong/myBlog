---
title: Numpy使用
date: 2018-07-14 12:26:07
tags: Python
categories: 学习笔记
---
# 简介

- numpy是科学运算最常见的一个库，支持大量的矩阵运算，是机器学习的基础库。<!--more-->

1.安装

    pip install numpy
    
    
2.numpy基本属性

    import numpy as np
    
    # 将列表转化为矩阵
    array = np.array([[1, 2, 3], [1, 2, 3]])

    # 矩阵的维度
    print("number of dim:", array.ndim)

    # 矩阵的行数和列数
    print("shape:", array.shape)
    
    # 矩阵的size，总共有几个元素
    print("size:", array.size)
    
3.numpy创建array

    import numpy as np
    
    # 创建矩阵
    a = np.array([1, 2, 3])
    
    # 添加矩阵类型，可选参数有np.int32,np.int64,np.float32,float64等
    a = np.array([1, 2, 3], dtype=np.int)
    
    # 生成全部为0的3行4列矩阵
    a = np.zeros( (3, 4) )
    
    # 生成全部为1的3行4列矩阵
    a = np.ones( (3, 4) )
    
    # 生成列表，参数和range()一样
    a = np.arange(10, 20, 2)
    
    # 生成列表后再生成3行4列的矩阵
    a = np.arange(12).reshape( (3, 4) )
    
    # 生成从1到10的4段数列,5个点
    a = np.linspace(1, 10, 5)
    a = np.linsapce(1, 10, 6).reshape( (2, 3) )
    
4.numpy的基础运算

    import numpy as np
    
    # 在numpy中，array的乘法运算和普通列表不同，array的乘法是将每个元素都乘以系数，而列表的乘法是重复
    a = np.array([1, 2])
    # a*2的结果是[1, 4]
    print(a*2)
    
    # sin,cos,tan同样也是对array中每个元素求sin,cos,tan
    c = np.sin(a)
    
    # 判断array中哪些元素的值小于3，返回一个列表类似于[True, False]
    print(a < 3)
    
    # 矩阵的乘法分两种，一种是用*来实现对应元素的相乘，另一种是通过np.dot(a, b)或.dot实现真正的矩阵相乘
    a = np.array([[1, 2], [1, 2]])
    b = np.arange(4).reshape( (2, 2) )
    c = a * b
    c_dot = np.dot(a, b)
    c_dot_2 = a.dot(b)
    
    # 通过np.random.random((a, b))生成一个a行b列的矩阵，矩阵中的每个数都在区间0-1中
    a = np.random.random( (2, 3) )
    
    # np.sum(a, axis=None)不增加axis参数可以计算出这个array中所有元素的和，如果axis=1，求的是每一行的和，axis=0是列的和
    a = np.random.random( (2, 3) )
    print(np.sum(a, axis=0))
    print(np.sum(a, axis=1))
    
    # np.min(a, axis=None)和np.max(a, axis=None)的用法和np.sum(a, axis=None)用法相同
    print(np.min(a, axis=0))
    print(np.max(a, axis=1))
    
    # 通过np.argmin()和np.argmax()获取矩阵的最小值索引和最大值索引
    print(np.argmin(a))
    print(np.argmax(a))
    
    # np.mean()或a.mean()或np.average()计算矩阵的平均值
    print(np.mean(a))
    print(a.mean())
    print(np.average())
    
    # np.median()计算中位数
    print(np.median(a))
    
    # 矩阵的累加，例如矩阵为[[1, 2],[1, 2]]，则累加后的值为[1, 3, 4, 6]
    print(np.cumsum(a))
    
    # 矩阵的累差，算的是每一行的累差
    print(np.diff(a))
    
    # 矩阵的逐行排序
    a = np.arange(14, 2, -1).reshape((3, 4))
    print(np.sort(a))
    
    # 通过np.transpose()或者a.T获得矩阵的转置
    print(np.transpose(a))
    print(a.T)
    
    # 通过np.clip(a, a_min, a_max)来将矩阵中小于a_min的值转化为a_min，大于a_max的值转化为a_max
    print(np.clip(a, 5, 10))
    
5.numpy的索引

    import numpy as np
    
    # 索引的使用和列表相同，如果是二维矩阵，可以通过:来获得某一行或者某一列的所有值
    a = np.arange(3, 15).reshape((3, 4))
    
    # 获得第3行所有值
    print(a[2, :])
    
    # 迭代矩阵的每一行
    for row in a:
        print(row)
        
    # 迭代矩阵的每一列
    for column in a.T:
        print(column)
        
    # 迭代矩阵的每一项
    for item in a.flat:
        print(item)
        
6.numpy array合并

    import numpy as np
    
    A = np.array([1, 1, 1])
    B = np.array([2, 2, 2])
    
    # 将A和B上下合并为一个两行三列的矩阵
    print(np.vstack((A, B)))
    
    # 将A和B左右合并为一个一行六列的序列
    print(np.hstack((A, B)))
    
7.numpy array分割

    import numpy as np
    
    A = np.arange(12).reshape((3, 4))
    
    # 将A在行方向上分割，np.split()不能进行不等的分割
    print(np.split(A, 2, axis=1))
    
    # 使用np.array_split()进行不等的分割
    
    # 使用vsplit()或hsplit()进行纵向或横向的分割
    print(np.vsplit(A, 3))
    print(np.hsplit(A, 2))
    


