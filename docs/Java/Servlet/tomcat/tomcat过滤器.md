# Tomcat过滤器

- 过滤器是能够对web请求和web响应的头属性和内容体进行操作的一种特殊web组件
- 过滤器的特殊之处在于本身并不直接生成web响应，而是拦截web请求和响应，以便查看、提取或以某种方式操作客户机和服务器之间交换的数据

## 过滤器的功能

- 分析web请求，对输入数据进行预处理
- 阻止web请求和响应的进行
- 根据功能改动请求的头信息和数据体
- 与其他web资源协作

## 过滤器执行原理简图

![过滤器执行原理](E:\Study\study_note\Java\Servlet\tomcat\imgs\过滤器执行原理.png)

## 怎么使用过滤器

1. 定义普通的java类，实现Filter接口
2. 重写方法
   - init：完成初始化功能        tomcat启动的时候执行一次
   - dofilter：进行过滤处理     每次发送请求都会执行
   - destroy：销毁功能          tomcat服务关闭的时候执行
3. 在web.xml文件中配置

```xml
<filter>
    <!-- filter的别名 -->
    <filter-name>filter</filter-name>
    <!-- filter的指定类名 -->
    <filter-class>com.shanlei.filter.MyFilter</filter-class>
</filter>
<filter-mapping>
    <!-- filter的指定别名 -->
    <filter-name>filter</filter-name>
    <!-- 表示要匹配的请求 -->
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

## 过滤器实现登录状态验证与编码格式设置

- 登录状态验证

```java
public class LoginFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("登录过滤器初始化");
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        System.out.println("登录过滤器处理");
        HttpSession session = ((HttpServletRequest)servletRequest).getSession();
        if(session.getAttribute("user")== null){
            ((HttpServletResponse)servletResponse).sendRedirect("login.jsp");
        }else {
            filterChain.doFilter(servletRequest, servletResponse);
        }
        System.out.println("登录过滤器处理完成");
    }

    @Override
    public void destroy() {
        System.out.println("登录过滤器销毁");
    }
}
```

- 编码格式设置

```java
public class EncodingFilter implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("编码过滤器的初始化");
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        System.out.println("编码过滤器的逻辑处理");

        servletRequest.setCharacterEncoding("utf-8");
        servletResponse.setCharacterEncoding("utf-8");
        servletResponse.setContentType("text/html:charset=utf-8");
        filterChain.doFilter(servletRequest, servletResponse);

        System.out.println("编码过滤器执行完成");

    }

    @Override
    public void destroy() {
        System.out.println("编码过滤器被销毁");
    }
}
```

