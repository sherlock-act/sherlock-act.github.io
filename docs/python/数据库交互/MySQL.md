# pymysql

> python与mysql交互需要使用pymysql模块

- 首先需要安装pymysql模块
  - `pip install pymysql`
  - `conda install pymysql`
- 使用pymysql与mysql数据库交互需要先实例化连接对象
  - `con = pymysql.connect(host='localhost', port=3306, user='root', password='123456', database='test')`
    - host:服务器地址
    - port:mysql端口号
    - user:用户名
    - password:密码
    - database:连接的数据库名称
- 获取指针对象
  - `cur = con.cursor()`
- 执行SQL语句
  - `cur.execute(<SQL script>)`
- 获取查询到的数据
  - `cur.fetchone()` --获取一条数据
  - `cur.fetchall()` --获取所有数据
- 需要注意pymysql默认开启事务,所以如果是执行增删改的操作,需要commit
- 关闭连接
  - `con.close()`