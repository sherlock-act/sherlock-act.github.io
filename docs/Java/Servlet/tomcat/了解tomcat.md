# 了解tomcat

- tomcat由apache开源组织使用java开发的一款web容器

## tomcat简单原理图

![tomcat基础实现原理](E:\Study\study_note\Java\Servlet\tomcat\imgs\tomcat基础实现原理.png)

## 自定义实现基础tomcat功能

- 定义request类(用来接收客户端发送来的请求)

```java
package com.shanlei;

import java.io.IOException;
import java.io.InputStream;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class MyRequest {

    // 请求方法GET/POST
    private String requestMethod;
    // 请求地址
    private String requestUrl;

    public MyRequest(InputStream inputStream) throws IOException {
        // 缓冲空间
        byte[] buffer = new byte[1024];

        int len = 0;

        // 定义请求的变量
        String str = null;

        if((len = inputStream.read(buffer))>0){
            str = new String(buffer, 0, len);
        }
        String data = str.split("\n")[0];
        String[] params = data.split(" ");
        this.requestMethod = params[0];
        this.requestUrl = params[1];
    }

    public String getRequestMethod() {
        return requestMethod;
    }

    public void setRequestMethod(String requestMethod) {
        this.requestMethod = requestMethod;
    }

    public String getRequestUrl() {
        return requestUrl;
    }

    public void setRequestUrl(String requestUrl) {
        this.requestUrl = requestUrl;
    }
}

```

- 定义response类(用来给客户端返回数据)

```java
package com.shanlei;

import jdk.internal.util.xml.impl.Input;

import javax.swing.text.html.HTML;
import java.io.IOException;
import java.io.OutputStream;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class MyResponse {
    private OutputStream outputStream;

    public MyResponse(OutputStream outputStream) {
        this.outputStream = outputStream;
    }
    public void write(String str) throws IOException {
        StringBuilder builder = new StringBuilder();
        builder.append("HTTP/1.1 200 OK\n")
                .append("Content-Type:text/html\n")
                .append("\r\n")
                .append("<html>")
                .append("<body>")
                .append("<h1>" + str +"</h1>")
                .append("</body>")
                .append("</html>");
        this.outputStream.write(builder.toString().getBytes());
        this.outputStream.flush();
        this.outputStream.close();
    }
}
```

- 定义Mapping类(用来映射请求与applet)

```java
package com.shanlei;

import java.util.HashMap;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class MyMapping {
    public static HashMap<String, String> mapping = new HashMap<>();

    static{
        mapping.put("/mytomcat", "com.shanlei.MyServlet");

    }

    public static HashMap<String, String> getMapping() {
        return mapping;
    }
}
```

- 定义HttpServlet抽象类(定义doGet与doPost与service方法)

```java
package com.shanlei;

/**
 * @author: shanlei
 * @version: 1.0
 */
public abstract class MyHttpServlet {

    // 定义常量
    public static final String METHOD_GET = "GET";
    public static final String METHOD_POST = "POST";

    public abstract void doGet(MyRequest myRequest, MyResponse myResponse) throws Exception;

    public abstract void doPost(MyRequest myRequest, MyResponse myResponse) throws Exception;

    /**
     * 根据请求来判断嗲用哪种处理方法
     * @param myRequest
     * @param myResponse
     */
    public void Service(MyRequest myRequest,MyResponse myResponse) throws Exception{
        if(METHOD_GET.equals(myRequest.getRequestMethod())){
            doGet(myRequest, myResponse);
        }else if(METHOD_POST.equals(myRequest.getRequestMethod())){
            doPost(myRequest, myResponse);
        }
    }
}
```

- 定义Servlet类(继承HttpServlet,进行具体业务逻辑)

```java
package com.shanlei;

import java.io.IOException;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class MyServlet extends MyHttpServlet {
    @Override
    public void doGet(MyRequest myRequest, MyResponse myResponse) throws Exception {
        myResponse.write("myTomcat");
    }

    @Override
    public void doPost(MyRequest myRequest, MyResponse myResponse) throws Exception {
        myResponse.write("POST Tomcat");
    }
}

```

- 定义server类(开启服务)

```java
package com.shanlei;

import org.omg.CORBA.Request;

import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class MyServer {
    /**
     * 定义服务端接收程序,接收Socket请求
     * @param port
     */
    public static void startServer(int port) throws Exception {
        // 定义服务端套接字
        ServerSocket serverSocket = new ServerSocket(port);
        // 定义客户端套接字
        Socket socket = null;

        while(true){
            socket = serverSocket.accept();

            // 获取输入流与输出流
            InputStream inputStream = socket.getInputStream();
            OutputStream outputStream = socket.getOutputStream();

            // 定义请求对象
            MyRequest myRequest = new MyRequest(inputStream);
            // 定义响应对象
            MyResponse myResponse = new MyResponse(outputStream);

            String clazz = new MyMapping().getMapping().get(myRequest.getRequestUrl());
            if(clazz!=null){
                Class<MyServlet> myServletClass = (Class<MyServlet>)Class.forName(clazz);
                // 根据myServlet创建对象
                MyServlet myServlet = myServletClass.newInstance();
                myServlet.Service(myRequest, myResponse);
            }
        }
    }

    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        try {
            startServer(8888);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

