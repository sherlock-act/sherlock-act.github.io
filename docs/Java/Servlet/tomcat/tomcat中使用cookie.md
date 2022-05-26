# Tomcat中使用cookie

- cookie是用来处理客户端发送不同请求的时候如何使用相同的参数信息

## cookie的使用

- 创建cookie对象  Cookie cookie = new Cookie("name", name);
- 在response对象中添加cookie  response.addCookie(cookie);
- cookie设置生命周期，单位是秒：cookie.setMaxAge(3*24*3600);
- 给cookie设置固定路径（只有在请求设置的路径才发送响应的cookie）
- 获取cookie对象 Cookie[] cookies = request.getCookies();

## cookie的特点

- cookie是保存在浏览器端的数据名称
- cookie分类：临时cookie（默认存储在内存中，浏览器关闭，cookie失效）、持久化cookie（保存在浏览器中，当时间过期后才失效）
- 每一个cookie对象中保存一个key=value键值对数据，想要存储多个数据，就需要创建多个cookie对象

```java

package com.shanlei;

import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author: shanlei
 * @version: 1.0
 */

/**
 * cookie 用来处理客户端发送不同请求的时候如何使用相同的参数信息
 *  cookie的使用
 *     1、创建cookie对象  Cookie cookie = new Cookie("name", name);
 *     2、在response对象中添加cookie  response.addCookie(cookie);
 *     3、cookie设置生命周期，单位是秒：cookie.setMaxAge(3*24*3600);
 *     4、给cookie设置固定路径（只有在请求设置的路径才发送响应的cookie）
 *     5、获取cookie对象 Cookie[] cookies = request.getCookies();
 *  特点：
 *      1、cookie是保存在浏览器端的数据名称
 *      2、cookie分类：临时cookie（默认存储在内存中，浏览器关闭，cookie失效）、持久化cookie（保存在浏览器中，当时间过期后才失效）
 *      3、每一个cookie对象中保存一个key=value键值对数据，想要存储多个数据，就需要创建多个cookie对象
 *
 */
public class CookieServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("this is post method");
        this.doGet(request, response);

    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setCharacterEncoding("gbk");

        String name = request.getParameter("name");
        String age = request.getParameter("age");

        // 创建Cookie
        Cookie nameCookie = new Cookie("name", name);
        Cookie ageCookie = new Cookie("age", age);
        // 给cookie对象添加时间有效期，单位是s
        nameCookie.setMaxAge(3*24*3600);
        // 给cookie设置固定路径
        ageCookie.setPath("/cookie/age");
        // 将cookie设置到response对象中
        response.addCookie(nameCookie);
        response.addCookie(ageCookie);
        response.getWriter().write("学习cookie");
        
        // 获取cookie对象
        Cookie[] cookies = request.getCookies();
        if(cookies.length>0){
            for (Cookie cookie : cookies) {
                String name = cookie.getName();
                String value = cookie.getValue();
                System.out.println(name+":"+value);
            }
        }
    }
}

```

