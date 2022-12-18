## Django使用

### 1.创建Django项目

命令：`django-admin startproject 项目名`

项目目录如下：

```
yangyi@yangyi-virtual-machine:~/桌面/test2$ tree
.
├── manage.py
└── test2
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

* `__init__.py`说明test2是一个python包
* `settings.py`整个项目的配置文件
* `urls.py`进行url路由的配置
* `wsgi.py`web服务器和Django交互的入口
* `manage.py`项目的管理文件

---

### 2、创建Django应用

&emsp;在Django中，一个<font color=red>功能模块</font>分别使用一个<font color=red>应用</font>来实现，整个项目由很多个应用组成，每一个应用完成一个功能模块，例如：整个网页可以分为<font color=red>用户模块、商品模块、购物模块、订单模块</font>。

命令：`python manage.py startapp 应用名`

<font color=red>注意：创建应用的时候，需要先进入项目目录内</font>

应用目录如下：

```
yangyi@yangyi-virtual-machine:~/桌面/test2/booktest$ tree
.
├── admin.py
├── __init__.py
├── migrations
│   ├── __init__.py
├── models.py
├── tests.py
└── views.py
```

* `__init__.py`: 说明目录是一个Python模块。
* `models.py`: 写和数据库项目的内容, 设计模型类。
* `views.py`: ，接收请求，进行处理，与M和T进行交互，返回应答。
* `tests.py`: 写测试代码的文件。
* `admin.py`: 网站后台管理相关的文件。

---

### 3、Django应用注册

&emsp;应用创建后，为了建立应用和项目之间的联系，需要对<font color=red>应用进行注册</font>，注册的方法：修改`settiongs.py`中的`INSTALLED_APPS`的配置

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'booktest', # 注册应用，以上的应用都是Django项目自带的应用
]
```

---

### 4、启动Django项目

运行开发web服务器命令

```shell
python manage.py runserer											# 默认在本地8000端口启动项目,不支持外部访问
python manage.py runserver  6000							# 使用本地连接6000端口启动,
python3 manage.py runserver 0.0.0.0:6000 			# 使用6000端口启动,支持局域网访问
```



