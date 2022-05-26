# 创建简单的tomcat项目

- 开发工具:IDEA

1. 首先创建一个web工程

![创建tomcat-1](E:\Study\study_note\Java\Servlet\tomcat\imgs\创建tomcat-1.jpg)

工程创建后目录结构

![创建tomcat-2](E:\Study\study_note\Java\Servlet\tomcat\imgs\创建tomcat-2.png)

2. 创建Servlet实现类(在servlet类中实现具体业务逻辑),需要在设置中指定

![创建tomcat-3](E:\Study\study_note\Java\Servlet\tomcat\imgs\创建tomcat-3.png)

- 这里继承HttpServlet的时候,找不到父类,需要在项目结构里面指定jar包

![创建tomcat-4](E:\Study\study_note\Java\Servlet\tomcat\imgs\创建tomcat-4.png)

![创建tomcat-5](E:\Study\study_note\Java\Servlet\tomcat\imgs\创建tomcat-5.png)

![创建tomcat-6](E:\Study\study_note\Java\Servlet\tomcat\imgs\创建tomcat-6.png)

- 完成以上步骤之后,HttpServlet就能找到,可以自动完成导入jar包

- 然后在MyServlet中完成业务逻辑

```java
package com.shanlei;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class MyServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 给浏览器返回一个h1标签
        resp.getWriter().write("<h1>first tomcat page</h1>");
    }
}
```

3. 配置web映射关系

- 在web.xml文件中配置映射关系

```java
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <servlet>
        <!-- 配置servlet的别名,可以是任意名称 -->
        <servlet-name>MyServlet</servlet-name>
        <!-- 配置servlet类的完全限定名  包名+类名 指定servlet类 -->
        <servlet-class>com.shanlei.MyServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <!-- 配置servlet跟请求的映射关系,servlet-name指定servlet名,url-pattern指定请求的地址 -->
        <servlet-name>MyServlet</servlet-name>
        <url-pattern>/first</url-pattern>
    </servlet-mapping>
</web-app>
```

4. 启动tomcat服务

- 在IDEA中启动tomcat服务,需要在RUN中配置

![启动tomcat-1](E:\Study\study_note\Java\Servlet\tomcat\imgs\启动tomcat-1.png)

![启动tomcat-2](E:\Study\study_note\Java\Servlet\tomcat\imgs\启动tomcat-2.png)

![启动tomcat-3](E:\Study\study_note\Java\Servlet\tomcat\imgs\启动tomcat-3.png)

![启动tomcat-4](E:\Study\study_note\Java\Servlet\tomcat\imgs\启动tomcat-4.png)

![启动tomcat-5](E:\Study\study_note\Java\Servlet\tomcat\imgs\启动tomcat-5.png)

![启动tomcat-6](E:\Study\study_note\Java\Servlet\tomcat\imgs\启动tomcat-6.png)