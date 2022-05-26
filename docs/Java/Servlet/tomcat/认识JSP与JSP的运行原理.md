# 认识JSP与JSP的简单运行原理

## 什么是JSP

- JSP（全称为Java Server Page），是sun公司为主导创建的一种动态网页技术标准，主要的目的就是将标识逻辑从servlet中分离出来
- 它实现了Html语法中可以嵌入java编码的扩展（以 <%, %>形式）。JSP与Servlet一样，是在服务器端执行的。通常返回给客户端的就是一个HTML文本，因此客户端只要有浏览器就能浏览。
- 一般在web项目中，采用JSP+Servlet+JavaBean的技术（SSM）
- JSP本质上就是Servlet，JSP也是Java类，通过JSP引擎将JSP转译成Servlet
- 常见的集中动态网页技术：
  - JSP(Java Server Page)
  - ASP(Active Server Page)
  - PHP(Hypertext Preprocessor) 超文本预处理语言

## JSP的继承结构

- JSP文件转换成JAVA代码之后,它默认继承了HttpJSPBase,实现了JSPSourceDependent,和JSPSourceImports两个接口,其中HttpJSPBase又继承了HttpServlet ,也就是说,JSP本质上就是一个Servlet

## JSP的简单运行原理

![JSP执行过程](E:\Study\study_note\Java\Servlet\tomcat\imgs\JSP执行过程.png)

1. 客户端发出Request请求
2. JSP Container 将JSP转译成Servlet的源代码.java文件
3. 将产生的Servlet源代码经过编译后.生成字节码.class文件
4. 将.class字节码文件加载进入内存并执行,其实就是在运行一个Servlet
5. 通过Response对象将数据响应给浏览器

### JSP的加载引擎

- 通过查看tomcat web.xml我们发现,这里默认配置了一个JSP的加载引擎—JSPServlet

```xml
<servlet>
    <servlet-name>jsp</servlet-name>
    <servlet-class>org.apache.jasper.servlet.JspServlet</servlet-class>
    <init-param>
        <param-name>fork</param-name>
        <param-value>false</param-value>
    </init-param>
    <init-param>
        <param-name>xpoweredBy</param-name>
        <param-value>false</param-value>
    </init-param>
    <load-on-startup>3</load-on-startup>
</servlet>
```

- 匹配路径规则如下：

```xml
<servlet-mapping>
    <servlet-name>jsp</servlet-name>
    <url-pattern>*.jsp</url-pattern>
    <url-pattern>*.jspx</url-pattern>
</servlet-mapping>
```

- 通过上面的代码可以发现，浏览器在请求JSP的时候都会被JSP加载引擎匹配

### 转译JSP页面：

- 将JSP页面翻译成一个Servlet，这个Servlet是一个java文件，同时也是一个完整的java程序

### 编译JSP对应java文件：

- JSP引擎调用java编译器对这个Servlet进行编译，得到可执行文件class

### 请求处理阶段：

- JSP引擎调用java虚拟机来解释执行class文件，生成向客户端发送的应答，然后发送给客户端