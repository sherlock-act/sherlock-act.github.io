# Tomcat监听器

- Servlet监听器用于监听一些重要事件的发生，监听器对象可以在事情发生前、发生后可以做一些必要的处理
- 通过实现Servlet API提供的Listense接口，可以在监听正在执行的某一个程序，并且根据程序的需求做出适当的响应
- 监听作用域对象的创建和销毁以及属性的相关配置，可以添加一些公共的属性配置，做逻辑判断
- 也可以通过`Log4j`来做日志的记录等等

|    **监听对象**    |                        **监听器接口**                        |                       **监听事件**                        |
| :----------------: | :----------------------------------------------------------: | :-------------------------------------------------------: |
| **ServletContext** | **ServletContextListener**  **ServletContextAttributeListener** | **ServletContextEvent**  **ServletContextAttributeEvent** |
|  **HttpSession**   |  **HttpSessionListener**  **HttpSessionActivationListener**  |                   **HttpSessionEvent**                    |
|  **HttpSession**   | **HttpSessionAttributeListener**  **HttpSessionBindingListener** |                **HttpSessionBindingEvent**                |
| **ServletRequest** | **ServletRequestListener**  **ServletRequestAttributeListener** | **ServletRequestEvent**  **ServletRequestAttributeEvent** |

## ServletRequest监听对象

- 需要是实现的接口与重写方法
  - `servletRequestListener`：监听request对象的创建和销毁
    - `public void requestDestroyed(ServletRequestEvent servletRequestEvent)`  request对象被销毁的时候添加的逻辑代码
    - `public void requestInitialized(ServletRequestEvent servletRequestEvent)`  request对象被初始化的时候添加的逻辑代码
  - `ServletRequestAttributeListener`：监听request作用域属性的添加，删除和修改
    - `public void attributeAdded(ServletRequestAttributeEvent servletRequestAttributeEvent)` :request作用域属性被添加的时候的逻辑代码
    - `public void attributeRemoved(ServletRequestAttributeEvent servletRequestAttributeEvent)` :request作用域属性被删除的时候的逻辑代码
    - `public void attributeReplaced(ServletRequestAttributeEvent servletRequestAttributeEvent)` :request作用域属性被修改的时候的逻辑代码

```java
package com.shanlei.listense;

import javax.servlet.*;
import java.util.Date;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class Mylistense implements ServletRequestListener, ServletRequestAttributeListener {
    @Override
    public void requestDestroyed(ServletRequestEvent servletRequestEvent) {
        System.out.println("request对象被销毁--:"+new Date());
    }

    @Override
    public void requestInitialized(ServletRequestEvent servletRequestEvent) {
        System.out.println("request对象被初始化---:"+new Date());
    }

    @Override
    public void attributeAdded(ServletRequestAttributeEvent servletRequestAttributeEvent) {
        System.out.println("request对象属性被添加---："+new Date());
        System.out.println(servletRequestAttributeEvent.getName());
        System.out.println(servletRequestAttributeEvent.getValue());
    }

    @Override
    public void attributeRemoved(ServletRequestAttributeEvent servletRequestAttributeEvent) {
        System.out.println("request对象属性被删除---："+new Date());
    }

    @Override
    public void attributeReplaced(ServletRequestAttributeEvent servletRequestAttributeEvent) {
        System.out.println("request对象属性被修改---："+new Date());
    }
}
```



## ServletContext监听对象

- 需要是实现的接口与重写方法
  - `ServletContextListener`：监听servletContext对象的创建和销毁
    - `public void contextDestroyed(ServletContextEvent servletContextEvent)`  servletContext对象被销毁的时候添加的逻辑代码
    - `public void contextInitialized(ServletContextEvent servletContextEvent)`  servletContext对象被初始化的时候添加的逻辑代码
  - `ServletContextAttributeListener`：监听servletContext作用域属性的添加，删除和修改
    - `public void attributeAdded(ServletContextAttributeEvent servletContextAttributeEvent)` :servletContext作用域属性被添加的时候的逻辑代码
    - `public void attributeRemoved(ServletContextAttributeEvent servletContextAttributeEvent)` :servletContext作用域属性被删除的时候的逻辑代码
    - `public void attributeReplaced(ServletContextAttributeEvent servletContextAttributeEvent)` :servletContext作用域属性被修改的时候的逻辑代码

```java
package com.shanlei.listense;

import javax.servlet.*;
import java.util.Date;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class Mylistense implements ServletContextListener, ServletContextAttributeListener {
    @Override
    public void attributeAdded(ServletContextAttributeEvent servletContextAttributeEvent) {
        System.out.println("ervletContext对象属性被添加---："+new Date());
        System.out.println(servletContextAttributeEvent.getName());
        System.out.println(servletContextAttributeEvent.getValue());
    }

    @Override
    public void attributeRemoved(ServletContextAttributeEvent servletContextAttributeEvent) {
        System.out.println("servletContext对象属性被删除---："+new Date());
        System.out.println(servletContextAttributeEvent.getName());
        System.out.println(servletContextAttributeEvent.getValue());
    }

    @Override
    public void attributeReplaced(ServletContextAttributeEvent servletContextAttributeEvent) {
        System.out.println("servletContext对象属性被修改---："+new Date());
        System.out.println(servletContextAttributeEvent.getName());
        System.out.println(servletContextAttributeEvent.getValue());
    }

    @Override
    public void contextInitialized(ServletContextEvent servletContextEvent) {
        System.out.println("servletContext对象被初始化--:"+new Date());
    }

    @Override
    public void contextDestroyed(ServletContextEvent servletContextEvent) {
        System.out.println("servletContext对象被销毁--:"+new Date());
    }
}
```

## HttpSession监听对象

- 需要是实现的接口与重写方法
  - `HttpSessionListener`：监听session的创建与销毁
    - `public void sessionCreated(HttpSessionEvent httpSessionEvent)`  session对象被创建的时候添加的逻辑代码
    - `public void sessionDestroyed(HttpSessionEvent httpSessionEvent)`  session对象被销毁的时候添加的逻辑代码
  - `HttpSessionAttributeListener`：监听session的属性的添加、删除与修改
    - `public void attributeAdded(HttpSessionBindingEvent httpSessionBindingEvent)` :session添加属性的时候添加的逻辑代码
    - `public void attributeRemoved(HttpSessionBindingEvent httpSessionBindingEvent)` :session添加属性的时候删除的逻辑代码
    - `public void attributeReplaced(HttpSessionBindingEvent httpSessionBindingEvent)` :session添加属性的时候修改的逻辑代码
- `HttpSessionActivationListenser`是在session被持久化后当被重新读取到内存中的时候使用的监听器，一般不使用
- `HttpSessionBindingListener`绑定监听器，需要另外创建对象才能实现监听，所以也一般不使用

```java
package com.shanlei.listense;

import javax.servlet.http.HttpSessionAttributeListener;
import javax.servlet.http.HttpSessionBindingEvent;
import javax.servlet.http.HttpSessionEvent;
import javax.servlet.http.HttpSessionListener;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class SessionListense implements HttpSessionListener, HttpSessionAttributeListener {
    @Override
    public void sessionCreated(HttpSessionEvent httpSessionEvent) {
        System.out.println("session对象被创建");
    }

    @Override
    public void sessionDestroyed(HttpSessionEvent httpSessionEvent) {
        System.out.println("session对象被销毁");
    }

    @Override
    public void attributeAdded(HttpSessionBindingEvent httpSessionBindingEvent) {
        System.out.println("session添加属性");
        System.out.println(httpSessionBindingEvent.getName());
        System.out.println(httpSessionBindingEvent.getValue());
    }

    @Override
    public void attributeRemoved(HttpSessionBindingEvent httpSessionBindingEvent) {
        System.out.println("session删除属性");
        System.out.println(httpSessionBindingEvent.getName());
        System.out.println(httpSessionBindingEvent.getValue());
    }

    @Override
    public void attributeReplaced(HttpSessionBindingEvent httpSessionBindingEvent) {
        System.out.println("session修改属性");
        System.out.println(httpSessionBindingEvent.getName());
        System.out.println(httpSessionBindingEvent.getValue());
    }
}

```

