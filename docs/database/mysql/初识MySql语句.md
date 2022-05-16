# 初识MySQL语句

```mysql
## 单行注释
/*
多行注释
多行注释
*/
/*
建立一张用来存储学生信息的表
字段包含学号、姓名、性别，年龄、入学日期、班级，email等信息
*/
-- 创建数据库表  --也是注释
create table t_student(
	sno int(6),-- 6代表显示长度
	sname varchar(10), -- 10代表10个字符
	sex char(1),
	age int(3),
	enterdate date,
	classname varchar(10),
	email varchar(15)
);

-- 查看表的结构 , 展示表的详细信息
desc t_student;

-- 查看表中的数据
select * from t_student;

-- 查看建表语句
show create table t_student;
/*
CREATE TABLE `t_student` (
  `sno` int DEFAULT NULL,
  `sname` varchar(10) DEFAULT NULL,
  `sex` char(1) DEFAULT NULL,
  `age` int DEFAULT NULL,
  `enterdate` date DEFAULT NULL,
  `classname` varchar(10) DEFAULT NULL,
  `email` varchar(15) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
*/
```

