# 模型类

## ORM

&emsp;django中内嵌了ORM框架，ORM框架可以将类和数据表进行对应，只需要通过类和对象就可以对数据表进行操作。

在Django中主要的设计类：<font color=red>模型类</font>

ORM的另一作用：<font color=red>根据设计的类，生成数据库中的表</font>

### 模型类的设计

&emsp;设计模型类，需要在应用的`models.py`中进行

&emsp;模型类必须继承`models.Model`类

```python
from django.db import models

# Create your models here.


# 一类
class Department(models.Model):
    """部门表"""
    title = models.CharField(max_length=32, verbose_name="标题")

    # 修改str方法返回自己的title
    def __str__(self):
        return self.title


class UserInfo(models.Model):
    """员工表"""
    name = models.CharField(verbose_name="姓名", max_length=16)
    password = models.CharField(verbose_name="密码", max_length=64)
    age = models.IntegerField(verbose_name="年龄")
    account = models.DecimalField(verbose_name="余额", max_digits=10, decimal_places=2, default=0)
    create_time = models.DateField(verbose_name="入职时间")
    
    # 设置gender的取值范围
    gender_choices = ((1, "男"), (0, "女"))
    gender = models.SmallIntegerField(verbose_name="性别", choices=gender_choices)
    
    # 设置外键,让两个表产生关联
    depart = models.ForeignKey(verbose_name="部门", to="Department", to_field="id", on_delete=models.CASCADE)
```

&emsp;<font color=red>Models.ForeignKey</font>可以建立两个模型类之间一对多的关系，django在生成表的时候，就会在多端的表中创建一列作为外键，建立两个表之间一对多的关系。

### 模型类的字段属性和选项

1. **模型类属性命名限制**

* 不能是python的保留关键字
* 不允许使用连续的下划线（这是由于Django的查询方式决定的）
* 定义属性时，需要指定字段类型，通过字段类型的参数指定选项，例：<font color=red>属性名=models.字段类型(选项)</font>

2. **字段类型**

|                          类型                          |                             描述                             |
| :----------------------------------------------------: | :----------------------------------------------------------: |
|                     **AutoField**                      | 自动增长的IntegerField，通常不用指定，不指定时Django会自动创建属性名为id的自动增长属性。 |
|                    **BooleanField**                    |                 布尔字段，值为True或False。                  |
|                  **NullBooleanField**                  |                支持Null、True、False三种值。                 |
|           **CharField**(max_length=最大长度)           |           字符串。参数max_length表示最大字符个数。           |
|                     **TextField**                      |            大文本字段，一般超过4000个字符时使用。            |
|                    **IntegerField**                    |                             整数                             |
| **DecimalField**(max_digits=None, decimal_places=None) | 十进制浮点数。参数max_digits表示总位。参数decimal_places表示小数位数。 |
|                     **FloatField**                     |                       浮点数。参数同上                       |
| **DateField：**([auto_now=False, auto_now_add=False])  | 日期。  1)参数auto_now表示每次保存对象时，自动设置该字段为当前时间，用于"最后一次修改"的时间戳，它总是使用当前日期，默认为false。  2) 参数auto_now_add表示当对象第一次被创建时自动设置当前时间，用于创建的时间戳，它总是使用当前日期，默认为false。  3)参数auto_now_add和auto_now是相互排斥的，组合将会发生错误。 |
|                     **TimeField**                      |                   时间，参数同DateField。                    |
|                   **DateTimeField**                    |                 日期时间，参数同DateField。                  |
|                     **FileField**                      |                        上传文件字段。                        |
|                     **ImageField**                     |  继承于FileField，对上传的内容进行校验，确保是有效的图片。   |

3. **选项**

|      选项名      |                             描述                             |
| :--------------: | :----------------------------------------------------------: |
|   **default**    |                     默认值。设置默认值。                     |
| **primary_key**  | 若为True，则该字段会成为模型的主键字段，默认值是False，一般作为AutoField的选项使用。 |
|    **unique**    |   如果为True, 这个字段在表中必须有唯一值，默认值是False。    |
|   **db_index**   |   若值为True, 则在表中会为此字段创建索引，默认值是False。    |
|  **db_column**   |          字段的名称，如果未指定，则使用属性的名称。          |
|     **null**     |          如果为True，表示允许为空，默认值是False。           |
|    **blank**     |       如果为True，则该字段允许为空白，默认值是False。        |
| **verbose_name** |                           字段别名                           |

<font color=red>         对比：null是数据库范畴的概念，blank是后台管理页面表单验证范畴的  </font>

&emsp;当修改模型类之后，如果添加的选项不影响表的结构，则不需要重新做迁移，商品的选项中default和blank不影响表结构。

### 模型类生成表

1. 首先需要生成迁移文件

&emsp;命令：`python manage.py makemigrations`

&emsp;这样在应用的`migrations`文件夹中就会生成迁移文件

2. 执行迁移生成表

&emsp;命令：`python manage.py migrate`

&emsp;根据迁移文件生成表，生成的表名的默认格式：<font color=red>应用名_模型类名小写</font>

### 通过模型类操作数据表

1. 向表中插入一条数据

```Python
# 方式一,实例化对象,然后使用对象调用save函数
dept = Department(title="IT")
dept.save()

# 方式二 使用类对象的create方法
Department.objects.create(title="IT")
```

2. 查询的数据

```python
# filter查询寻来的是一个列表
# 列表中的元素为模型类对象
# 使用first()方法获取第一个元素,如果有元素则获取第一个,没有数据返回None
dept = Department.objects.filter(id=1).first() 

# 查询所有数据
depts = Department.objects.all()
```

3. 修改数据

```Python
# 方法一: 修改对象属性,并调用对象的save方法
dept.title = "运营"
dept.save() #才会更新表格中的数据

# 方法二:调用update方法
Department.objects.filter(id=1).update(title="运营")
```

4. 删除数据

```python
dept.delete() # 才会删除
```

