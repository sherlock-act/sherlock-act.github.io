# servlet请求转发

- 在servlet中设置请求转发
  - `request.getRequestDispatcher("XXXX").forward(request, response);`
- servlet请求转发的特点
  - 客户端只发送一次请求
  - 浏览器的地址栏地址没有变化
  - 请求过程中只有一个request和response对象
  - 几个servlet共享一个request和response对象
  - 对客户端透明，客户端不需要知道服务端进行了哪些操作
- servlet请求转发示意图

![servlet请求转发](E:\Study\study_note\Java\Servlet\tomcat\imgs\servlet请求转发.png)