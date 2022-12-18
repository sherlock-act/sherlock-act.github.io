### Django后台管理

1. 需要本地化项目

&emsp;对<font color=red>语言和时区</font>进行本地化，需要修改`settings.py`文件，如下：

``` python
# LANGUAGE_CODE = 'en-us' 将默认的英语语言注释掉
LANGUAGE_CODE = 'zh-hans' # 将语言改为中国汉字

# TIME_ZONE = 'UTC' 将UTC时区注释掉
TIME_ZONE = 'Asia/Shanghai' # 将时区修改为中国，没有北京时间
```

2. 创建管理员

&emsp;命令：`python manage.py createsuperuser`

&emsp;创建管理员的时候需要创建<font color=red>管理员名</font>和<font color=red>管理员密码</font>

3. 创建模型类与自定义管理页面

&emsp;创建模型类就是在`admin.py`中注册模型类，是为django框架指定注册的模型类来生成管理页面。

```python
from django.contrib import admin
from project_test.models import BookInfo, HeroInfo # 需要创建哪些后台管理的类，就需要先将models.py中定义的模型类先导入


# 后台管理相关文件
# Register your models here.
# 自定义一个模型管理类
class BookInfoAdmin(admin.ModelAdmin):
    '''图书模型管理类'''
    
    # 指定后台管理中需要显示的类的哪些属性，这里是在自定义管理页面
    list_display = ['id', 'btitle', 'bpub_date']

class HeroInfoAdmin(admin.ModelAdmin):
    '''英雄模型管理类'''
    
    # 指定后台管理中需要显示的类的哪些属性，这里是在自定义管理页面
    list_display = ['id', 'hname', 'hcomment']
    
    
class AreaInfoAdmin(admin.ModelAdmin):
    '''地区模型管理类'''
    list_per_page = 10 # 指定每页显示10条数据
    list_display = ['id', 'atitle', 'title', 'parent']
    actions_on_bottom = True
    actions_on_top = False
    list_filter = ['atitle'] # 列表页右侧过滤栏
    search_fields = ['atitle'] # 列表页上方的搜索框

    # fields = ['aParent', 'atitle'] # 更改编辑页选项
    fieldsets = (
        ('基本', {'fields':['atitle']}),
        ('高级', {'fields':['aParent']})
    ) # 更改编辑页选项，与fields只能使用一个 给编辑页添加组

    # inlines = [AreaStackedInline]
    inlines = [AreaTabularInline]
    
# 注册模型类
admin.site.register(BookInfo, BookInfoAdmin)
admin.site.register(HeroInfo, HeroInfoAdmin)
admin.site.register(AreaInfo, AreaInfoAdmin)

admin.site.register(PicTest)

```

```python
class AreaInfo(models.Model):
    '''地址模型类'''
    # 地区名称
    atitle = models.CharField(verbose_name='标题', max_length=20)
    # 自关联属性
    aParent = models.ForeignKey('self', null=True, blank=True)

    def __str__(self):
        return self.atitle

    def title(self):
        return self.atitle
    title.admin_order_field = 'atitle'
    title.short_description = '地区名称'

    def parent(self):
        if self.aParent is None:
            return ''
        return self.aParent.atitle
    parent.short_description = '父级地区名称'
```

#### 关联对象

* 块的形式嵌入

1. 打开admin.py文件，创建AreaStackedInline类。 

```python
class AreaStackedInline(admin.StackedInline):
    # model后面写多类的名字
    model = AreaInfo#关联子对象
    # 预留可添加编辑的数据位置，默认3个
    extra = 2#额外编辑2个子对象
```

2. 打开admin.py文件，修改AreaAdmin类如下： 

```python
class AreaAdmin(admin.ModelAdmin):
    ...
    inlines = [AreaStackedInline]
```

* 表格的形式嵌入

1. 打开admin.py文件，创建AreaTabularInline类。

```
class AreaTabularInline(admin.TabularInline):
    model = AreaInfo#关联子对象
    extra = 2#额外编辑2个子对象
```

2. 打开admin.py文件，修改AreaAdmin类如下：

```
class AreaAdmin(admin.ModelAdmin):
    ...
    inlines = [AreaTabularInline]
```

#### 重写模板

1. 在templates/目录下创建admin目录，结构如下图：

2. 打开当前虚拟环境中Django的目录，再向下找到admin的模板，目录如下：

```
/home/python/.virtualenvs/py_django/lib/python3.5/site-packages/django/contrib/admin/templates/admin
```

3. 将需要更改文件拷贝到第一步建好的目录里，此处以base_site.html为例。

编辑base_site.html文件：

```
{% extends "admin/base.html" %}

{% block title %}{{ title }} | {{ site_title|default:_('Django site admin') }}{% endblock %}

{% block branding %}
<h1 id="site-name"><a href="{% url 'admin:index' %}">{{ site_header|default:_('Django administration') }}</a></h1>
<hr>
<h1>自定义的管理页模板</h1>
<hr>
{% endblock %}

{% block nav-global %}{% endblock %}
```

其它后台的模板可以按照相同的方式进行修改



&emsp;未进行定义的模型类，在后台管理中显示的都是模型类的名字，需要改写模型类的魔法方法`__str__`，返回我们希望后台管理中看到的内容

```python
class BookInfo(models.Model):
    """图书模型类"""
    # CharField说明是一个字符串，max_length指定字符串的最大长度
    btitle = models.CharField(max_length=20)
    # 出版日期 Datefield说明是一个日期类型
    bpub_date = models.DateField()

    def __str__(self):
        # 改写魔法属性，返回书名
        return self.btitle
```

---

### 