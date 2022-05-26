# Servlet的生命周期

- 一个Servlet的生命周期是从客户端请求这个Servlet的服务开始,一直到tomcat服务关闭为止
- tomcat服务启动的时候,是不会创建Servlet对象的,只有当客户端请求了这个Servlet的服务的时候,才会创建对象

```java
public class Servletlive extends HttpServlet {
    // init方法是在对象被创建的时候会执行的方法
    @Override
    public void init() throws ServletException {
        System.out.println("init-----创建ServletLive对象");
    }

    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.getWriter().write("<h1>servicelife</h1>");
    }

    // destory方法是在对象被清理的时候会执行的方法
    @Override
    public void destroy() {
        System.out.println("destory----对象被清理");
    }
}
```

