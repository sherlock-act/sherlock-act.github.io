# Python Django使用



## 认识Django

[参考文档]( https://docs.djangoproject.com/ )

### 1、MVC框架

mvc框架是一种软件设计模式

* 简介

  MVC的生产理念：<font color=red>分工</font>。让专门的人去做专门的事情。

  MVC的核心思想：<font color=red>解耦</font>

  MVC的思想被应用在web开发方面，就产生了<font color=red>web MVC框架</font>

* Web MVC框架的模块功能

![Web MVC框架原理](images\Web MVC框架原理.png)



1. M: Model,模型，与数据库进行交互。
2. V: View,视图，产生html页面。
3. C: Controller，控制器，接收请求，进行处理，与M和V进行交互，返回应答。

---

### 2、Django框架

* 简介
  Django框架遵循MVC的思想，但是有自己的名词，叫做<font color=red>MVT</font>
  Django遵循<font color=red>快速开发</font>和<font color=red>DRY</font>的原则。DRY：Do not repeat yourself。

![Django框架原理](images\Django框架原理.png)



1. M:Model,模型， 和MVC中M功能相同，和数据库进行交互。

2. V:View,视图， 和MVC中C功能相同，接收请求，进行处理，与M和T进行交互，返回应答。

3. T:Template,模板， 和MVC中V功能相同，产生html页面。