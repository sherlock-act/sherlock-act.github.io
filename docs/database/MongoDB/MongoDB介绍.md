# MongoDB介绍

## NoSQL是什么？

- NoSQL，指的是非关系型的数据库，相比于sql关系型数据库来说
- NoSQL = Not Only SQL ，意即"不仅仅是SQL"
- NoSQL用于超大规模数据的存储，这些类型的数据存储不需要固定的模式，无需多余操作就可以横向扩展
  - 今天我们可以通过第三方平台很容易的访问和抓取数据：用户的个人信息，社交网络，地理位置
  - 数据采集过程中，由于采集字段无法完全确定，用nosql更简单、直接
- 优点
  - 高可扩展性
  - 分布式计算
  - 低成本
  - 架构的灵活性，半结构化数据
  - 没有复杂的关系
- 缺点
  - 没有标准化
  - 有限的查询功能（到目前为止）
  - 最终一致是不直观的程序
- 我们选择哪种Nosql数据库？
  - MongoDB：文档存储一般用类似json的格式存储，存储的内容是文档型的。这样也就有机会对某些字段建立索引，实现关系数据库的某些功能

## 什么是MongoDB？

- 概念
  - MongoDB 是一个基于分布式文件存储的数据库。由 C++ 语言编写。旨在为 WEB 应用提供可扩展的高性能数据存储解决方案
  - MongoDB是非关系数据库
- 存储对象
  - MongoDB 将数据存储为一个文档，数据结构由键值(key=>value)对组成
  - MongoDB 文档类似于 JSON 对象，字段值可以包含其他文档，数组及文档数组
- 特点
  - MongoDB安装简单
  - MongoDB 是一个面向文档存储的数据库，操作起来比较简单和容易。
  - 你可以在MongoDB记录中设置任何属性的索引 (如：FirstName="Sameer",Address="8 Gandhi Road")来实现更快的排序
  - MongoDB支持各种编程语言:RUBY，**PYTHON**，JAVA，C++，PHP，C#等多种语言

- MongoDB安装

  - 安装mongo
    - win
      - MongoDB 提供了可用于 32 位和 64 位系统的预编译二进制包，你可以从MongoDB官网下载安装
      - https://www.mongodb.com/download-center/community
    - mac
      - MongoDB 提供了 OSX 平台上 64 位的安装包，你可以在官网下载安装包
      - https://www.mongodb.com/download-center/community

## MongoDB概念解析

  - 关系型数据管理系统与mongodb中概念的对应关系（RDBMS - MongoDB）
    - 数据库 - 数据库
    - 表格 - 集合
    - 行 - 文档
    - 列 - 字段
  - 数据库：database
    - 概念
      - 一个mongodb中可以建立多个数据库。
      - MongoDB的默认数据库为"db"，该数据库存储在data目录中
      - MongoDB的单个实例可以容纳多个独立的数据库，每一个都有自己的集合和权限，不同的数据库也放置在不同的文件中
  - 数据库表/集合：collection
    - 概念
      - 集合就是 MongoDB 文档组
      - 集合存在于数据库中，集合没有固定的结构，这意味着你在对集合可以插入不同格式和类型的数据，但通常情况下我们插入集合的数据都会有一定的关联性
    - 注意，集合命名问题
      - 集合名不能是空字符串""
      - 集合名不能含有\0字符（空字符)，这个字符表示集合名的结尾
      - 集合名不能以"system."开头，这是为系统集合保留的前缀
      - 用户创建的集合名字不能含有保留字符。有些驱动程序的确支持在集合名里面包含，这是因为某些系统生成的集合中包含该字符。除非你要访问这种系统创建的集合，否则千万不要在名字里出现$
  - 数据记录行/文档：document
    - 概念
      - 文档是一组键值(key-value)对，类似python中的字典对象，但不完全一样
    - 注意
      - 文档中的键/值对是有序的
      - MongoDB区分类型和大小写
      - MongoDB的文档不能有重复的键
      - 文档的键是**字符串**。除了少数例外情况，键可以使用任意UTF-8字符
    - 示例
      - `{"name": "farbird", "age":18}`
  - 数据字段/域：field
  - 索引：index
  - 主键：primary key
    - MongoDB自动将_id字段设置为主键

## MongoDB数据类型

  - **String 字符串。存储数据常用的数据类型。在 MongoDB 中，UTF-8 编码的字符串才是合法的**
  - **Integer 整型数值。用于存储数值。根据你所采用的服务器，可分为 32 位或 64 位**
  - **Boolean 布尔值。用于存储布尔值（真/假）**
  - **Double 双精度浮点值。用于存储浮点值**
  - **Timestamp 时间戳。记录文档修改或添加的具体时间。**
  - Min/Max keys 将一个值与 BSON（二进制的 JSON）元素的最低值和最高值相对比。
  - Array 用于将数组或列表或多个值存储为一个键。
  - Object 用于内嵌文档。
  - Null 用于创建空值。
  - Symbol 符号。该数据类型基本上等同于字符串类型，但不同的是，它一般用于采用特殊符号类型的语言。
  - Date 日期时间。用 UNIX 时间格式来存储当前日期或时间。你可以指定自己的日期时间：创建 Date 对象，传入年月日信息。
  - Object ID 对象 ID。用于创建文档的 ID。
  - Binary Data 二进制数据。用于存储二进制数据。
  - Code 代码类型。用于在文档中存储 JavaScript 代码。
  - Regular expression 正则表达式类型。用于存储正则表达式。