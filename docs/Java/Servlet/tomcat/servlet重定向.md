# servlet重定向

- 在servlet中设置重定向
  - `response.sendRedirect("XXXX");`
- servlet请求转发的特点
  - 浏览器发送两次请求
  - 浏览器的地址发生变化
  - 请求过程中产生两个request对象和两个response对象
  - 两个servlet不能共享同一个request对象和response对象
- servlet重定向示意图

![servlet重定向](E:\Study\study_note\Java\Servlet\tomcat\imgs\servlet重定向.png)