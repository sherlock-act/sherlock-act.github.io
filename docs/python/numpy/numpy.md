# Numpy

## 什么是numpy

​     一个在Python中做科学计算的基础库，重在数值计算，也是大部分PYTHON科学计算库的基础库，多用于在大型、多维数组上执行数值运算

## numpy基础

- 创建数组

```python
import numpy as np

# 使用numpy生成数组，得到ndarray类型的类型
t1 = np.array([1, 2, 3])

print(t1)
print(type(t1))


t2 = np.array(range(10))
print(t2)
print(t2.dtype)


t3 = np.arange(4, 10, 2)
print(t3)
# t3.dtype 是数组中存储数据的类型
print(t3.dtype)

# 使用dtype参数来制定创建数据的类型
t4 = np.arange(10, dtype=float)
# t4 = np.arange(10, dtype="float32")
# t4 = np.arange(10, dtype="i1")
print(t4)
print(t4.dtype)

# numpy中的bool类型
t5 = np.array([1,1,1,1,0,0,0], dtype=bool)
print(t5)
print(t5.dtype)

# 改变数据类型
t6 = t5.astype("int8")
print(t6)
print(t6.dtype)

# numpy中的小数
t7 = np.array([random.random() for i in range(10)])
print(t7)
print(t7.dtype)

# 修改小数显示位数
t8 = np.round(t7,2)
print(t8)
```

- numpy的数据类型

![numpy数据类型](images\numpy数据类型.png)

## numpy的形状

![数组的形状](images\数组的形状.png)

![数组的形状2](images\数组的形状2.png)

```python
In [1]: import numpy as np

In [2]: t1 = np.arange(12)

In [3]: t1
Out[3]: array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11])

# t1就是一维数组
In [4]: t1.shape
Out[4]: (12,)

In [5]: t2 = np.array([[1,2,3],[4,5,6]])

In [6]: t2
Out[6]:
array([[1, 2, 3],
       [4, 5, 6]])

# shape查看数组的形状
# t2这种就是二维数组
In [7]: t2.shape
Out[7]: (2, 3)
  

# t3就是三维数组
In [13]: t3 = np.array([[[1,2,3],[4,5,6]],[[7,8,9,],[10,11,12]]])

In [14]: t3
Out[14]:
array([[[ 1,  2,  3],
        [ 4,  5,  6]],

       [[ 7,  8,  9],
        [10, 11, 12]]])

In [15]: t3.shape
Out[15]: (2, 2, 3)
    
    
# 修改数组的形状 reshape可以改变数组的形状 注意 总的数据个数不能变
In [16]: t4 = np.arange(12)

In [17]: t4
Out[17]: array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11])

In [18]: t4.reshape((3,4))
Out[18]:
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11]])

# flatten可以将多维数组转为一维数组

In [19]: t4.flatten()
Out[19]: array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11])
```

## 数组的计算

numpy的广播机制，导致在运算过程中，加减乘除的值被广播到所有的元素上面，简单理解就是加减乘除会对数组中的每一个数进行处理

```python
In [28]: t4
Out[28]:
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11]])

In [29]: t4+2
Out[29]:
array([[ 2,  3,  4,  5],
       [ 6,  7,  8,  9],
       [10, 11, 12, 13]])
```

- 除以0会得出nan  和inf   0除以0  会出现nan  其他数字除以0 会出现inf

- 数据与数据之间的运算会将对应位置进行运算(数组形状要必须一样)

```python
In [31]: t5 = np.arange(24).reshape((4,6))

In [32]: t5
Out[32]:
array([[ 0,  1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23]])

In [33]: t6 = np.arange(100,124).reshape((4,6))

In [34]: t6
Out[34]:
array([[100, 101, 102, 103, 104, 105],
       [106, 107, 108, 109, 110, 111],
       [112, 113, 114, 115, 116, 117],
       [118, 119, 120, 121, 122, 123]])

In [35]: t6+t5
Out[35]:
array([[100, 102, 104, 106, 108, 110],
       [112, 114, 116, 118, 120, 122],
       [124, 126, 128, 130, 132, 134],
       [136, 138, 140, 142, 144, 146]])
```

- 不同形状的会在相同的维度上进行运算，

```python
In [36]: t7 = np.arange(0, 6)

In [37]: t7
Out[37]: array([0, 1, 2, 3, 4, 5])

In [38]: t5
Out[38]:
array([[ 0,  1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23]])

In [39]: t5-t7
Out[39]:
array([[ 0,  0,  0,  0,  0,  0],
       [ 6,  6,  6,  6,  6,  6],
       [12, 12, 12, 12, 12, 12],
       [18, 18, 18, 18, 18, 18]])

In [40]: t8 = np.arange(4).reshape((4,1))

In [41]: t8
Out[41]:
array([[0],
       [1],
       [2],
       [3]])

In [42]: t5-t8
Out[42]:
array([[ 0,  1,  2,  3,  4,  5],
       [ 5,  6,  7,  8,  9, 10],
       [10, 11, 12, 13, 14, 15],
       [15, 16, 17, 18, 19, 20]])
```

- 两个所有的维度都不相同的数组不能进行运算

```python
In [43]: t9 = np.arange(10)

In [44]: t9
Out[44]: array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

In [45]: t5
Out[45]:
array([[ 0,  1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23]])

In [46]: t5-t9
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-46-dcf9c8dd3788> in <module>
----> 1 t5-t9

ValueError: operands could not be broadcast together with shapes (4,6) (10,)
```

## numpy的轴

- 在numpy中可以理解为方向,使用0,1,2...数字表示,对于一个一维数组,只有一个0轴,对于2维数组(shape(2,2)),有0轴和1轴,对于三维数组(shape(2,2, 3)),有0,1,2轴

- 有了轴的概念之后,我们计算会更加方便,比如计算一个2维数组的平均值,必须指定是计算哪个方向上面的数字的平均值

- 那么问题来了: 在前面的知识,轴在哪里?回顾np.arange(0,10).reshape((2,5)),reshpe中2表示0轴长度(包含数据的条数)为2,1轴长度为5,2X5一共10个数据

## numpy读取本地数据

- np.loadtxt(fname,dtype=np.float,delimiter=None,skiprows=0,usecols=None,unpack=False)

![numpy读取数据](images\numpy读取数据.png)

```python
import numpy as np


us_file_path = "./youtube_video_data/US_video_data_numbers.csv"
uk_file_path = "./youtube_video_data/GB_video_data_numbers.csv"
# unpack 属性可进行转置
t1 = np.loadtxt(us_file_path, delimiter=",", dtype="int", unpack=True)
t2 = np.loadtxt(uk_file_path, delimiter=",", dtype="int")

print(t1)
```

## numpy中二维数组的转置方法

- transpose
- T
- swapaxes

```python

In [48]: t2 = np.arange(24).reshape((4,6))

In [49]: t2
Out[49]:
array([[ 0,  1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23]])

In [50]: t2.transpose()
Out[50]:
array([[ 0,  6, 12, 18],
       [ 1,  7, 13, 19],
       [ 2,  8, 14, 20],
       [ 3,  9, 15, 21],
       [ 4, 10, 16, 22],
       [ 5, 11, 17, 23]])

In [51]: t2.T
Out[51]:
array([[ 0,  6, 12, 18],
       [ 1,  7, 13, 19],
       [ 2,  8, 14, 20],
       [ 3,  9, 15, 21],
       [ 4, 10, 16, 22],
       [ 5, 11, 17, 23]])

In [52]: t2.swapaxes(1, 0)
Out[52]:
array([[ 0,  6, 12, 18],
       [ 1,  7, 13, 19],
       [ 2,  8, 14, 20],
       [ 3,  9, 15, 21],
       [ 4, 10, 16, 22],
       [ 5, 11, 17, 23]])
```

## numpy索引和切片

```python
import numpy as np


us_file_path = "./youtube_video_data/US_video_data_numbers.csv"
uk_file_path = "./youtube_video_data/GB_video_data_numbers.csv"

t1 = np.loadtxt(us_file_path, delimiter=",", dtype="int")
# t2 = np.loadtxt(uk_file_path, delimiter=",", dtype="int")
print(t1)
print("*"*100)

# 取行
print(t1[2])
print("*"*100)

# 取连续的多行
print(t1[2:])
print("*"*100)

# 取不连续的多行,需要多加一对方括号
print(t1[[2, 8, 10]])
print("*"*100)

# 通用方法 方括号内，逗号前面表示需要取的行，逗号后面表示需要取的列
print(t1[1, :])
print("*"*100)

# 取列
print(t1[:, 0])
print("*"*100)

# 取连续的多列
print(t1[:, 2:])
# 两个冒号，相当于取步长
print(t1[:, 2::2])
print("*"*100)

# 取不连续的多列
print(t1[:, [1, 3]])
print("*"*100)

# 取行和列
print(t1[3, 3])
print(type(t1[3, 3]))
print("*"*100)

# 取多行多列
print(t1[2:4, 0:2])
print("*"*100)

# 取多个不相邻的点
print(t1[[0, 2], [0, 1]])
print(t1[[0, 2, 2], [0, 1, 2]])
# 选出来的结果是（0,0），（2,1），（2,2）
print("*"*100)
```

## numpy中数值的修改

- 修改numpy中的数值，直接将对应位置数据取出来然后重新赋值就可以

```python
In [3]: t
Out[3]:
array([[ 0,  1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23]])

In [4]: t[:,2:4] = 0

In [5]: t
Out[5]:
array([[ 0,  1,  0,  0,  4,  5],
       [ 6,  7,  0,  0, 10, 11],
       [12, 13,  0,  0, 16, 17],
       [18, 19,  0,  0, 22, 23]])
```

- 按条件进行赋值
  - 将小区10 的数值修改为3

```python
In [7]: t2
Out[7]:
array([[ 0,  1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23]])

In [8]: t2<10
Out[8]:
array([[ True,  True,  True,  True,  True,  True],
       [ True,  True,  True,  True, False, False],
       [False, False, False, False, False, False],
       [False, False, False, False, False, False]])
    
In [10]: t2[t2<10] = 3

In [11]: t2
Out[11]:
array([[ 3,  3,  3,  3,  3,  3],
       [ 3,  3,  3,  3, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23]])
```

## numpy中的三元运算符

```python
In [12]: t3 = np.arange(24).reshape(4,6)

In [13]: t3
Out[13]:
array([[ 0,  1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23]])
# where的用法与三元运算符类似
In [15]: np.where(t3<10, 0, 10)
Out[15]:
array([[ 0,  0,  0,  0,  0,  0],
       [ 0,  0,  0,  0, 10, 10],
       [10, 10, 10, 10, 10, 10],
       [10, 10, 10, 10, 10, 10]])
```

- numpy中的clip（裁剪）

```python
In [16]: t4 = np.arange(24).reshape(4,6)

In [17]: t4
Out[17]:
array([[ 0,  1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23]])

# clip意思是将小于10的替换成10，大于18的替换成18
In [18]: t4.clip(10,18)
Out[18]:
array([[10, 10, 10, 10, 10, 10],
       [10, 10, 10, 10, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 18, 18, 18, 18, 18]])
```

## numpy中的nan和inf

- nan(NAN,Nan):not a number表示不是一个数字
- 什么时候numpy中会出现nan：
  -  当我们读取本地的文件为float的时候，如果有缺失，就会出现nan  
  - 当做了一个不合适的计算的时候(比如无穷大(inf)减去无穷大)
- inf(-inf,inf):infinity,inf表示正无穷，-inf表示负无穷
- 什么时候回出现inf包括（-inf，+inf）
  
-  比如一个数字除以0，（python中直接会报错，numpy中是一个inf或者-inf）  
  
- nan的特殊属性

  - 两个nan是不相等的

  ```python
  In [19]: np.nan == np.nan
  Out[19]: False
  ```

  - np.nan != np.nan

  ```python
  In [21]: np.nan != np.nan
  Out[21]: True
  ```

  - 利用以上的特性，可以判断数组中的nan的个数

  ```python
  In [36]: t1
  Out[36]: array([ 1.,  2., nan])
  
  In [37]: np.count_nonzero(t1 != t1)
  Out[37]: 1
  ```

  

  - 由于2，那么如何判断一个数字是否为nan呢？通过np.isnan(a)来判断，返回bool类型

  ```python
  In [36]: t1
  Out[36]: array([ 1.,  2., nan])
      
  In [38]: np.isnan(t1)
  Out[38]: array([False, False,  True])
  ```

  

  - nan和任何值计算都为nan

  ```python
  In [41]: t1
  Out[41]: array([ 1.,  2., nan])
  
  In [42]: t2
  Out[42]:
  array([[ 0,  1,  2],
         [ 3,  4,  5],
         [ 6,  7,  8],
         [ 9, 10, 11]])
  
  In [43]: t2+t1
  Out[43]:
  array([[ 1.,  3., nan],
         [ 4.,  6., nan],
         [ 7.,  9., nan],
         [10., 12., nan]])
  
  In [44]: t1
  Out[44]: array([ 1.,  2., nan])
  
  In [45]: np.sum(t1)
  Out[45]: nan
  ```

## numpy中的数学运算

```python
求和：t.sum(axis=None)
均值：t.mean(a,axis=None)  受离群点的影响较大
中值：np.median(t,axis=None) 
最大值：t.max(axis=None) 
最小值：t.min(axis=None)
极值：np.ptp(t,axis=None) 即最大值和最小值只差
标准差：t.std(axis=None) 
```

- 标准差是一组数据平均值分散程度的一种度量。一个较大的标准差，代表大部分数值和其平均值之间差异较大；一个较小的标准差，代表这些数值较接近平均值反映出数据的波动稳定情况，越大表示波动越大，越不稳定

## numpy中nan的替换注意事项

- 单纯的把nan替换为0肯定是不合适的，全部替换为0后，替换之前的平均值如果大于0，替换之后的均值肯定会变小，所以更一般的方式是把缺失的数值替换为均值（中值）或者是直接删除有缺失值的一行 

```python
import numpy as np


def fill_ndarray(t1):
    for i in range(t1.shape[1]):
        temp_col = t1[:, i] # 当前这一列
        nan_num = np.count_nonzero(temp_col != temp_col)
        if nan_num != 0: # 如果不为0，说明这一列数据中有nan
            temp_not_nan = temp_col[temp_col == temp_col] # 当前列中不为nan的array
            temp_col[np.isnan(temp_col)] = temp_not_nan.mean() # 选中当前为nan的位置，把值赋值为平均数
    return t1

if __name__ == "__main__":
    t1 = np.arange(12).reshape((3, 4)).astype("float")
    t1[1, 2:] = np.nan
    print(t1)
    t1 = fill_ndarray(t1)
    print(t1)
```

## 数组的拼接

```python
In [7]: t1
Out[7]:
array([[ 0,  1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23]])

In [8]: t2
Out[8]:
array([[25, 26, 27, 28, 29, 30],
       [31, 32, 33, 34, 35, 36],
       [37, 38, 39, 40, 41, 42],
       [43, 44, 45, 46, 47, 48]])

# vstack 竖直拼接
In [9]: np.vstack((t1,t2))
Out[9]:
array([[ 0,  1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23],
       [25, 26, 27, 28, 29, 30],
       [31, 32, 33, 34, 35, 36],
       [37, 38, 39, 40, 41, 42],
       [43, 44, 45, 46, 47, 48]])

# hstack 水平拼接
In [10]: np.hstack((t1,t2))
Out[10]:
array([[ 0,  1,  2,  3,  4,  5, 25, 26, 27, 28, 29, 30],
       [ 6,  7,  8,  9, 10, 11, 31, 32, 33, 34, 35, 36],
       [12, 13, 14, 15, 16, 17, 37, 38, 39, 40, 41, 42],
       [18, 19, 20, 21, 22, 23, 43, 44, 45, 46, 47, 48]])
```

## numpy数组的行列交换

```python
In [11]: t1
Out[11]:
array([[ 0,  1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23]])

# 进行行交换
In [12]: t1[[1,2],:] = t1[[2,1],:]

In [13]: t1
Out[13]:
array([[ 0,  1,  2,  3,  4,  5],
       [12, 13, 14, 15, 16, 17],
       [ 6,  7,  8,  9, 10, 11],
       [18, 19, 20, 21, 22, 23]])

# 进行列交换
In [14]: t2
Out[14]:
array([[25, 26, 27, 28, 29, 30],
       [31, 32, 33, 34, 35, 36],
       [37, 38, 39, 40, 41, 42],
       [43, 44, 45, 46, 47, 48]])

In [15]: t2[:,[0,2]] = t2[:,[2,0]]

In [16]: t2
Out[16]:
array([[27, 26, 25, 28, 29, 30],
       [33, 32, 31, 34, 35, 36],
       [39, 38, 37, 40, 41, 42],
       [45, 44, 43, 46, 47, 48]])
```

## numpy更多的方法

- 获取最大最小值的位置

```python
np.argmax(t,axis=0)
np.argmin(t,axis=1)
```

- 创建一个全0的数组

```python
np.zeros((3,4))
```

- 创建一个全1的数组

```python
np.ones((3,4))
```

- 创建一个对角线为1的正方形数组

```python
np.eye(3)
```

## numpy生成随机数

![numpy生成随机数](images\numpy生成随机数.png)

```python
import numpy as np


np.random.seed(10)

t = np.random.randint(0, 20, (3, 4))

print(t)


"""
[[ 9  4 15  0]
 [17 16 17  8]
 [ 9  0 10  8]]
"""
```

## numpy的注意点 copy和view

1. a=b 完全不复制，a和b相互影响

2. a = b[:],视图的操作，一种切片，会创建新的对象a，但是a的数据完全由b保管，他们两个的数据变化是一致的，

3. a = b.copy(),复制，a和b互不影响











