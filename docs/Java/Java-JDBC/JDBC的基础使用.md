# JDBC的基础使用

- JDBC是Java执行SQL的API,为多种关系型数据库提供统一访问,由一组用Java语言编写的类和接口组成
- JDBC的主要组成
  - DriverManager类   作用：管理各种不同的JDBC驱动
  - Connection接口
  - Statement接口和PreparedStatement接口      
  - ResultSet接口
- JDBC访问数据的步骤
  - 加载一个Driver驱动
  - 注册Driver驱动
  - 创建数据库连接（Connection）
  - 创建SQL命令发送器Statement
  - 通过Statement发送SQL命令并得到结果
  - 处理结果（select语句）
  - 关闭数据库资源ResultSet  Statement  Connection

- JDBC在获取创建数据库连接的时候需要传入三个参数

  - user:登录数据库用户名

  - password:登录数据库的密码

  - url:统一资源定位符,定位到需要连接的数据库,url中主要有以下数据:

    - 协议	jbdc:mysql

    - IP        127.0.0.1/localhost

    - 端口号 3306

    - 数据库名字  mytestdb

    - 参数  连接mysql数据库需要准备一些特殊参数

      - useSSL = false
      - useUnicode = true
      - characterEncoding = UTF-8
      - serverTimezone = Asia/Shanghai

    - url 的格式:协议://ip:端口/资源路径?参数名=参数值&参数名=参数值&....

    - ```java
      "jdbc:mysql://localhost/mytestdb?useSSL=false&useUnicode=ture&characterEncoding=UTF-8&serverTimezone=Asia/Shanghai"
      ```

- JDBC基础使用代码示例:

```java
package com.shanlei.test01;

import com.mysql.cj.jdbc.Driver;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class Test01 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws SQLException {
        /**
         *向dept表中插入一条数据
         */
        // 1.加载驱动 创建的对象需要是导入的依赖中的driver实现类
        Driver driver = new Driver();

        // 2.注册驱动 DriverManager
        DriverManager.registerDriver(driver);

        //3.获得链接 Connection
        /**
         user:用户名
         * password:密码
         * url:统一资源定位符 定位我们要连接的数据库的
         *   1协议         jdbc:mysql
         *   2IP          127.0.0.1/localhost
         *   3端口号       3306
         *   4数据库名字   mydb
         *   5参数
         *   协议://ip:端口/资源路径?参数名=参数值&参数名=参数值&....
         *   jdbc:mysql://127.0.0.1:3306/mydb
         */
        String url = "jdbc:mysql://localhost/mytestdb?useSSL=false&useUnicode=ture&characterEncoding=UTF-8&serverTimezone=Asia/Shanghai";
        String user = "XXXX", password = "XXXX";
        Connection connection = DriverManager.getConnection(url, user, password);

        // 4.获取语句对象
        Statement statement = connection.createStatement();
        // 5.执行语句
        /**
         *  insert delete update 都是修改语句,在JDBC中都是通过statement.executeUpdate操作修改语句
         *  statement.executeUpdate的返回值是一个int类型的数值,SQL语句影响的数据行数
         */
        String sql = "insert into dept values (50,'LOGISTICS','BEIJING');";
        int rows = statement.executeUpdate(sql);
        System.out.println("语句操作成功,共影响:"+ rows + "行数据");

        // 6.关闭资源
        /**
         * 关闭资源的时候需要后获取先关闭
         * 只用关闭statement与connection
         */
        statement.close();
        connection.close();

    }
}

```

