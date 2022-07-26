# manage常用命令

## 创建项目

```shell
# 终端中使用
django-admin.py startproject mysite

# 创建后目录树结构如下
.
├── mysite							项目目录
│   ├── __init__.py			初始化文件
│   ├── asgi.py					
│   ├── settings.py			项目设置文件
│   ├── urls.py					路由设置文件,即访问url和业务逻辑的对应关系
│   └── wsgi.py					项目部署使用文件
└── manage.py						项目管理文件
```

## 创建应用

1. 使用命令生成应用

```shell
# 终端中执行
python manage.py startapp appname

# 创建后目录结构如下
.
├── blog
│   ├── __init__.py											应用初始化文件
│   ├── admin.py												应用后台管理相关
│   ├── apps.py													应用设置信息
│   ├── migrations											数据库变更记录
│   │   └── __init__.py
│   ├── models.py												模型,数据库相关
│   ├── tests.py												测试相关,单元测试编写在这个脚本
│   └── views.py												视图相关,编写视图函数和类
├── db.sqlite3
├── demo
│   ├── __init__.py
│   ├── __pycache__
│   │   ├── __init__.cpython-38.pyc
│   │   ├── settings.cpython-38.pyc
│   │   ├── urls.cpython-38.pyc
│   │   └── wsgi.cpython-38.pyc
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── manage.py
```

2. 将应用添加到项目的setting.py中

- 应用只用在`INSTALLED_APPS`中设置后,应用中的模型、静态文件、模板等才能正常工作。如果添加了一个Python包，只是把公用的部分提取出来，放到一个公用的目录中，那么这个目录不需要加入到INSTALLED_APPS中，因为对于Django而言它不是一个应用。

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog' # 将新应用添加到项目中
]
```





## 项目调试启动

```shell
# 终端中执行
python manage.py runserver

# 也可以在运行的时候指定端口和ip地址
python manage.py runserver 8080   # 使用8080端口,默认就是8000
python manage.py runserver 0.0.0.0:8080 # 允许所有其他ip地址访问
python manage.py runserver 0:8080 # 允许所有其他ip地址访问
```



# 使用模型类在数据库中创建对应表格

- 首先需要使用`makemigrations`生成模型类与数据库表中的差异文件

```shell
python manage.py makemigrations blog

# 这个命令会检查app blog中的模型的变更，会发现其中创建了一个Blog类
# 输出如下:
Migrations for 'blog':
  blog/migrations/0001_initial.py
    - Create model Blog
```

- 然后使用`migrate`将模型的类对应的表格信息在数据库中进行创建

```shell
python manage.py migrate bolo

# 输入内容如下
$ python manage.py migrate blog￼
Operations to perform:￼
	Apply all migrations: blog￼
Running migrations:￼
	Applying blog.0001_initial... OK
```

## 创建admin站点

- 首先需要创建一个管理员账号,用于系统登录

```shell
python manage.py createsuperuser

# 用于创建超级管理员用户
```

- 在`admin.py`中添加后台信息的设置

```python
from django.contrib import admin
from blog.models import Blog


@admin.register(Blog)
class BlogAdmin(admin.ModelAdmin):

    # list_display控制在管理员页面每天记录显示的字段名有哪些
    list_display = ["title", "author"]

    # seatch_fields控制参与搜索的字段列表
    search_fields = ["title", "author"]
```

- [点击查看更多ModelAdmin常用属性](./ModelAdmin常用属性与方法.md)

## 修改中文显示

- 在`setting.py`文件中,将`LANGUAGE_CODE`修改为`zh-hans`

```python
# LANGUAGE_CODE = 'en-us'  en-us页面显示为英文
LANGUAGE_CODE = 'zh-hans' # zh-hans 简体中文  zh-hant 繁体中文
```



