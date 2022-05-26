# Tomcat中使用servletContext

- 运行在JVM上的每一个web应用程序都有一个与之对应的Servlet上下文（Servlet运行环境）
- Servlet API提供ServletContext接口用来标识Servlet上下文，ServletContext对象可以被web应用程序中的所有Servlet访问
- ServletContext对象是web服务器中的一个一直路径的根
- ServletContext用来解决不同用户之间的数据共享

## ServletContext的特点

- 由服务器创建
- 所有用户共享同一个ServletContext对象
- 所有的Servlet都可以访问到同一个ServletContext中的属性
- 每一个web项目对象的是一个ServletContext

## ServletContext的使用

- 获取ServletContext

  - 方式1`ServletContext servletContext = this.getServletContext()`
  - 方式2`ServletContext servletContext1 = this.getServletConfig().getServletContext();`
  - 方式3`ServletContext servletContext2 = request.getSession().getServletContext();`

- servletcontext设置属性值

  - `servletContext.setAttribute("name", "zhangsan");`

- 读取servletcontext的属性值

  - `String name = (String)servletContext.getAttribute("name");`

- 获取web，xml中配置的公共属性

  - ```xml
    <context-param>
    	<param-name>chengdu</param-name>
    	<param-value>beautiful</param-value>
    </context-param>
    <!--  在xml配置中添加公共属性  -->
    ```

  - `String chengdu = servletContext.getInitParameter("chengdu");`

- 获取项目下某个文件的绝对路径

  - `String realPath = servletContext.getRealPath("web.xml");`

- 获取web项目的上下文路径（虚拟目录路径）

  - `String contextPath = servletContext.getContextPath();`

```java
public class ServletContextServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 设置编码
        request.setCharacterEncoding("utf-8");
        response.setCharacterEncoding("utf-8");
        response.setContentType("text/html:charset=utf-8");

        // 获取ServletContext
        // 方式1
        ServletContext servletContext = this.getServletContext();
        // 方式2
        ServletContext servletContext1 = this.getServletConfig().getServletContext();
        // 方式3
        ServletContext servletContext2 = request.getSession().getServletContext();

        // servletcontext设置属性值
        servletContext.setAttribute("name", "zhangsan");

        // 读取servletcontext的属性值
        String name = (String)servletContext.getAttribute("name");

        //  从web和xml中获取参数值
        String chengdu = servletContext.getInitParameter("chengdu");
        System.out.println(chengdu);

        // 获取项目下某个文件的绝对路径
        String realPath = servletContext.getRealPath("web.xml");
        System.out.println(realPath);

        // 获取web项目的上下文路径
        String contextPath = servletContext.getContextPath();
        System.out.println(contextPath);
    }
}
```







