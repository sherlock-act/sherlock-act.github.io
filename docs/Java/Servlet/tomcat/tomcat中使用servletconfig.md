# Tomcat中使用ServletConfig

- 方便每一个Servlet获取自己单独的属性配置

## ServletConfig的特点

- 每一个servlet单独拥有一个servletConfig对象

## ServletConfig的使用

- 获取ServletConfig

  - `ServletConfig servletConfig = this.getServletConfig();`

- 读取ServletConfig的属性值

  - `String value = servletConfig.getInitParameter("china");`

- 获取ServletConfig中的所有属性名

  - ```java
    // 获取所有属性名，返回枚举类对象
    Enumeration<String> initParameterNames = servletConfig.getInitParameterNames();
    // 遍历枚举类对象
    while (initParameterNames.hasMoreElements()){
        String key = initParameterNames.nextElement();
        String value2 = servletConfig.getInitParameter(key);
        System.out.println(key+"------"+value2);
    }
    ```

- 练习实例


```java
public class ServletConfigServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 设置编码
        request.setCharacterEncoding("utf-8");
        response.setCharacterEncoding("utf-8");
        response.setContentType("text/html:charset=utf-8");

        // 获取servletConfig对象
        ServletConfig servletConfig = this.getServletConfig();
        String value = servletConfig.getInitParameter("china");
        System.out.println(value);

        // 获取所有的key
        Enumeration<String> initParameterNames = servletConfig.getInitParameterNames();
        while (initParameterNames.hasMoreElements()){
            String key = initParameterNames.nextElement();
            String value2 = servletConfig.getInitParameter(key);
            System.out.println(key+"------"+value2);
        }
    }
}
```







