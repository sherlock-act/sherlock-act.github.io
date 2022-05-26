# EL表达式

- tomcat项目中，JSP页面与Servlet之间，使用传统方式获取request对象中的值的时候有以下缺点
  - JSP页面中必须要导包
  - 数据必须进行强制类型转换
  - 层次结构非常复杂
- 所以就引入了EL表达式
  - 概念：
    - EL（Expression Language），一种写法非常简单的表达式，语法简单易懂，便于使用  
  - 作用：
    - 让jsp书写起来更加的方便。简化在jsp中获取作用域或者请求数据的写法
  - 语法规则：
    - `${expression},可以使用.或者[]来获取属性值或者指定索引位置的对象`
    - 获取值的时候，直接使用作用域中的key即可，然后使用 . 来引用属性，使用 [] 来获取指定索引位置的对象
  - 作用域：
    - pageContext--->request--->session--->application
  - 获取作用域数据的顺序：
    - 从小的作用域开始查询，如果找到则返回对应的值，不接着向大范围寻找数据
    - 当四种作用域中存在相同key的属性的时候，可以通过pageScope，requestScope，sessionScope，applicationScope获取指定作用域的数据
  - EL表达式可以进行算术运算和关系运算
    - 直接在表达式中写入算法操作即可，如果是关系运算，返回true或者false
    - 注意：在el表达式中的+表示加法操作而不是字符串连接符
  - EL表达式可以进行逻辑运算
    - `${true&&false}`
    -  `${true&&true}`
    - `${true||false}`
    - `${true||true}`
  - EL表达式获取header信息
    - `${header}`:获取所有请求头信息
    - `${header[key]}`:获取指定key的数据
    - `${headerValues[key]}`:获取key对应的一组数据，返回类型是数组
    - `${headervalues[key][0]}`:获取key对应数组的某一个值
  - EL表达式获取cookie数据
    - `${cookie}`:获取cookie中的所有数据
    - `${cookie.key}`：获取cookie中指定key的数据
    - `${cookie.key.name}`：获取cookie指定key数据的name
    - `${cookie.key.value}`：获取cookie指定key数据的value

## 首先在serlvet中给request添加属性

```java
public class ELServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request,response);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //设置请求响应的编码格式
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");

        //从请求中获取数据
        String name = request.getParameter("name");
        String pwd = request.getParameter("pwd");
        System.out.println(name);
        System.out.println(pwd);
        
        //给request对象单独设置属性
        request.setAttribute("job","无线网络优化");
        
        //给request添加对象
        User user = new User(1,"张三",new Address("四川省","成都市","郫都区"));
        User user2 = new User(2,"张三",new Address("四川省","德阳市","绵竹市"));

        ArrayList<User> list  =new ArrayList<>();
        list.add(user);
        list.add(user2);
        
        // 给request添加user对象
        request.setAttribute("user",user);

        //给request对象设置集合
        request.setAttribute("list",list);

        //给reqeust对象设置map对象
        HashMap<String,String> map = new HashMap<>();
        map.put("china","sichuan");
        map.put("sichuan","chengdu");

        request.setAttribute("map",map);

        HashMap<String,User> map2 = new HashMap<>();
        map2.put("a1",user);
        map2.put("a2",user2);

        request.setAttribute("map2",map2);

        //通过请求转发的方式跳转到某一个jsp页面
        request.getRequestDispatcher("el.jsp").forward(request,response);
    }
}
```

## 然后在JSP页面中获取request的属性

```JSP
<%@ page import="com.shanlei.entity.User" %>
<%@ page import="java.util.HashMap" %>
<%@ page import="java.util.ArrayList" %>

<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/3/11
  Time: 21:40
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<!--使用传统方式获取作用域中的值-->
name:<%=request.getParameter("name")%>
pwd:<%=request.getParameter("pwd")%>
job:<%=request.getAttribute("job")%>
town1:<%=((User)request.getAttribute("user")).getAddress().getTown()%>
town2：<%=((User)((ArrayList)request.getAttribute("list")).get(1)).getAddress().getTown()%>
mapvalue:<%=((HashMap)request.getAttribute("map")).get("china")%>
mapUser:<%=((User)((HashMap)request.getAttribute("map2")).get("a1")).getAddress().getTown()%>

<!--
使用传统方式获取request对象中的值有一下缺点
1、必须要导入包
2、进行类型的强制转换
3、层次结构比较复杂

解决办法使用EL表达式
-->
<br>
<%--使用EL表达式获取作用域中的值--%>

<%--直接获取请求中所携带的参数--%>
name:${param.name}
pwd:${param.pwd}

<%--获取给request设置的attribute--%>
job:${job}

<%--获取user对象的属性--%>
town1:${user.address.town}

<%--获取list中的对象的属性--%>
town2：${list[1].address.town}

<%--获取map中的属性--%>
mapvalue:${map.china}

<%--获取map中的对象的属性--%>
mapUser:${map2.a1.address.town}

</body>
</html>
```

## EL表达式获取四个作用域中相同key的属性

```JSP
<%-- 获取不同作用域的相同key的值 --%>
pageContext:${pageScope.key}
<br>
pageContext:${requestScope.key}
<br>
pageContext:${sessionScope.key}
<br>
pageContext:${applicationScope.key}
```

## EL表达式进行算术运算与关系运算

```jsp
<%--使用EL表达式进行基本运算--%>
${1+2}<br>
${1-2}<br>
${1*2}<br>
${1/2}<br>
${1<2}<br>
<%--EL表达式同样可以进行三目运算--%>
${1<2?"男":"女"}
```

## EL表达式获取header中的信息

```jsp
<%--EL表达式获取header信息--%>
${header}
<br>
${header["host"]}
<br>
${headerValues["accept-language"][0]}
```

## EL表达式获取cookie中的信息

```jsp
<%--获取cookie--%>
${cookie}
<br>
${cookie.JSESSIONID}
<br>
${cookie.JSESSIONID.name}
<br>
${cookie.JSESSIONID.value}
```

## EL表达式进行逻辑运算

```jsp
<%--EL表达式逻辑运算--%>
${true&&false}<br>
${true&&true}<br>
${true||false}<br>
${true||true}<br>
```

