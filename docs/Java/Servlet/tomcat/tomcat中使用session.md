# Tomcat中使用session

- 解决相同用户发送不同请求时的数据共享问题

## cookie的特点

- 服务器端存储共享数据的技术
- session需要以来cookie技术
- 每个用户对应一个独立的session对象
- 每个session对象的有效时长默认30分钟
- 每次关闭浏览器的时候，重新请求都会开启一个新的session对象，因为返回的JSESSIONID是临时cookie

## cookie的使用

- `HttpSession session = request.getSession();`
- 修改session回话的保持时间  `session.setMaxInactiveInterval(600);`
- 设置session强制失效  `session.invalidate();`
- 设置session属性值  `session.setAttribute("name", "zhangsan");`
- 读取session属性值  `String name = (String)session.getAttribute("name");`

```java
package com.shanlei;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

/**
 * @author: shanlei
 * @version: 1.0
 */

/**
 * session
 *  作用：解决相同用户发送不同请求时的数据共享问题
 *  特点：
 *      1、服务器端存储共享数据的技术
 *      2、session需要以来cookie技术
 *      3、每个用户对应一个独立的session对象
 *      4、每个session对象的有效时长默认30分钟
 *      5、每次关闭浏览器的时候，重新请求都会开启一个新的session对象，因为返回的JSESSIONID是临时cookie
 *  使用：
 *       HttpSession session = request.getSession();
 *      修改session回话的保持时间  session.setMaxInactiveInterval(600);
 *      设置session强制失效  session.invalidate();
 *      设置session属性值  session.setAttribute("name", "zhangsan");
 *      读取session属性值  String name = (String)session.getAttribute("name");
 */
public class SessionServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 设置编码格式
        request.setCharacterEncoding("utf-8");
        response.setCharacterEncoding("utf-8");
        response.setContentType("text/html:charset=utf-8");

        System.out.println("接收到请求");
        // 获取session对象
        HttpSession session = request.getSession();

        // 设置session回话保持时间 单位s
        session.setMaxInactiveInterval(600);

        // getid方法获取JSESSIONID
        String id = session.getId();
        System.out.println(id);

        // 设置session参数
        session.setAttribute("name", "zhangsan");

        // 获取session参数
        String name = (String)session.getAttribute("name");

        // 设置session强制失效
        // session.invalidate();

        response.getWriter().write("学习session");


    }
}

```







