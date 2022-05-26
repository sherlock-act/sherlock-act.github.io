# Java-JDBC-PreparedStatement进行CURD

- PreparedStatement 预编译语句对象可以方式SQL注入攻击,可以稍微提高SQL执行效率
- 直接上代码PreparedStatement进行CURD

```java
package com.shanlei.test03;

import com.shanlei.entity.Emp;

import javax.swing.text.html.HTMLDocument;
import java.sql.*;
import java.util.ArrayList;
import java.util.List;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class TestCURD {
    private static String url = "jdbc:mysql://localhost/mytestdb?useSSL=false&usrUnicode=true&characterEncoding=UTF-8&serverTimezone=Asia/Shanghai";
                                // "jdbc:mysql://localhost/mytestdb?useSSL=false&usrUnicode=true&characterEncoding=UTF-8&serverTimezone=Asia/Shanghai"
    private static String user = "root";
    private static String password = "123456";
    private static String driver = "com.mysql.cj.jdbc.Driver";

    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        // prepareStatement实现CURD
        // testAdd();
        // testUpdate();
        // testDelete();
        testQuery();
    }

    // 增加
    public static void testAdd(){
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        try {
            // 注册驱动
            Class.forName(driver);
            // 获取连接
            connection = DriverManager.getConnection(url, user, password);
            // 准备SQL,获取preparedStatement对象
            String sql = "insert into emp values (default,?,?,?,?,?,?,?);";
            preparedStatement = connection.prepareStatement(sql);
            // 设置参数
            preparedStatement.setString(1,"john");
            preparedStatement.setString(2,"MANAGER");
            preparedStatement.setInt(3,7839);
            preparedStatement.setDate(4,new Date(System.currentTimeMillis()));
            preparedStatement.setDouble(5,3000.45);
            preparedStatement.setDouble(6,0);
            preparedStatement.setInt(7,30);
            // 发送SQL进行操作
            int result = preparedStatement.executeUpdate();
            System.out.println("成功插入"+result+"条数据!");

        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // 关闭资源
            if(null != preparedStatement){
                try {
                    preparedStatement.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
           if(null != connection){

           }try {
                connection.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

    // 修改
    public static void testUpdate(){
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        try {
            // 加载驱动
            Class.forName(driver);
            // 获取连接
            connection = DriverManager.getConnection(url, user, password);
            // 准备SQL,获取preparedstatement对象
            String sql = "update emp set ename=?, job=? where empno=?";
            preparedStatement = connection.prepareStatement(sql);
            // 设置参数
            preparedStatement.setString(1,"holmes");
            preparedStatement.setString(2,"ANALYST");
            preparedStatement.setInt(3,7935);
            // 发送语句执行
            int result = preparedStatement.executeUpdate();
            System.out.println("完成修改"+ result +"行数据");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // 关闭资源
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
    }

    // 删除
    public static void testDelete(){
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        try {
            // 加载驱动
            Class.forName(driver);
            // 获取连接
            connection = DriverManager.getConnection(url, user, password);
            // 准备sql,获取preparedstatement对象
            String sql = "delete from emp where empno=?;";
            preparedStatement = connection.prepareStatement(sql);
            // 设置参数
            preparedStatement.setInt(1, 7935);
            // 发送语句执行
            int result = preparedStatement.executeUpdate();
            System.out.println("成功删除"+ result +"条数据");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // 关闭资源
            if(null!=preparedStatement){
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
    }

    // 查询
    public static void testQuery(){
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        List<Emp> list = null;

        try {
            // 注册驱动
            Class.forName(driver);
            // 获取连接
            connection = DriverManager.getConnection(url, user, password);
            // 准备sql 获取preparedstatement对象
            String sql = "select * from emp where ename like ?;";
            preparedStatement = connection.prepareStatement(sql);
            // 设置参数
            preparedStatement.setString(1,"%A%");
            // 发送sql获取返回resultSet
            ResultSet resultSet = preparedStatement.executeQuery();

            // 遍历resultSet
            list = new ArrayList<Emp>();
            while (resultSet.next()){
                int empno = resultSet.getInt("empno");
                String ename = resultSet.getString("ename");
                String job = resultSet.getString("job");
                int mgr = resultSet.getInt("mgr");
                Date hiredate = resultSet.getDate("hiredate");
                double sal = resultSet.getDouble("sal");
                double comm = resultSet.getDouble("comm");
                int deptno = resultSet.getInt("deptno");
                list.add(new Emp(empno, ename, job, mgr, hiredate, sal, comm, deptno));
            }

        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            // 关闭资源
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
        for (Emp emp : list) {
            System.out.println(emp);
        }
    }
}

```

