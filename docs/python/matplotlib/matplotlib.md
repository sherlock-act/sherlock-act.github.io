# Matplotlib

- 什么是Matplotlib：最流行的Python底层绘图库，主要做数据可视化图表,名字取材于MATLAB，模仿MATLAB构建。

# 绘制二维图形

绘制二维图形需要使用matplotlib中的pyplot包

```python
from matplotlib import pyplot as plt
```



## figure axes axis

首先,在画图前,需要现了解figure与axes

- figure:可以理解为要绘制图形的整个画布
- axes:可以理解为绘制的图形的整体
- axis:坐标轴,在二维图形上就是x轴与y轴

## 创建画布与图形

在了解了上面三个概念之后,就能比较容易理解后面对图形的各种调整,要绘制图形首先就需要现有一个画布

- `figure`创建画布
  - 返回一个画布对象
  - 需要绘制图形需要在画布上添加图形
  - add_axes:必须传入新图形四个边框的长度


```python
fig = plt.figure()
ax = fig.add_axes([0.1, 0.1, 0.8, 0.8])
ax.plot([1, 2], [1, 2])
plt.show()
```

- 常用参数
  - figsize:需要穿一个两个元素的数组,表示画布的大小
  - dpi:每一寸的像素点个数,默认值100,表示画出来的图形的清晰度
- `subplots`创建画布与图形

```python
fig, ax = plt.subplots()
ax.plot([1, 2], [1, 2])
plt.show()
```

- 常用参数
  - nrows, ncols:子图的行数与列数,即表示有多少个子图
  

## 折线图

```python
from matplotlib import pyplot as plt
import numpy as np


_x = np.arange(20)
_y = np.random.randint(1, 20, size=20)

fig, ax = plt.subplots() # 创建画布与图形
ax.plot(_x, _y, c="black", marker="o", ms=5, ls="-.", lw=0.5, alpha=0.6, label="line_1") # 绘制折线图
plt.show()
```

- 参数解释:
  - c 或 color: 线条颜色
  - marker: 端点样式
  - ms 或 markersize: 端点大小
  - ls 或 linestyle: 线条样式
  - lw 或 linewidth: 线条宽度
  - alpha:透明度
  - label:线条名称,显示图例时显示线条名称









## 折线图

- 简单使用

```python
from matplotlib import pyplot as plt


x = range(2, 26, 2)
y = [15, 13, 14.5, 17, 20, 25, 26, 26, 24, 22, 18, 15]

plt.plot(x, y)
plt.show()
```

- 设置图片大小

```python
from matplotlib import pyplot as plt


fig = plt.figure(figsize=(20, 8), dpi=80)
# figure图形图标的意思，这里指绘画的图
# figsize，指图片的大小
# dpi，指图片的分辨率
x = range(2, 26, 2)
y = [15, 13, 14.5, 17, 20, 25, 26, 26, 24, 22, 18, 15]

plt.plot(x, y)
plt.show()
```

- 保存图片

```python
from matplotlib import pyplot as plt


fig = plt.figure(figsize=(20, 8), dpi=80)
# figure图形图标的意思，这里指绘画的图
# figsize，指图片的大小
# dpi，指图片的分辨率
x = range(2, 26, 2)
y = [15, 13, 14.5, 17, 20, 25, 26, 26, 24, 22, 18, 15]

plt.plot(x, y)
plt.savefig("./t1.png")
# 使用save保存图片
# 可以保存为 SVG这种矢量图的格式，放大不会有锯齿
```

- 调整x轴与y轴的刻度

```python
from matplotlib import pyplot as plt


fig = plt.figure(figsize=(20, 8), dpi=80)
# figure图形图标的意思，这里指绘画的图
# figsize，指图片的大小
# dpi，指图片的分辨率
x = range(2, 26, 2)
y = [15, 13, 14.5, 17, 20, 25, 26, 26, 24, 22, 18, 15]

# 绘图
plt.plot(x, y)

# 设置X轴
# x轴需要显示哪些值就传哪些就可以了
# 以每一个X的指作为坐标轴
# plt.xticks(x)

# 可以自己传递传输，调整X轴
# plt.xticks(range(2, 25))

# 要是觉得X轴的取值依然不够，还可以直接更加细化
# _xticks_lable = [i/2 for i in range(2, 49)]
# plt.xticks(_xticks_lable)

# 要是觉得X轴太密集，可以通过取列表的步长来调整
_xticks_lable = [i/2 for i in range(4, 49)]
plt.xticks(_xticks_lable[::2])

# 设置y轴
# y轴的方法与x相同
plt.yticks(range(min(y), max(y)+1))

# 展示图形
plt.show()
```

- 扩展:调整X轴（将字符串设置为刻度）

```python
from matplotlib import pyplot as plt
import random
import matplotlib
from matplotlib import font_manager


# 第一种方式，windows和linux下可用
# 设置图片显示的字体
# font = {'family': 'MicroSoft YaHei'}
# # 以下两种写法都可以
# matplotlib.rc("font", **font)
# # matplotlib.rc("font", family='NotoSansCJK-Black')

# 方法二。通用，导入matplotlib的font manager

my_font = font_manager.FontProperties(fname="/usr/share/fonts/opentype/noto/NotoSansCJK-Regular.ttc")
# fname是传的字体地址

a = [random.randint(20, 35) for i in range(120)]

x = range(120)

plt.figure(figsize=(20, 8), dpi=80)

plt.plot(x, a)

# 调整X的刻度
# _x = list(x)[::10]
# _xticks_lable = ["hello,{}".format(i) for i in _x]
# 可以给xticks里面传多个值，显示自定义内容,两个值必须一一对应
# plt.xticks(_x, _xticks_lable)

# 让x轴显示时间
_xticks_lable = ["10点{}分".format(i) for i in range(60)]
_xticks_lable += ["11点{}分".format(i) for i in range(60)]

# matplotlib默认不支持中文字体，要想显示中文需要传fontproperties
plt.xticks(list(x)[::4], _xticks_lable[::4], rotation=45, fontproperties=my_font)
# rotation参数是设置坐标轴旋转的角度


plt.show()
```

- 添加描述信息

```python
from matplotlib import pyplot as plt
import random
from matplotlib import font_manager


my_font = font_manager.FontProperties(family="MicroSoft YaHei")
y = [random.randint(25, 34) for i in range(120)]
x = [i for i in range(120)]
_x = ["10点{}分".format(i) for i in range(60)]
_x += ["11点{}分".format(i) for i in range(60)]

plt.figure(figsize=(20, 8), dpi=80)

plt.plot(x, y)
plt.xticks(list(x)[::4], _x[::4], rotation=45, fontproperties=my_font)

# 添加描述信息
plt.xlabel("时间  单位（分）", fontproperties=my_font)
plt.ylabel("温度  单位（℃）", fontproperties=my_font)
plt.title("10点至12点每分钟温度变化情况", fontproperties=my_font)

plt.show()
```

- 画多条折线

```python
from matplotlib import pyplot as plt
import random


x = range(10)
y1 = [random.randint(5, 10) for i in range(10)]
y2 = [random.randint(12, 18) for a in range(10)]
y3 = [random.randint(20, 25) for b in range(10)]

# 在绘制的时候绘制多次就可以绘制多条折线图
plt.plot(x, y1, label="first", color="r", linestyle="--", linewidth=5, alpha=0.5)
# color 线条的颜色 也可以传16进制颜色号
# linestyle 线条的风格 - 实线  -- 虚线  -.点划线  : 点虚线
# linewidth 线条粗细
# alpha 透明度
plt.plot(x, y2, label="seconde")
plt.plot(x, y3, label="third")

# legend函数显示图例
plt.legend()
# 要显示中文需要添加prop显示中文
plt.show()
```

- 绘制网格

```python
from matplotlib import pyplot as plt
import random
from matplotlib import font_manager


my_font = font_manager.FontProperties(family="MicroSoft YaHei", size=20)
a = [random.randint(0, 5) for i in range(20)]
x = ["{}岁".format(b) for b in range(11, 31)]

plt.figure(figsize=(20, 10), dpi=80)

plt.plot(x, a)
plt.xticks(rotation=45, fontproperties=my_font)
plt.xlabel("岁数", fontproperties=my_font)
plt.ylabel("交往女朋友个数", fontproperties=my_font)
plt.title("每年交往女朋友的个数", fontproperties=my_font)

# 绘制网格
plt.grid(alpha=0.4)
# 不传参数是直接在每个X轴与Y轴分别绘制一条灰色实线
# alpha 代表透明度 取值范围 0-1

plt.show()
```

- 添加水印和文本注释

```python

```

## 散点图

- 简单使用

```python
from matplotlib import pyplot as plt
from matplotlib import font_manager

y_3 = [11, 17, 16, 11, 12, 11, 12, 6, 6, 7, 8, 9, 12, 15, 14, 17, 18, 21, 16, 17, 20, 14, 15, 15, 15, 19, 21, 22, 22, 22, 23]
y_10 = [26, 26, 28, 19, 21, 17, 16, 19, 18, 20, 20, 19, 22, 23, 17, 20, 21, 20, 22, 15, 11, 15, 5, 13, 17, 10, 11, 13, 12, 13, 6]

x = range(1, 32)

# 绘制
plt.scatter(x, y_3)

# 展示
plt.show()
```

- 绘制两个图形

```python
from matplotlib import pyplot as plt
from matplotlib import font_manager


my_font = font_manager.FontProperties(family="MicroSoft YaHei")

y_3 = [11, 17, 16, 11, 12, 11, 12, 6, 6, 7, 8, 9, 12, 15, 14, 17, 18, 21, 16, 17, 20, 14, 15, 15, 15, 19, 21, 22, 22, 22, 23]
y_10 = [26, 26, 28, 19, 21, 17, 16, 19, 18, 20, 20, 19, 22, 23, 17, 20, 21, 20, 22, 15, 11, 15, 5, 13, 17, 10, 11, 13, 12, 13, 6]

# 设置图形大小
plt.figure(figsize=(20, 8), dpi=80)

x_3 = range(1, 32)
x_10 = range(51, 82)
_x_all = list(x_3) + list(x_10)
_x = ["3月{}日".format(i) for i in range(1, 32)]
_x += ["10月{}日".format(n) for n in range(51, 82)]

# 绘制 使用scatter 绘制散点图
plt.scatter(x_3, y_3, label="3月")
plt.scatter(x_10, y_10, label="10月")

# 调整X
plt.xticks(_x_all[::3], list(_x)[::3], rotation=45, fontproperties=my_font)

# 设置说明信息
plt.xlabel("日期", fontproperties=my_font)
plt.ylabel("气温", fontproperties=my_font)
plt.title("3月与10月气温分布情况", fontproperties=my_font)

# 添加图例
plt.legend(prop=my_font)

# 展示
plt.show()
```

## 绘制条形图

- 简单使用

```python 
from matplotlib import pyplot as plt
from matplotlib import font_manager

a = ["战狼2", "速度与激情8", "功夫瑜伽", "西游伏妖篇", "变形金刚5：最后的骑士", "摔跤吧！爸爸", "加勒比海盗5：死无对证", "金刚：骷髅岛", "极限特工：终极回归", "生化危机6：终章", "乘风破浪", "神偷奶爸3", "智取威虎山", "大闹天竺", "金刚狼3：殊死一战", "蜘蛛侠：英雄归来", "悟空传", "银河护卫队2", "情圣", "新木乃伊", ]

b = [56.01, 26.94, 17.53, 16.49, 15.45, 12.96, 11.8, 11.61, 11.28, 11.12, 10.49, 10.3, 8.75, 7.55, 7.32, 6.99, 6.88, 6.86, 6.58, 6.23]

# 设置字体
my_font = font_manager.FontProperties(family="MicroSoft YaHei")

# 设置图形大小
plt.figure(figsize=(20, 10), dpi=80)

# 绘制条形图，width设置宽带
plt.bar(range(len(a)), b, width=0.3)

# 调整x轴
plt.xticks(range(len(a)), a, rotation=45, fontproperties=my_font)

# 设置说明
plt.xlabel("电影名称", fontproperties=my_font)
plt.ylabel("票房（亿）", fontproperties=my_font)
plt.title("电影票房排行", fontproperties=my_font)

# 展示
plt.show()
```

- 绘制横着的条形图

```python
from matplotlib import pyplot as plt
from matplotlib import font_manager


a = ["战狼2", "速度与激情8", "功夫瑜伽", "西游伏妖篇", "变形金刚5：最后的骑士", "摔跤吧！爸爸", "加勒比海盗5：死无对证", "金刚：骷髅岛", "极限特工：终极回归", "生化危机6：终章", "乘风破浪", "神偷奶爸3", "智取威虎山", "大闹天竺", "金刚狼3：殊死一战", "蜘蛛侠：英雄归来", "悟空传", "银河护卫队2", "情圣", "新木乃伊", ]

b = [56.01, 26.94, 17.53, 16.49, 15.45, 12.96, 11.8, 11.61, 11.28, 11.12, 10.49, 10.3, 8.75, 7.55, 7.32, 6.99, 6.88, 6.86, 6.58, 6.23]

# 设置字体
my_font = font_manager.FontProperties(family="MicroSoft YaHei")

# 设置图形大小
plt.figure(figsize=(20, 8), dpi=80)

# 绘制横着的条形图，width设置宽带
# plt.bar(range(len(a)), b, width=0.3)
plt.barh(range(len(a)), b, height=0.3, color="cyan")

# 调整y轴
plt.yticks(range(len(a)), a, fontproperties=my_font)

# 设置说明
plt.xlabel("票房（亿）", fontproperties=my_font)
plt.ylabel("电影名称", fontproperties=my_font)
plt.title("电影票房排行", fontproperties=my_font)

# 绘制网格
plt.grid(linestyle="-.", alpha=0.5)

# 展示
plt.show()
```

- 绘制多条条形图
  - 绘制多条条形图的时候，需要将X偏移一点

```python 
from matplotlib import pyplot as plt
from matplotlib import font_manager

a = ["猩球崛起3：终极之战", "敦刻尔克", "蜘蛛侠：英雄归来", "战狼2"]
b_16 = [15746, 312, 4497, 319]
b_15 = [12357, 156, 2045, 168]
b_14 = [2358, 399, 2358, 362]

x_14 = list(range(len(a)))
x_15 = [i+0.2 for i in x_14]
x_16 = [n+0.2 for n in x_15]

# 设置字体
my_font = font_manager.FontProperties(family="MicroSoft YaHei")

# 设置图形大小
plt.figure(figsize=(20, 8), dpi=80)

# 绘制条形图
plt.bar(x_14, b_14, width=0.2, label="14日")
plt.bar(x_15, b_15, width=0.2, label="15日")
plt.bar(x_16, b_16, width=0.2, label="16日")

# 调整x轴
plt.xticks(x_15, a, fontproperties=my_font)

# 显示图例
plt.legend(prop=my_font)

# 展示
plt.show()
```

## 绘制直方图

```python
from matplotlib import pyplot as plt
from matplotlib import  font_manager

a = [131, 98, 125, 131, 124, 139, 131, 117, 128, 108, 135, 138, 131, 102, 107, 114, 119, 128, 121, 142, 127, 130, 124,
     101, 110, 116, 117, 110, 128, 128, 115, 99, 136, 126, 134, 95, 138, 117, 111, 78, 132, 124, 113, 150, 110, 117, 86,
     95, 144, 105, 126, 130, 126, 130, 126, 116, 123, 106, 112, 138, 123, 86, 101, 99, 136, 123, 117, 119, 105, 137,
     123, 128, 125, 104, 109, 134, 125, 127, 105, 120, 107, 129, 116, 108, 132, 103, 136, 118, 102, 120, 114, 105, 115,
     132, 145, 119, 121, 112, 139, 125, 138, 109, 132, 134, 156, 106, 117, 127, 144, 139, 139, 119, 140, 83, 110, 102,
     123, 107, 143, 115, 136, 118, 139, 123, 112, 118, 125, 109, 119, 133, 112, 114, 122, 109, 106, 123, 116, 131, 127,
     115, 118, 112, 135, 115, 146, 137, 116, 103, 144, 83, 123, 111, 110, 111, 100, 154, 136, 100, 118, 119, 133, 134,
     106, 129, 126, 110, 111, 109, 141, 120, 117, 106, 149, 122, 122, 110, 118, 127, 121, 114, 125, 126, 114, 140, 103,
     130, 141, 117, 106, 114, 121, 114, 133, 137, 92, 121, 112, 146, 97, 137, 105, 98, 117, 112, 81, 97, 139, 113, 134,
     106, 144, 110, 137, 137, 111, 104, 117, 100, 111, 101, 110, 105, 129, 137, 112, 120, 113, 133, 112, 83, 94, 146,
     133, 101, 131, 116, 111, 84, 137, 115, 122, 106, 144, 109, 123, 116, 111, 111, 133, 150]

# 计算组数
d = 3 # 组距
num_bins = (max(a) - min(a))//d
# 如果极差不能被设置的组距整除，那么绘制的图形会有所偏差

# 设置图形大小
plt.figure(figsize=(20, 8), dpi=80)

# 绘制直方图
plt.hist(a, num_bins)

# 调整x轴
plt.xticks(range(min(a), max(a)+d, d))

# 绘制网格
plt.grid()

# 展示
plt.show()
```

## 常见问题总结

- 应该选择那种图形来呈现数据

- matplotlib.plot(x,y)

- matplotlib.bar(x,y)

- matplotlib.scatter(x,y)

- matplotlib.hist(data,bins,normed)

- xticks和yticks的设置

- label和titile,grid的设置

- 绘图的大小和保存图片

## matplotlib使用的流程总结

1. 明确问题

2. 选择图形的呈现方式

3. 准备数据

4. 绘图和图形完善

## matplotlib绘制更多图形

matplotlib支持的图形是非常多的，如果有其他的需求，我们

可以查看一下url地址：

 http://matplotlib.org/gallery/index.html

## 更多的绘图工具

plotly:可视化工具中的github,相比于matplotlib更加简单,图形更加漂亮,同时兼容matplotlib和pandas



使用用法:简单,照着文档写即可



文档地址: *https://**plot.ly**/python/*























