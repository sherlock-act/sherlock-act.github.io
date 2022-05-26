# Tomcat的Request对象的常用方法

- Requset对象可以通过对象获取`请求行`,`请求头`,`请求体`中的所有信息

```java
package com.shanlei;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.Enumeration;

/**
 * @author: shanlei
 * @version: 1.0
 */

/**
 * HttpServletRequest 用来存放客户端请求的参数
 * 请求行
 * 请求头
 * 请求体
 */
public class RequestServlet extends HttpServlet {

    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("Post请求");
        this.doGet(request, response);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("get请求");
        // 获取请求行数据
        // 获取请求中的请求方式
        System.out.println(request.getMethod());
        // 获取请求的完整地址
        StringBuffer requestURL = request.getRequestURL();
        System.out.println(requestURL);
        System.out.println(request.getRequestURI());
        // 获取请求中的协议
        System.out.println(request.getScheme());

        // 获取请求头数据
        // 获取User-Agent
        System.out.println(request.getHeader("User-Agent"));
        // 获取请求头信息中的所有key的枚举对象
        Enumeration<String> headerNames = request.getHeaderNames();
        while (headerNames.hasMoreElements()){
            // System.out.println(headerNames.nextElement());
            String key = headerNames.nextElement();
            String value = request.getHeader(key);
            System.out.println(key+":"+value);
        }

        // 获取用户请求体  用户请求数据
        // 无论请求方式是post还是get,获取用户数据的方式不变
        String user = request.getParameter("user");
        String pwd = request.getParameter("pwd");
        System.out.println("user:"+user);
        System.out.println("password:"+pwd);

        Enumeration<String> parameterNames = request.getParameterNames();
        while(parameterNames.hasMoreElements()){
            String key = parameterNames.nextElement();
            String value = request.getParameter(key);
            System.out.println(key+":"+value);
        }

        // 获取相同key的多个数据值,例如checkbox
        String[] favs = request.getParameterValues("fav");
        for (String fav : favs) {
            System.out.println(fav);
        }

        // 其他常用方法
        // 获取客户端地址
        String remoteAddr = request.getRemoteAddr();
        // 获取客户端主机名称
        String remoteHost = request.getRemoteHost();
        // 获取客户端端口号
        int remotePort = request.getRemotePort();

        // 获取本地主机信息
        String localAddr = request.getLocalAddr();
        String localName = request.getLocalName();
        int localPort = request.getLocalPort();
    }
}

```

