# Tomcat中Response对象的常用方法

- Response对象可以设置服务端返回给客户端的`响应头`,`响应行`,`响应体`的所有内容

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
 * response表示服务端返回数据的响应对象
 *  响应头:
 *  响应行:
 *  响应体:
 */
public class ResponseServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("this is post");
        this.doGet(request, response);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("this is get");
        // 按照k=v键值对的方式设置响应头, 存在相同的key,value会被覆盖
        response.setHeader("head", "info");
        // 按照k=v键值对的方式设置响应头,存在相同的key,value不会被覆盖
        response.addHeader("city", "chengdu");

        // 设置响应状态码
        // response.sendError(404,"not found page");

        // 设置content-type 服务端返回的对象数据要按照一定的格式要求进行渲染 以下两种方式都可以,只有设置为text/html才能作为网页进行渲染
        response.setHeader("Content-Type", "text/html");
        // response.setContentType("text/html");

        // 给客户端返回数据
        response.getWriter().write("<h1>study hard</h1>");
    }
}

```

