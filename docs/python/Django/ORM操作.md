### 模型类的查询操作

* 查询函数：通过`模型类.objects`属性可以调用查询函数，实现对模型类对应的数据表进行查询

|  函数名  |                             功能                             |                       返回值                       |                             说明                             |
| :------: | :----------------------------------------------------------: | :------------------------------------------------: | :----------------------------------------------------------: |
|   get    | 返回表中满足条件的<font  color=red>一条数据，且只能有一条数据</font> |               返回值是一个模型类对象               | 参数中写查询条件。查询到多条数据，抛出异常：MultipleObjectsReturned。查询不到数据抛出异常：DoesNotExist。 |
|   all    |    返回模型类对应表格中的<font  color=red>所有数据</font>    | <font  color=red>返回值是查询集（QuerySet）</font> |                            无参数                            |
|  filter  |          返回<font  color=red>满足</font>条件的数据          | <font  color=red>返回值是查询集（QuerySet）</font> |                        参数写查询条件                        |
| exclude  |         返回<font  color=red>不满足</font>条件的数据         | <font  color=red>返回值是查询集（QuerySet）</font> |                        参数写查询条件                        |
| order_by |                      对查询结果进行排序                      | <font  color=red>返回值是查询集（QuerySet）</font> |                 参数中写根据哪些字段进行排序                 |

* 查询条件：用于查询函数中的条件。条件格式：`模型类属性名__条件名=值`<font color=red>(双下划线)</font>

|    条件    |            解释            |                             示例                             |
| :--------: | :------------------------: | :----------------------------------------------------------: |
|   exact    | 判断是否相等，可直接使用 = |              BookInfo.objects.get(id__exact=1)               |
|  contains  |            包含            |        BookInfo.objects.filter(btitle__contains="传")        |
| startswith |         以什么开头         |       BookInfo.objects.filter(btitle__startswith="部")       |
|  endswith  |         以什么结尾         |        BookInfo.objects.filter(btitle__endswith="部")        |
|   isnull   |           空查询           |        BookInfo.objects.filter(btitle__isnull=False)         |
|     in     |          范围查询          |           BookInfo.objects.filter(id__in=[1,3,5])            |
|     gt     |     大于(greate than)      |              BookInfo.objects.filter(id__gt=3)               |
|     lt     |      小于(less than)       |              BookInfo.objects.filter(id__lt=3)               |
|    gte     |          大于等于          |              BookInfo.objects.filter(id__gte=3)              |
|    lte     |          小于等于          |              BookInfo.objects.filter(id__lte=3)              |
|    year    |          日期查询          | BookInfo.objects.filter(bpub_date__year=1980)      BookInfo.objects.filter(bpub_date__gt=date(1980,1,1)) |
|  order_by  |        从小到大排序        |            BookInfo.objects.all().order_by('id')             |
|  order_by  |        从大到小排序        |            BookInfo.objects.all().order_by('-id')            |

### 查询集

&emsp;all，filter，exclude，order_by，调用这些函数回产生一个查询集，QuerySet类对象可以继续调用上面的所有函数

* **查询集的特性**

1. 惰性查询：<font color=red>只有在实际使用查询集中的数据的时候才会发生对数据库的真正查询。</font>

2. 缓存：<font color=red>当使用的是同一个查询集时，第一次使用的时候会发生实际数据库的查询，然后把结果缓存起来，之后再使用这个查询集时，使用的是缓存中的结果。</font>

*  **限制查询集**  

1. 可以对一个查询集进行取下标或者切片操作来限制查询集的结果。

2. 对一个查询集进行切片操作**会产生一个新的查询集**,下标不允许为负数

示例：

|   方式   |                  说明                  |
| :------: | :------------------------------------: |
|   b[0]   |  如果b[0]不存在，会抛出IndexError异常  |
| exists() | 判断一个查询集中是否有数据。True False |

### 模型类的关系

* 一对多关系

&emsp;例如：图书类-角色类，对应关系定义在多类中

  ```python
# 括号中指定对应的类名,通过on_delete设置删除时的外键策略
models.ForeignKey(on_delete=models.CASCADE) 

# 通过to指定要关联的模型类,to_field指定关联的字段,on_delete设置删除时的外键策略,on_delete必须写
depart = models.ForeignKey(verbose_name="部门", to="Department", to_field="id", on_delete=models.CASCADE)
  ```

* 多对多关系

&emsp;例如：新闻类-新闻类型类，对应关系可以随便定义在哪个类中

```python
models.ManyToManyField() # 括号中指定对应的类名
```

* 一对一关系

&emsp;例如：员工基本信息类-员工详细信息类，对应关系可以随便定义在哪个类中

```python
models.OneToOneField() # 括号中指定对应的类名
```

### 关联查询（一对多关系）

&emsp;多类中定义的建立关联的类新型叫做关联属性

|  查询条件  |                     一般方法                     |            模型类查询             |
| :--------: | :----------------------------------------------: | :-------------------------------: |
| 一类查多类 | ad = Admin.objects.get(id=1)，ad.order_set.all() | Order.objects.filter(admin__id=1) |
| 多类查一类 |     Obj = Order.objects.get(id=1)，obj.admin     |   Admin.objects.filter(order=1)   |

<font color=red>注意：</font>

1. 通过模型类实现关联查询时，要查哪个表中的数据，就需要通过哪个类来差。
2. 写关联查询条件的时候，如果类中没有关系属性，条件需要写对应类的名，如果类中有关系属性，直接写关系属性。

### F对象

&emsp;F对象是用于类属性之间进行比较的，在使用F对象之前，需要先导入F对象`from django.db.models import F`

示例：

```python
# 查询图书阅读量大于评论量的图书信息
BookInfo.objects.filter(bread__gt=F('bcomment'))
# 查询涂上阅读量大于2倍评论量的图书信息
BookInfo.objects.filter(bread__gt=F('bcomment')*2)
```

### Q对象

&emsp;Q对象是用于查询时判断条件之间的逻辑关系<font color=red>not，and，or</font>可以对Q对象进行<font color=red>~，&，|</font>操作。在使用Q对下行之前，需要先导入Q对象`from django.db.models import Q`

示例：

```python
# 查询id大于3且阅读量大于30的图书的信息。
BookInfo.objects.filter(id__gt=3, bread__gt=30)
BookInfo.objects.filter(Q(id__gt=3)&Q(bread__gt=30))
# 查询id大于3或者阅读量大于30的图书的信息。
BookInfo.objects.filter(Q(id__gt=3)|Q(bread__gt=30))
# 查询id不等于3图书的信息。
BookInfo.objects.filter(~Q(id=3))
```

### 自关联

<font color=red>&emsp;自关联就是特殊的一对多的关系</font>;只是所有的关联都在一张表里面，在定义数据表的时候就在表中定义关系属性；<font color=red>自关联查询依然遵循关联查询操作原则</font>

```python
class AreaInfo(models.Model):
    """自关联模型类"""
    # 地区名称
    atitle = models.CharField(max_length=20)
    # 关系属性，代表当前地区的父级地区
    aparent = models.ForeignKey('self', null=True, blank=True)
```

### 聚合函数

&emsp;对查询结果进行聚合；(sum,count,avg,max,min)

* **aggregate：**调用这个函数来使用聚合，返回值是一个字典；

使用前需要先导入<font color=red>聚合类</font>`form django.db.models import Sum,Count,Max,Min,Avg`

示例：

```python
# 查询所有图书的数目。
BookInfo.objects.all().count()
{'id__count': 5}
# 查询所有图书阅读量的总和。
from django.db.models import Avg
Book.objects.aggregate(Avg('price'))
{'price__avg': 34.35}
```

* **count：**统计满足条件数据的数目，返回值是一个数字；

示例：

```python
# 统计所有图书的数目。
BookInfo.objects.all().count()
BookInfo.objects.count()
# 统计id大于3的所有图书的数目。
BookInfo.objects.filter(id__gt=3).count()
```

