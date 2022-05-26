# tomcat项目中各种乱码问题的处理方式

## request中处理乱码的方式

- get请求处理乱码的方式
  - 获取字符串之后使用new String(name.getBytes("iso-8859-1"), "utf-8")
  - 使用request.setCharacterEncoding("utf-8")设置请求的编码格式 并且在tomcat配置文件server.xml设置端口的配置项中添加 useBodyEncodingForURI="true"
  - 在tomcat配置文件server.xml设置端口的配置项中添加 URIEncoding="utf-8"
- post请求处理乱码的方式
  - request.setCharacterEncoding("utf-8");

## response中处理乱码的方式

- response.setCharacterEncoding("utf-8");或者设置为gbk

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

/**
 * 处理乱码问题的方式
 * 1、get请求
 *      1、获取字符串之后使用new String(name.getBytes("iso-8859-1"), "utf-8")
 *      2、使用request.setCharacterEncoding("utf-8")设置请求的编码格式 并且在tomcat配置文件server.xml设置端口的配置项中添加 useBodyEncodingForURI="true"
 *      3、在tomcat配置文件server.xml设置端口的配置项中添加 URIEncoding="utf-8"
 * 2、post请求
 *      1、request.setCharacterEncoding("utf-8");
 *
 * 3、response响应编码
 *      1、response.setCharacterEncoding("utf-8");或者设置为gbk
 */
public class CharsetServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        System.out.println("post:"+request.getParameter("name"));
        response.setCharacterEncoding("gbk");
        response.getWriter().write("欢迎");
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 设置请求的编码格式 并且在tomcat配置文件设置端口的配置项中添加 useBodyEncodingForURI="true"
        // request.setCharacterEncoding("utf-8");
        String name = request.getParameter("name");
        // 获取字符串之后使用new String(name.getBytes("iso-8859-1"), "utf-8")
        // System.out.println(new String(name.getBytes("iso-8859-1"), "utf-8"));
        System.out.println("get:"+name);
    }
}

```

