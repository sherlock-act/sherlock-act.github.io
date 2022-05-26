# Java-JDBC防止SQL注入攻击

- SQL注入攻击指的是通过构建特殊的输入作为参数传入Web应用程序，而这些输入大都是SQL语法里的一些组合，通过执行SQL语句进而执行攻击者所要的操作，其主要原因是程序没有细致地过滤用户输入的数据，致使非法数据侵入系统。
- 例如
  - 我们在JDBC中写的验证用户登录的方法是直接使用Statement执行的,那么SQL语句就是直接使用字符串拼接的形式`"select * from account where username ='"+username+"' and password ='"+pwd+"'";`
  - 那么这个时候,如果输入的用户名是`qwer`,密码是`qwer'or'a'='a`这样的字符串
  - 然后,这个用户名与密码在与SQL语句完成拼接后就变成了`"select * from account where username ='qwer' and password ='qwer'or'a'='a'";`
  - 这样,SQL的where子句就变成了判断(有没有账号为`qwer`并且密码为`qwer`)或者(a=a)
  - 很显然,`a=a`肯定成立,所以就会直接查询数据表中的所有数据,这样就实现SQL注入获取了数据表中的数据

## 如何防止SQL注入

- 为了防止SQL注入攻击,JDBC中推荐使用预编译语句对象`prepareStatement`执行SQL查询语句
  - `PreparedStatement `可以使用 ? 作为参数的占位符
  - 使用?作为占位符,即使是字符串和日期类型,也不使用单独再添加 ''
  - 如果SQL语句中有?作为参数占位符号,那么要在执行CURD之前先设置参数
  - 通过`set***`(问号的编号,数据) 方法设置参数
  - `prepareStatment`对象在`set***`方法上,会对单引号进行转译处理,也就是说,?中的数据的单引号  ‘  会被转义成 \’,这样就单引号就不会破坏sql语句的结构

- 首先准备一个实体类

```java
package com.shanlei.entity;

import java.io.Serializable;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class Account implements Serializable {
    private int id;
    private String user;
    private String password;
    private double balance;

    @Override
    public String toString() {
        return "Account{" +
                "id=" + id +
                ", user='" + user + '\'' +
                ", password='" + password + '\'' +
                ", balance=" + balance +
                '}';
    }

    public Account() {
    }

    public Account(int id, String user, String password, double balance) {
        this.id = id;
        this.user = user;
        this.password = password;
        this.balance = balance;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getUser() {
        return user;
    }

    public void setUser(String user) {
        this.user = user;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public double getBalance() {
        return balance;
    }

    public void setBalance(double balance) {
        this.balance = balance;
    }
}

```

- JDBC查询代码

```java
package com.shanlei.test02;

import com.shanlei.entity.Account;

import java.sql.*;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class TestInjection {
    private static String url = "jdbc:mysql://localhost/mytestdb?useSSL=false&usrUnicode=true&characterEncoding=UTF-8&serverTimezone=Asia/Shanghai";
    private static String user = "root";
    private static String password = "123456";
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        // 使用扫描器录入用户名密码
        Scanner sc = new Scanner(System.in);
        System.out.print("请输入账号:");
        String userIn = sc.next();
        System.out.print("请输入密码:");
        String passwordIn = sc.next();
        // 调用getAccount验证账号密码
        List<Account> account = getAccount(userIn, passwordIn);
        System.out.println(account.isEmpty()?"登录失败":"登录成功");
        sc.close();

    }
    public static List<Account> getAccount(String userIn, String passwordIn){
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;
        List<Account> accounts = null;
        try {
            // 加载注册驱动
            Class.forName("com.mysql.cj.jdbc.Driver");

            // 获取连接
            connection = DriverManager.getConnection(url, user, password);

            // 获取语句对象
            /*
             * 1使用PreparedStatement语句对象防止注入攻击
             * 2PreparedStatement 可以使用 ? 作为参数的占位符
             * 3使用?作为占位符,即使是字符串和日期类型,也不使用单独再添加 ''
             * 4connection.createStatement();获得的是普通语句对象 Statement
             * 5connection.prepareStatement(sql);可以获得一个预编译语句对象PreparedStatement
             * 6如果SQL语句中有?作为参数占位符号,那么要在执行CURD之前先设置参数
             * 7通过set***(问号的编号,数据) 方法设置参数
             * */
            String sql = "select * from account where user = ? and password = ?";
            preparedStatement = connection.prepareStatement(sql);//这里已经传入SQL语句
            // 设置参数
            preparedStatement.setString(1,userIn);
            preparedStatement.setString(2,passwordIn);

            // 执行语句
            resultSet = preparedStatement.executeQuery();// 这里不需要再传入SQL语句
            accounts = new ArrayList<Account>();
            while(resultSet.next()){
                int id = resultSet.getInt("id");
                String user = resultSet.getString("user");
                String password = resultSet.getString("password");
                double balance = resultSet.getDouble("balance");
                accounts.add(new Account(id, user, password, balance));

            }

        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            //关闭资源
            if(null != resultSet){
                try {
                    resultSet.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if(null != preparedStatement){
                try {
                    preparedStatement.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if(null != connection){
                try {
                    connection.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
        return accounts;
    }
}

```

