# JSTL标签库

## 完整JSTL标签库学习地址[JSTL菜鸟教程](https://www.runoob.com/jsp/jsp-jstl.html)

## 认识JSTL

- JSTL（Java server pages standarded tag library，即JSP标准标签库）是由JCP（Java community Proces）所制定的标准规范，它主要提供给Java Web开发人员一个标准通用的标签库，并由Apache的Jakarta小组来维护

- 支持在jsp页面中添加复杂的逻辑判断，避免逻辑代码和页面标签混为一谈
- JSTL是EL的扩展，同时，JSTL依赖于EL，为了方便的从作用域中获取值

## JSTL的导入

1. 首先在项目的WEB-INF目录下创建lib目录
2. 将`jstl-1.2.jar`的jar包粘贴进lib目录下
3. 右键点击`jstl-1.2.jar`然后点击`Add as Libray`
4. 在jsp页面中核心标签库导入jstl包`<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>`

![使用jstl](E:\Study\study_note\Java\Servlet\tomcat\imgs\使用jstl.png)

## JSTL标签的分类

- 核心标签库
- 格式化标签库
- 函数标签库
- XML标签库
- SQL标签库

## 部分常用核心标签库学习

```jstl
<!--
<c:out value="输出一句话到浏览器"></c:out>
        value：填写要输出的值
        default：默认值

    <c:set var="java" value="pageContext"></c:set>
        var：表示参数的key
        value：表示参数值
        注意：当只配置这两个属性的时候，默认是想pageContext作用域中设置属性，可以通过参数来选择向哪个作用域设置参数
        scope：通过page、request、session、application来设置作用域

    <c:remove var="java"></c:remove><br>
        var：表示参数的key
        scope：指定删除的作用域
        注意：如果scope没有指定的话，那么默认会那所有作用域中key的属性都删除

    <c:if test="${a>5}">
        <h1>study jstl</h1>
    </c:if>
        进行逻辑判断，if判断
        test：填写逻辑判断表达式
        var：条件表达式的结果存储变量
        scope：结果变量存储的作用域

    <c:choose>
        <c:when test="${age<10}">
            <h1>小孩</h1>
        </c:when>
        <c:when test="${age<20}">
            <h1>青年</h1>
        </c:when>
        <c:when test="${age<30}">
            <h1>壮年</h1>
        </c:when>
        <c:when test="${age<40}">
            <h1>中年</h1>
        </c:when>
        <c:otherwise>
            <h1>i don't like</h1>
        </c:otherwise>
    </c:choose>
        进行多重逻辑判断，类似switch

    <c:forEach begin="0" end="4" step="1" varStatus="sta" var="i" items="${list}">
        ${i}
    </c:forEach>
    循环标签
        begin：起始值
        end：结束值
        step：步长
        varStatus：循环状态的变量值名称
        var：结合数据的每条记录的迭代之
        items：从作用域中获取的数据
-->
```

## 部分常用核心标签库代码示例

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt"%>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%
    request.setAttribute("str","china");
    request.setAttribute("hello", "world");
    request.setAttribute("java", "123456");
%>

<%--<c:out></c:out> 输出字符串到浏览器 --%>
<c:out value="输出一句话到浏览器"></c:out><br>
<c:out value="${str2}" default="默认值"></c:out><br>
<c:out value="${hello}"></c:out><br>

<%--<c:set></c:set> 向作用域设置属性值 --%>
<c:set var="java" value="pageContext" scope="page"></c:set>
<c:set var="java" value="request" scope="request"></c:set>
<c:set var="java" value="session" scope="session"></c:set>
<c:set var="java" value="application" scope="application"></c:set>
<c:out value="${java}"></c:out><br>
<c:out value="${pageScope.java}"></c:out><br>
<c:out value="${requestScope.java}"></c:out><br>
<c:out value="${sessionScope.java}"></c:out><br>
<c:out value="${applicationScope.java}"></c:out><br>

<%--删除作用域的数据--%>
<c:remove var="java" scope="request"></c:remove><br>
<c:out value="${pageScope.java}"></c:out><br>
<c:out value="${requestScope.java}"></c:out><br>
<c:out value="${sessionScope.java}"></c:out><br>
<c:out value="${applicationScope.java}"></c:out><br>

<%--逻辑判断标签--%>
<c:set var="a" value="7"></c:set>
<c:if test="${a>5}">
    <h1>study jstl</h1>
</c:if>

<c:set var="age" value="15"></c:set>
<c:choose>
    <c:when test="${age<10}">
        <h1>小孩</h1>
    </c:when>
    <c:when test="${age<20}">
        <h1>青年</h1>
    </c:when>
    <c:when test="${age<30}">
        <h1>壮年</h1>
    </c:when>
    <c:when test="${age<40}">
        <h1>中年</h1>
    </c:when>
    <c:otherwise>
        <h1>i don't like</h1>
    </c:otherwise>
</c:choose>

<%--循环标签--%>
<c:forEach begin="0" end="3" step="1" varStatus="sta">
    ${sta.index}---${sta.count}---${sta.first}---${sta.last}<br>
</c:forEach>

<%
    ArrayList<String> list = new ArrayList<String>();
    list.add("aaa");
    list.add("bbb");
    list.add("ccc");
    list.add("ddd");
    list.add("eee");
    request.setAttribute("list",list);

    HashMap<String, String> map = new HashMap<String, String>();
    map.put("zhangsan", "18");
    map.put("lisi", "17");
    map.put("wangwu", "19");
    request.setAttribute("map",map);
%>
<c:forEach begin="0" end="4" step="1" varStatus="sta" var="i" items="${list}">
    ${i}
</c:forEach>

<table border="1px">
    <tr>
        <td>姓名</td>
        <td>年龄</td>
    </tr>
<c:forEach begin="0" end="2" step="1" var="i" items="${map}">
    <tr>
        <td>${i.key}</td>
        <td>${i.value}</td>
    </tr>
</c:forEach>
</table>
</body>
</html>
```

