### Django使用mysql数据库

1. **创建项目使用的数据库**

`create database python_study charset=utf8;`

2. **Django中配置使用mysql数据库，修改`setting.py`中的`DATABASES`**

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'python_study',
        'USER': 'root',
        'PASSWORD': '310585',
        'HOST': 'localhost',
        'PORT': 3306,
    }
}
```

3. **修改__init__文件或下载mysqlclient**
 ```python
 pip install mysqlclient=2.0.3
 ```

```
import pymysql


pymysql.install_as_MySQLdb()
```

4.**mysql的日志文件**

&emsp;mysql.log是mysql的日志文件，里面记录的对MySQL数据库的操作记录。默认情况下mysql的日志文件没有产生，需要修改mysql的配置文件，步骤如下：

* 使用下面的命令打开mysql的配置文件，去除68,69行的注释，然后保存。

`sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf`

* 重启mysql服务，就会产生mysql日志文件。

`sudo service mysql restart `

* 打开MySQL的日志文件。

`/var/log/mysql/mysql.log `是mysql日志文件所在的位置。

* 使用下面的命令可以实时查看mysql的日志文件:

`sudo tail -f /var/log/mysql/mysql.log `