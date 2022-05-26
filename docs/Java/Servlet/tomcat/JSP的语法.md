# JSP语法

## 编译器指令

- page：用来设置转译成servlet文件时的参数
  - `contentType:表示览器解析响应信息的时候使用的编码和解析格式`
  - `language:表示JSP要转译成的文件类型`
  - `import:导入需要的jar包`
  - `pageEncoding:设置页面的编码格式 可以与contentType只选择一个使用，两个同时使用必须保持一致`
  - `session:用来控制Servlet中是否有session对象`
  - `errorPage:当页面发生逻辑错误的时候跳转的页面`
  - `extends:需要转译的servlet类要继承的父类（包名+类名）`

```JSP
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/3/10
  Time: 19:56
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" import="java.util.*" pageEncoding="utf-8" %>
<%@ page session="true" %>
<%@ page errorPage="error.jsp" %>
<html>
<head>
    <title>page</title>
</head>
<body>
    <h1>this is a page</h1>
</body>
</html>

```

## 代码块

- 局部代码块
  - 可以将java代码跟页面展示的标签写到一个jsp页面中，在java代码转译成的servlet文件中，java代码跟输出是保存在service方法中的
  - 缺点：
    - 代码可读性差
    - 开发比较麻烦
    - 所以一般不使用局部代码块
- 全局代码块
  - 定义公共的方法的时候需要使用全局代码块使用<%!%>       生成的代码在servlet类中
  - 调用的时候，需要使用局部局部代码块

```JSP
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/3/10
  Time: 19:56
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>page</title>
</head>
<body>
<h1>this is a page</h1>
<%--  下面是使用局部代码块实现逻辑判断，并按照条件将内容反馈给客户端  --%>
<%
    int i = new Random().nextInt(10);
    if(i>5){
%>
<b>i大于5，则在页面能看到这句话</b>
<%}%>

<%--  使用全局代码块定义一个test方法  --%>
<%!
    public void test(){
        System.out.println("这是一段全局代码块");
    }
%>
<%--全局代码块需要使用局部代码块调用--%>
<%test();%>
</body>
</html>
```

## 脚本语法

- 脚本调用方法：
  - 使用<%=直接调用变量和方法（方法必须有返回值）%>
  - 注意：不能在变量或者方法名后面加;(分号)

```JSP
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/3/10
  Time: 19:56
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>page</title>
</head>
<body>
<h1>this is a page</h1>
<%--脚本调用方法 使用全局代码块定义一个属性与一个方法 --%>
<%! String str = "这是一个String"; %>
<%! public String demo(){
    return "这是一个简单的方法";
}%>
<%--使用脚本调用属性与方法--%>
<%=str%>
<%=demo()%>
</body>
</html>

```

## 页面导入

- 静态导入：
  - `<%@ include file="staticImport.jsp"%>`
  - file中填写的是jsp文件的相对路径使用静态导入页面的时候，不会将静态导入的页面生成一个新的servlet文件，而是将两个文件合并
  - 优点：运行效率高
  - 缺点：两个页面会组合到一起，不利于维护，两个页面中不能存在相同名称的变量
- 动态导入：
  - `<jsp:include page="dynamicImport.jsp"></jsp:include>`
  - 两个页面不会进行合并，分别生成自己的servlet文件，但是页面在最终展示的时候合并到一起
  - 优点：没有耦合，可以存在同名变量

```JSP
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/3/10
  Time: 19:56
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>page</title>
</head>
<body>
<h1>this is a page</h1>
<%--静态导入--%>
<%@ include file="staticImport.jsp"%>

<%--动态导入--%>
<jsp:include page="dynamicImport.jsp"></jsp:include>
</body>
</html>

```

## 请求转发

- 在jsp中也可以实现servlet的请求转发功能
- `<jsp:forward page="forward.jsp"></jsp:forward>`
- page中填写的是jsp文件的相对路径
- 注意：在标签中间，不可以添加任何字符,除了传递参数
- 传递参数：    
  - `<jsp:param name="sichuan" value="chengdu"></jsp:param>`
- 转发后的页面获取属性：    
  - `<%=request.getParameter("sichuan")%>`

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/3/10
  Time: 19:56
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>page</title>
</head>
<body>
<h1>this is a page</h1>
    
<%--请求转发--%>
<jsp:forward page="forward.jsp">
    <jsp:param name="sichuan" value="chengdu"></jsp:param>
</jsp:forward>
    
<%-- 获取转发前页面传递过来的参数 --%>
<%=request.getParameter("sichuan")%>
</body>
</html>

```

## JSP九大内置对象

- JSP页面在转译称为对象的servlet文件的时候，会自动声明一些对象，在JSP页面中直接使用
- 查看JSP生成的servlet的java文件可发现在`_jspService`方法中定义了九个对象

```java
public void _jspService(final javax.servlet.http.HttpServletRequest request, final javax.servlet.http.HttpServletResponse response)
        throws java.io.IOException, javax.servlet.ServletException {

    final javax.servlet.jsp.PageContext pageContext;
    javax.servlet.http.HttpSession session = null;
    final javax.servlet.ServletContext application;
    final javax.servlet.ServletConfig config;
    javax.servlet.jsp.JspWriter out = null;
    final java.lang.Object page = this;
    javax.servlet.jsp.JspWriter _jspx_out = null;
    javax.servlet.jsp.PageContext _jspx_page_context = null;
}
```

- 注意：    
  - 内置对象是在jsp页面中使用的    
  - 可以在局部代码块中使用，也可以在脚本段语句中使用，但是不能再全局代码块中使用
- 九大对象： pageContext、request、session、application这四个对象使用较多
  - pageContext：
    - 表示页面上下文对象，封存成了其他的内置对象，封存了当前页面的运行信息
    - 每一个页面都有一个对象的pageContext对象
    - 伴随着当前页面的结束而结束
  - request：
    - 封装当前请求的数据，由tomcat创建，一次请求对应一个request对象
  - session：
    - 用来封装同一个用户不同请求的共享数据
    - 一次会话对应一个session对象
  - application：
    - 相当于servletContext对象，一个web项目只有一个对象
    - 存储着所有用户的共享数据，从服务器启动到服务器结束
  - response：
    - 响应对象
    - 用来响应请求数据，将处理结果返回给浏览器，可以进行重定向
  - out：
    - 响应对象
    - jsp内部使用，带有缓冲区的响应对象，效率高于response
  - page：
    - 代表当前JSP对象，跟JAVA中的this指针类似
  - exception：
    - 异常对象，存储当前运行的异常信息，必须在page指令中添加 `isErrorPage="true"`
  - config：
    - 相当于ServletConfig对象，用来获取web.xml中配置的数据，完成servlet的初始化操作
- 四大对象的作用域：
  - pageContext：表示当前页面，解决当前页面内的数据共享，获取其他内置对象
  - request：一次请求，一次请求的servlet的数据共享，通过请求转发的方式，将数据流转到下一个servlet
  - session：一次回话，一个用户发送的不同请求之间的数据共享，可以将数据从一个请求流转到其他请求
  - application：项目内，不同用户的数据共享问题，将数据从一个用户流转到其他用户
- 路径问题：
  - 在超链接中，想要获取项目中的资源，可以使用相对路径，也可以使用绝对路径
  - 相对路径：相对于当前页面的路径
    - 问题：1、资源的位子不可以随便更改
    - 问题：2、需要使用../的方式进行文件夹的跳出，如果目录结构比较深，可能操作起来比较麻烦
  - 绝对路径:
    - 在请求路径的前面加 / 表示当前服务器的根路径，使用的时候要添加/虚拟项目名称/资源目录
  - 使用jsp中自带的全局路径声明：
    - 使用request的方法拼接当前目录的绝对路径，然后在页面的head标签中使用base标签定义项目目录路径

```jsp
<%
String path = request.getContextPath();
System.out.println(path);
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
System.out.println(basePath);
%>

<head>
    <base href="<%=basePath%>">
    <title>page</title>
</head>
<body>
    <a href="forward.jsp"></a>
</body>
```