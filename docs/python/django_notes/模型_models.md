# model

- **Model (模型)**： 简而言之即数据模型。模型不是数据本身（比如数据库里的数据），而是抽象的描述数据的构成和逻辑关系。通常模型包括了数据表的各个字段（比如人的年龄和出生日期）和相互关系（单对单，单对多关系等)。Web开发框架会根据模型的定义来自动生成数据表。
- 所有的模型类都需要继承自models.Model,这个类中有很多“魔法”操作，比如会给每个继承的子类添加一个DoesNotExist属性，进行数据库中数据和Python对象之间的转换操作等。

```python
from django.db import models # 所有的模型类都需要继承自models.Model


class Blog(models.Model):
    """博客类"""
    title = models.CharField("标题", max_length=200)
    author = models.CharField("作者", max_length=200)
    content = models.TextField("内容")

    def __str__(self):
        return self.title
```

