# pymongo

> python与mongodb交互需要使用pymongo模块

- 首先，需要安装pymongo包
  - `pip install pymongo`
- 在python语句中，需要使用pymongo的MongoClient
  - `from pymongo import MongoClient`
- 然后实例化pymongo获取连接对象
  - `client = MongoClient(host="127.0.0.1", port=27017)`本地可以不用写host
- 使用连接对象获取mongodb中的所有数据库
  - `myclient.list_database_names()`

- 访问数据库
  - `myclient[database_name] `
  - `myclient.database_name `

- 获取数据库下所有集合
  - `db.list_collection_names()`

- 使用目标集合
  - `db[collection_name]`
  - `db.collection_name`

- 也可以直接从连接对象获取集合
  - `myclient[databasename][collectionname]`
  - `myclient.databasename.collectionname`


```python
# 获取数据库连接对象
myclient = pymongo.MongoClient(host="localhost", port=27017)

# myclient.list_database_names() 获取所有数据库名称
print(myclient.list_database_names())

# myclient[database_name] 访问目标数据库
db = myclient["test"]

# db.list_collection_names() # 获取数据库下所有的集合名称
print(db.list_collection_names())

# db[collection_name] 使用目标集合
col = db["table"]
```



### 插入数据

- 插入一条数据

  - `collection.insert({"_id": 10010, "name": "xiaowang ", "age": 10})`

- 插入多条数据，将多条数据存入一个列表中，一次性插入

- ```python
  data_list = [{"name": "test{}".format(i)} for i in range(10)]
  collection.insert_many(data_list)
  
  # col.insert_one() 给集合中插入一条数据, 数据格式为字典格式
  # col.insert_many() 给集中中同时添加多条数据, 数据格式为列表内嵌套字段
  ```

### 删除数据

- 删除一条数据
  - delete_one
  - `collection.delete_one({"name": "xiaowang"})`
- 删除多条数据
  - delete_many
  - `collection.delete_many({"name": "xiaowang"})`

```python
# col.delete_one() 删除一条数据, 括号中可写条件
col.delete_one()

# col.delete_many() 删除多条数据, 括号中写条件, 如果不指定条件则删除集合中的所有数据
col.delete_many()
```

### 修改数据

- 更新一条数据
  - update_one
  - `collection.update_one({"name":"xiaowang"},{"$set":{"name":"new_xiaowang"}})`
- 更新多条数据
  - update_many
  - `collection.update_many({"name":"xiaowang"},{"$set":{"name":"new_xiaowang"}})`

```python
# 更新一条数据
col.update_one({"name":"xiaowang"},{"$set":{"name":"new_xiaowang"}})

# 更新多条数据
col.update_many({"name":"xiaowang"},{"$set":{"name":"new_xiaowang"}})
```

### 查询数据

- 查询一条数据
  - find_one==查找并返回一个结果，接收一个字典类型的条件
  - `ret = collection.find_one({"name": "xiaowang"})`
- 查询多条数据
  - 直接使用find就可以了，如果查询结果为多个值，则返回一个游标对象,可以使用for遍历游标对象
  - ret = collection.find({"name": "xiaowang"})

- 聚合框架查询
  - 在pymongo中使用aggregate通过聚合框架进行查询
  - `col.aggregate([管道1, 管道2, 管道3, .....])`
  - 具体管道使用查阅[Mongodb](/database/MongoDB/数据查询.md)

```python

# 查询数据
# col.find_one() 查询返回一条结果, 括号中可写条件, 具体代码格式与mongodb查询代码一致
# col.find
result = col.find_one({"股票名称": "康德莱"})
print(result)

# col.find() 查询所有数据, 括号中可写条件, 具体代码格式与mongodb中查询代码一致, 返回可迭代对象<class 'pymongo.cursor.Cursor'>
result2 = col.find({"股票名称": "康德莱"})
print(type(result2))
for i in result2:
    print(i)

# col.aggregate() 使用聚合框架查询所有数据, 具体代码格式与mongodb中查询代码一致, 返回可迭代对象<class 'pymongo.cursor.Cursor'>
result3 = col.aggregate([
	{"$group":{
		"_id":"null",
		"count":{"$sum":1}
	}},
	{"$project":{"_id":0, "count":1}}
])

print(result3)
for n in result3:
    print(n)

```



