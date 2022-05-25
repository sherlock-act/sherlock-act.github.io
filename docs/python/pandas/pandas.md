# Pandas

numpy能够帮我们处理处理数值型数据，但是这还不够，很多时候，我们的数据除了数值之外，还有字符串，还有时间序列等。所有需要使用pandas，==所以，numpy能够帮助我们处理数值，但是pandas除了处理数值之外(基于numpy)，还能够帮助我们处理其他类型的数据==

## pandas的数据类型

1. Series 一维，带标签数组
2. DataFrame 二维，Series容器

### Series

#### 创建Series

```python
In [28]: pd.Series([1,2,3,4,5,6,7,8])
Out[28]:
0    1
1    2
2    3
3    4
4    5
5    6
6    7
7    8
dtype: int64

In [29]: pd.Series(np.arange(12))
Out[29]:
0      0
1      1
2      2
3      3
4      4
5      5
6      6
7      7
8      8
9      9
10    10
11    11
dtype: int32

    
In [30]: t1 = pd.Series(np.arange(12))

In [31]: type(t1)
Out[31]: pandas.core.series.Series
```

- 指定index

```python
In [32]: t2 = pd.Series(np.arange(6), index=list("abcdef"))

In [33]: t2
Out[33]:
a    0
b    1
c    2
d    3
e    4
f    5
dtype: int32
```

- 通过字典创建Series

```python 
In [34]: temp_dict = {"name":"xiaohong", "age":30, "tel":10086}

In [35]: t3 = pd.Series(temp_dict)

In [36]: t3
Out[36]:
name    xiaohong
age           30
tel        10086
dtype: object
```

#### 修改Series的数据类型

- 和numpy中一样，使用astype进行修改
- `t2.astype("float")`

#### Series的切片和索引

```python
In [7]: t2
Out[7]:
name    xiaohong
age           18
tel        10086
dtype: object

# 通过index进行索引
In [8]: t2["age"]
Out[8]: 18
    
# 通过位置进行索引  
In [9]: t2[2]
Out[9]: 10086
    
# 通过位置进行切片去连续的数据
In [11]: t2[:2]
Out[11]:
name    xiaohong
age           18
dtype: object
    
# 通过位置进行不连续数据切片
In [12]: t2[[1,2]]
Out[12]:
age       18
tel    10086
dtype: object

# 通过index进行不连续数据切片
In [15]: t2[['name','tel']]
Out[15]:
name    xiaohong
tel        10086
dtype: object
    
# bool索引
In [16]: t1
Out[16]:
0      0
1      1
2      2
3      3
4      4
5      5
6      6
7      7
8      8
9      9
10    10
11    11
dtype: int32

In [17]: t1[t1>4]
Out[17]:
5      5
6      6
7      7
8      8
9      9
10    10
11    11
dtype: int32
```

- 切片：直接传入start end 或者步长即可
- 索引：一个的时候，直接传入序号或者index，多个的时候传入序号或者index的列表

#### Series的索引和值

- Series的index

```python
In [19]: t2.index
Out[19]: Index(['name', 'age', 'tel'], dtype='object')

In [20]: for i in t2.index:
    ...:     print(i)
    ...:
name
age
tel

In [21]: type(t2.index)
Out[21]: pandas.core.indexes.base.Index
    
In [23]: len(t2.index)
Out[23]: 3

In [24]: list(t2.index)
Out[24]: ['name', 'age', 'tel']
```

- Series的值

```python
In [26]: t2.values
Out[26]: array(['xiaohong', 18, 10086], dtype=object)

In [27]: type(t2.values)
Out[27]: numpy.ndarray
# Series的值同样可以进行遍历，len 与list强制类型转换
```

### DataFrame

#### 创建DataFrame

```python
In [28]: df = pd.DataFrame(np.arange(24).reshape((4,6
    ...: )))

In [29]: df
Out[29]:
    0   1   2   3   4   5
0   0   1   2   3   4   5
1   6   7   8   9  10  11
2  12  13  14  15  16  17
3  18  19  20  21  22  23
```

- DataFrame对象既有行索引，又有列索引

  - 行索引，表明不同行，横向索引，叫index，0轴，axis=0

  - 列索引，表名不同列，纵向索引，叫columns，1轴，axis=1

```python
# 指定index和columns
In [32]: df2 = pd.DataFrame(np.arange(24).reshape((4,
    ...: 6)), index=list("abcd"), columns=list("abcde
    ...: f"))

In [33]: df2
Out[33]:
    a   b   c   d   e   f
a   0   1   2   3   4   5
b   6   7   8   9  10  11
c  12  13  14  15  16  17
d  18  19  20  21  22  23
                                               
# 通过字典创建DataFrame
In [38]: df3 = pd.DataFrame(d1)

In [39]: df3
Out[39]:
       name  age    tel
0  xiaohong   18  10086
1  xiaoming   18  10010
```

- DataFrame就是Series的容器

#### DataFrame的方法和属性

![DataFrame的方法](images\DataFrame的方法.png)

```python
In [39]: df3
Out[39]:
       name  age    tel
0  xiaohong   18  10086
1  xiaoming   18  10010

In [40]: df3.index
Out[40]: RangeIndex(start=0, stop=2, step=1)

In [41]: df3.columns
Out[41]: Index(['name', 'age', 'tel'], dtype='object')
In [42]: df3.values
Out[42]:
array([['xiaohong', 18, 10086],
       ['xiaoming', 18, 10010]], dtype=object)

In [43]: df3.shape
Out[43]: (2, 3)

In [44]: df3.dtypes
Out[44]:
name    object
age      int64
tel      int64
dtype: object

In [45]: df3.ndim
Out[45]: 2

In [46]: df3.head(2)
Out[46]:
       name  age    tel
0  xiaohong   18  10086
1  xiaoming   18  10010

In [47]: df3.tail(1)
Out[47]:
       name  age    tel
1  xiaoming   18  10010

In [48]: df3.info
Out[48]:
<bound method DataFrame.info of        name  age    tel
0  xiaohong   18  10086
1  xiaoming   18  10010>
```

#### DataFrame的排序

```python
# DataFrame的排序，默认升序 ascending=False,标识降序排序
df.sort_values(by="Count_AnimalName", ascending=False)
```

#### DataFrame的切换和索引

- pandas取行或者列的注意事项
  - 方括号写数字表示取行，对行进行操作
  - 方括号写字符串表示取列索引，对列进行操作

```python
# 按行进行切片
In [5]: df[:20]
Out[5]:
   Row_Labels  Count_AnimalName
0           1                 1
1           2                 2
2       40804                 1
3       90201                 1
4       90203                 1
5      102201                 1
6     3010271                 1
7       MARCH                 2
8       APRIL                51
9      AUGUST                14
10   DECEMBER                 4
11     SUNDAY                13
12     MONDAY                 4
13     FRIDAY                19
14        JAN                 1
15        JUN                 1
16    JANUARY                 1
17       JUNE                24
18       JULY                 9
19        MON                 2

# 取前20行的Rowl_label
In [6]: df[:20]["Row_Labels"]
Out[6]:
0            1
1            2
2        40804
3        90201
4        90203
5       102201
6      3010271
7        MARCH
8        APRIL
9       AUGUST
10    DECEMBER
11      SUNDAY
12      MONDAY
13      FRIDAY
14         JAN
15         JUN
16     JANUARY
17        JUNE
18        JULY
19         MON
Name: Row_Labels, dtype: object
```

##### pandas的loc与iloc方法

- df.loc 通过**标签**索引行数据
- df.iloc 通过**位置**获取行数据

###### loc方法

```python
In [10]: df2
Out[10]:
   w  x   y   z
a  0  1   2   3
b  4  5   6   7
c  8  9  10  11

# 取某一行某一列
In [11]: df2.loc["a","z"]
Out[11]: 3

In [12]: type(df2.loc["a","z"])
Out[12]: numpy.int32
    
# 取某一行，方括号内直接写index
In [13]: df2.loc["a"]
Out[13]:
w    0
x    1
y    2
z    3
Name: a, dtype: int32
        
# 取某一列，方括号内打：表示取所有的行，然后打需要取的columns
In [15]: df2.loc[:,"y"]
Out[15]:
a     2
b     6
c    10
Name: y, dtype: int32
        
# 取不连续的多行  df2.loc[["a","c"]]
In [17]: df2.loc[["a","c"],:]
Out[17]:
   w  x   y   z
a  0  1   2   3
c  8  9  10  11
# 也可以不用写：
In [18]: df2.loc[["a","c"]]
Out[18]:
   w  x   y   z
a  0  1   2   3
c  8  9  10  11
# 取不连续多列与上述类似
In [19]: df2.loc[:,["x","z"]]
Out[19]:
   x   z
a  1   3
b  5   7
c  9  11

# 综合切片   需要注意，loc方法中C行能取出来
In [23]: df2.loc["a":"c", ["w","z"]]
Out[23]:
   w   z
a  0   3
b  4   7
c  8  11


```

###### iloc方法

```python
# 取一行
In [25]: df2
Out[25]:
   w  x   y   z
a  0  1   2   3
b  4  5   6   7
c  8  9  10  11

In [26]: df2.iloc[1]
Out[26]:
w    4
x    5
y    6
z    7
Name: b, dtype: int32

# 取某一列
In [28]: df2.iloc[:,2]
Out[28]:
a     2
b     6
c    10
Name: y, dtype: int32

# 取不连续多列
In [29]: df2.iloc[:,[2,1]]
Out[29]:
    y  x
a   2  1
b   6  5
c  10  9

# 取不连续的多行多列
In [30]: df2.iloc[[0,2], [2,1]]
Out[30]:
    y  x
a   2  1
c  10  9

# 连续的多行多列
In [31]: df2.iloc[1:,:2]
Out[31]:
   w  x
b  4  5
c  8  9
```

##### bool索引

```python
In [32]: df
Out[32]:
      Row_Labels  Count_AnimalName
0              1                 1
1              2                 2
2          40804                 1
3          90201                 1
4          90203                 1
...          ...               ...
16215      37916                 1
16216      38282                 1
16217      38583                 1
16218      38948                 1
16219      39743                 1

[16220 rows x 2 columns]

# 满足条件的值
In [33]: df[df["Count_AnimalName"]>800]
Out[33]:
      Row_Labels  Count_AnimalName
1156       BELLA              1195
2660     CHARLIE               856
3251        COCO               852
9140         MAX              1153
12368      ROCKY               823

# 多个条件 中间用&、|等符号连接起来 &表示且   |表示或
In [36]: df[(800<df["Count_AnimalName"])&(df["Count_AnimalName"]<1000)]
Out[36]:
      Row_Labels  Count_AnimalName
2660     CHARLIE               856
3251        COCO               852
12368      ROCKY               823

# 选择使用次数超过700次以上，且名字长度大于4的狗的名字
In [37]: df[(df["Row_Labels"].str.len()>4)&(df["Count_AnimalName"]>700)]
Out[37]:
      Row_Labels  Count_AnimalName
1156       BELLA              1195
2660     CHARLIE               856
8552       LUCKY               723
12368      ROCKY               823

```

#### pandas字符串的方法

![DataFrame字符串的方法](images\DataFrame字符串的方法.png)

## 缺失数据的处理

- 判断nan的方法

```python
pd.isnull(df)
pd.notnull(df)

In [43]: df2
Out[43]:
     w    x   y   z
a  0.0  1.0   2   3
b  NaN  NaN   6   7
c  NaN  NaN  10  11

In [44]: pd.isnull(df2)
Out[44]:
       w      x      y      z
a  False  False  False  False
b   True   True  False  False
c   True   True  False  False

In [46]: pd.notnull(df2)
Out[46]:
       w      x     y     z
a   True   True  True  True
b  False  False  True  True
c  False  False  True  True
```

- 缺失数据的处理方法

  - 方法一：删除NaN所在的行列

  ```python
  dropna (axis=0, how='any', inplace=False)
  
  In [47]: df2
  Out[47]:
       w    x   y   z
  a  0.0  1.0   2   3
  b  NaN  NaN   6   7
  c  NaN  NaN  10  11
  
  In [48]: df2[pd.notnull(df2["w"])]
  Out[48]:
       w    x  y  z
  a  0.0  1.0  2  3
  
  In [49]: df2.dropna(axis=0)
  Out[49]:
       w    x  y  z
  a  0.0  1.0  2  3
  
  # how 参数选择怎么删除，默认是any：只要有NaN就删除， all：行或者列的所有数据都为NaN才删除
  In [50]: df2.dropna(axis=0,how="all")
  Out[50]:
       w    x   y   z
  a  0.0  1.0   2   3
  b  NaN  NaN   6   7
  c  NaN  NaN  10  11
  
  
  ```

  - 方法二：填充数据

  ```python 
  t.fillna(t.mean())
  t.fiallna(t.median())
  t.fillna(0)
  
  In [51]: df2
  Out[51]:
       w    x   y   z
  a  0.0  1.0   2   3
  b  NaN  NaN   6   7
  c  NaN  NaN  10  11
  
  In [52]: df2.fillna(0)
  Out[52]:
       w    x   y   z
  a  0.0  1.0   2   3
  b  0.0  0.0   6   7
  c  0.0  0.0  10  11
  
  In [54]: df2.fillna("")
  Out[54]:
     w  x   y   z
  a  0  1   2   3
  b         6   7
  c        10  11
  ```

## pandas的统计方法

 ```python
 # 获取电影的平均评分
print(df["Rating"].mean())
  
# 导演的人数
print(len(set(df["Director"].tolist())))
 ```



![pandas_tongji1](images\pandas_tongji1.png)

## pandas读取外部数据

`pd.read_XXX`

## 统计数据提升

```python
import pandas as pd
import numpy as np
from matplotlib import pyplot as plt


file_path = "./IMDB-Movie-Data.csv"

df = pd.read_csv(file_path)

# 统计分类的列表
temp_list = df["Genre"].str.split(",").tolist()

genre_list = list(set(i for j in temp_list for i in j))

# 构造全为0的数组
zeros_df = pd.DataFrame(np.zeros((df.shape[0], len(genre_list))), columns=genre_list)

# 给每个点一个你出现分类的位置赋值1
for i in range(df.shape[0]):
    zeros_df.loc[i, temp_list[i]] = 1


# print(zeros_df.head(1))
#
# print(zeros_df.describe())

# 统计所有分类电影的数量合
genre_count = zeros_df.sum(axis=0)

genre_count = genre_count.sort_values()
_x = genre_count.index
_y = genre_count.values

plt.barh(_x, _y)
plt.grid()

plt.show()
```

## 数组的合并

### join

- join:默认情况下他是把行索引相同的数据合并到一起

```python
In [3]: t2 = pd.DataFrame(np.zeros((2,5)),index=list("AB"),columns=list("VWXYZ"
   ...: ))                                                                     

In [4]: t2                                                                     
Out[4]: 
     V    W    X    Y    Z
A  0.0  0.0  0.0  0.0  0.0
B  0.0  0.0  0.0  0.0  0.0

In [5]: t1 = pd.DataFrame(np.ones((3,4)),index=list("ABC"))                    

In [6]: t1                                                                     
Out[6]: 
     0    1    2    3
A  1.0  1.0  1.0  1.0
B  1.0  1.0  1.0  1.0
C  1.0  1.0  1.0  1.0

In [7]: t1.join(t2)                                                            
Out[7]: 
     0    1    2    3    V    W    X    Y    Z
A  1.0  1.0  1.0  1.0  0.0  0.0  0.0  0.0  0.0
B  1.0  1.0  1.0  1.0  0.0  0.0  0.0  0.0  0.0
C  1.0  1.0  1.0  1.0  NaN  NaN  NaN  NaN  NaN

In [8]: t2.join(t1)                                                            
Out[8]: 
     V    W    X    Y    Z    0    1    2    3
A  0.0  0.0  0.0  0.0  0.0  1.0  1.0  1.0  1.0
B  0.0  0.0  0.0  0.0  0.0  1.0  1.0  1.0  1.0

```

### merge

- merge:按照指定的列把数据按照一定的方式合并到一起

```python
In [11]: t2                                                                    
Out[11]: 
     V    W    X    Y    Z
A  0.0  0.0  0.0  0.0  0.0
B  0.0  0.0  0.0  0.0  0.0

In [12]: t3                                                                    
Out[12]: 
     X    Y    Z
A  0.0  0.0  0.0
B  0.0  0.0  0.0
C  0.0  0.0  0.0

In [13]: t2.merge(t3,on="X")                                                   
Out[13]: 
     V    W    X  Y_x  Z_x  Y_y  Z_y
0  0.0  0.0  0.0  0.0  0.0  0.0  0.0
1  0.0  0.0  0.0  0.0  0.0  0.0  0.0
2  0.0  0.0  0.0  0.0  0.0  0.0  0.0
3  0.0  0.0  0.0  0.0  0.0  0.0  0.0
4  0.0  0.0  0.0  0.0  0.0  0.0  0.0
5  0.0  0.0  0.0  0.0  0.0  0.0  0.0

```

- 合并方式
  - 默认的合并方式inner，并集
  - merge outer，交集，NaN补全
  - merge left，左边为准，NaN补全
  - merge right，右边为准，NaN补全

![merge合并](images\merge合并.png)

## 分组和聚合

### 分组

- 在pandas中类似的分组的操作我们有很简单的方式来完成
- `df.groupby(by="columns_name")`
  - grouped中的每一个元素是一个元组
  - ​     元组里面是（索引(分组的值)，分组之后的DataFrame）  
  - grouped是一个DataFrameGroupBy对象，是可迭代的，也可以直接调用聚合方法
- 数据可以按照多个条件进行分组
  - `df["Brand"].groupby(by=[df["Country"],df["State/Province"]])`
  - `df.groupby(by=["Country","State/Province"])`

```python
获取分组之后的某一部分数据：
 df.groupby(by=["Country","State/Province"])["Country"].count()

对某几列数据进行分组：
 df["Country"].groupby(by=[df["Country"],df["State/Province"]]).count()

```



### 聚合

![聚合方法](images\聚合方法.png)

```python
import pandas as pd
import numpy as np


pd.options.display.max_columns=999
file_path = "./starbucks_store_worldwide.csv"

df = pd.read_csv(file_path)

# print(df.head(3))
#
# print(df.info())
grouped = df.groupby(by="Country")

print(grouped)

# DataFrameGroupBy
# 可以进行遍历
# for i in grouped:
#     print(i)
#     print("*"*100)
# 可以进行聚合方法
# country_count = grouped["Brand"].count()
#
# print(country_count["US"])
# print(country_count["CN"])

# 统计中国每个省份星巴克的数量
cn_group = df[df["Country"] == "CN"].groupby(by="State/Province")

province_data = cn_group["Brand"].count()

print(province_data)
```

## 索引与复合索引

简单的索引操作：

- 获取index：df.index

- 指定index ：df.index = ['x','y']

- 重新设置index : df.reindex(list("abcedf"))

- 指定某一列作为index ：df.set_index("Country",drop=False)

- 返回index的唯一值：df.set_index("Country").index.unique()

![复合索引](images\复合索引.png)

![复合索引2](images\复合索引2.png)



- 复合使用swaplevel切换index的前后顺序

- DataFrame的复合索引

![DataFrame的方法](images\DataFrame的方法.png)

## 时间序列

