---
layout: post
title: "学习Numpy"
description: ""
category: python
tags: [python, numpy]
---

# Numpy学习笔记

## 基本操作

#### 1. `arange`: `array`类型的`range`函数

    ```python
    from numpy import *
    
    a = arange(5)
    a
    ```
    ```python
    array([0, 1, 2, 3, 4])
    ```



#### 2. 多维数组，由`array(list)`生成：


    a = array([arange(2), arange(2)]) # 2*2 array
    a




    array([[0, 1],
           [0, 1]])




    b = arange(24).reshape(2, 3, 4) # 2*3*4 array
    b




    array([[[ 0,  1,  2,  3],
            [ 4,  5,  6,  7],
            [ 8,  9, 10, 11]],
    
           [[12, 13, 14, 15],
            [16, 17, 18, 19],
            [20, 21, 22, 23]]])




    c = arange(7, dtype='f') # 指定格式的array， float32
    c




    array([ 0.,  1.,  2.,  3.,  4.,  5.,  6.], dtype=float32)



#### 3. 基本数据属性：`a.dtype`, `a.shape`


    a.dtype




    dtype('int32')




    a.shape




    (2, 2)



#### 4. 数据类型：`sctypeDict.keys()`查看所有数据类型

#### 5. 创建自定义数据类型：


    t = dtype([('name', str_, 40), ('numitems', int32), ('price', float32)])
    itemz = array([('Meaning of life DVD', 42, 3.14), ('Butter', 13, 2.72)], dtype=t)
    itemz




    array([('Meaning of life DVD', 42, 3.140000104904175),
           ('Butter', 13, 2.7200000286102295)], 
          dtype=[('name', 'S40'), ('numitems', '<i4'), ('price', '<f4')])



#### 6. 取子列：与list一样；多维数组分维度取：


    b = arange(24).reshape(2, 3, 4) 
    b[:,1,1]




    array([ 5, 17])



#### 7. 多维数组转成一维：


    b.ravel()




    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
           17, 18, 19, 20, 21, 22, 23])




    b.flatten()




    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
           17, 18, 19, 20, 21, 22, 23])



#### 8. 改变数组形状： `b.shape = (6, 4)`, `b.resize((2, 12))`, `b.transpose() # 转置`8. 

#### 9. 拼接数组：


    a = arange(9).reshape(3,3)
    print 'a = ', a
    b = 2*a
    print 'b = ', b

    a =  [[0 1 2]
     [3 4 5]
     [6 7 8]]
    b =  [[ 0  2  4]
     [ 6  8 10]
     [12 14 16]]
    


    hstack((a, b)) # 水平拼接， a左b右




    array([[ 0,  1,  2,  0,  2,  4],
           [ 3,  4,  5,  6,  8, 10],
           [ 6,  7,  8, 12, 14, 16]])




    concatenate((a, b), axis=1) # 同上




    array([[ 0,  1,  2,  0,  2,  4],
           [ 3,  4,  5,  6,  8, 10],
           [ 6,  7,  8, 12, 14, 16]])




    vstack((a, b)) # 竖直拼接，a上b下




    array([[ 0,  1,  2],
           [ 3,  4,  5],
           [ 6,  7,  8],
           [ 0,  2,  4],
           [ 6,  8, 10],
           [12, 14, 16]])




    concatenate((a, b), axis=0) # 同上




    array([[ 0,  1,  2],
           [ 3,  4,  5],
           [ 6,  7,  8],
           [ 0,  2,  4],
           [ 6,  8, 10],
           [12, 14, 16]])




    dstack((a, b)) # 第3维拼接




    array([[[ 0,  0],
            [ 1,  2],
            [ 2,  4]],
    
           [[ 3,  6],
            [ 4,  8],
            [ 5, 10]],
    
           [[ 6, 12],
            [ 7, 14],
            [ 8, 16]]])




    oned = arange(2)
    oned




    array([0, 1])




    twice = 2 * oned
    twice




    array([0, 2])




    column_stack((oned, twice)) # 按列来拼接




    array([[0, 0],
           [1, 2]])



#### 10. 分割数组


    a




    array([[0, 1, 2],
           [3, 4, 5],
           [6, 7, 8]])




    hsplit(a, 3) # 按行分割，分成的元素是列排列




    [array([[0],
           [3],
           [6]]),
     array([[1],
           [4],
           [7]]),
     array([[2],
           [5],
           [8]])]




    split(a, 3, axis=1) # 同上结果




    [array([[0],
           [3],
           [6]]),
     array([[1],
           [4],
           [7]]),
     array([[2],
           [5],
           [8]])]




    vsplit(a, 3) # 按列分割，分成的元素是行排列




    [array([[0, 1, 2]]), array([[3, 4, 5]]), array([[6, 7, 8]])]




    split(a, 3, axis=0) # 同上




    [array([[0, 1, 2]]), array([[3, 4, 5]]), array([[6, 7, 8]])]




    c = arange(27).reshape(3, 3, 3)
    c




    array([[[ 0,  1,  2],
            [ 3,  4,  5],
            [ 6,  7,  8]],
    
           [[ 9, 10, 11],
            [12, 13, 14],
            [15, 16, 17]],
    
           [[18, 19, 20],
            [21, 22, 23],
            [24, 25, 26]]])




    dsplit(c, 3)  # depth分割， 第3维




    [array([[[ 0],
            [ 3],
            [ 6]],
    
           [[ 9],
            [12],
            [15]],
    
           [[18],
            [21],
            [24]]]),
     array([[[ 1],
            [ 4],
            [ 7]],
    
           [[10],
            [13],
            [16]],
    
           [[19],
            [22],
            [25]]]),
     array([[[ 2],
            [ 5],
            [ 8]],
    
           [[11],
            [14],
            [17]],
    
           [[20],
            [23],
            [26]]])]



#### 11. 数组属性


    b




    array([[ 0,  2,  4],
           [ 6,  8, 10],
           [12, 14, 16]])




    b.ndim # 维度




    2




    b.size # 元素个数




    9




    b.nbytes # 存储所需字节数




    36




    b.size * b.itemsize # 同上




    36




    b.T  # b的转置




    array([[ 0,  6, 12],
           [ 2,  8, 14],
           [ 4, 10, 16]])



#### 12. 复数数组，用`j`表示


    b = array([1.j + 1, 2.j + 3])
    b




    array([ 1.+1.j,  3.+2.j])




    b.real




    array([ 1.,  3.])




    b.imag




    array([ 1.,  2.])



#### 13. flat迭代器(用于遍历所有元素)：


    b = arange(4).reshape(2,2)
    b




    array([[0, 1],
           [2, 3]])




    f = b.flat
    for item in f:
        print item

    0
    1
    2
    3
    

#### 14. 转换array到其他形式


    b.tolist() # 转成list




    [[0, 1], [2, 3]]



## 常用函数


    
