# Java-JDBC-事务与回滚

* 事务能够保证SQL要么全部执行成功,要么全部执行失败
* JDBC 默认是自动提交事务
   * 每条DML都是默认提交事务的,多个preparedStatement.executeUpdate();都会提交一次事务
* 如果想手动控制事务,那么就不能让事务自动提交
* 通过Connection对象控制connection.setAutoCommit(false)不自动提交事务;
* 如果不设置 默认值为true,自动提交,设置为false之后就是手动提交了
* 无论是否发生回滚,事务最终会一定要提交的 提交我们建议放在finally之中进行提交
* 如果是转账的过程中出现异常了,那么我们就要执行回滚,回滚操作应该方法catch语句块中

## 事务示例

```java
package com.shanlei.test05;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class TestTransaction {
    private static String url = "jdbc:mysql://localhost/mytestdb?useSSL=false&useUnicode=true&charcterEncoding=UTF-8&serverTimezone=Asia/Shanghai&useServerPrepStmts=true&cachePrepStmts=true&rewriteBatchedStatements=true";
    private  static String user = "root";
    private static String password ="123456";
    private static String driver = "com.mysql.cj.jdbc.Driver";
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        testTransaction();

    }
    public static void testTransaction(){
        /*
        使用AddBatch实现批处理
         */
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        /*
         * JDBC 默认是自动提交事务
         * 每条DML都是默认提交事务的,多个preparedStatement.executeUpdate();都会提交一次事务
         * 如果想手动控制事务,那么就不能让事务自动提交
         * 通过Connection对象控制connection.setAutoCommit(false);
         * 如果不设置 默认值为true,自动提交,设置为false之后就是手动提交了
         * 无论是否发生回滚,事务最终会一定要提交的 提交我们建议放在finally之中进行提交
         * 如果是转账的过程中出现异常了,那么我们就要执行回滚,回滚操作应该方法catch语句块中
          */
        try {
            //注册驱动
            Class.forName(driver);

            // 获取连接
            connection = DriverManager.getConnection(url, user, password);
            // connection控制不自动提交
            connection.setAutoCommit(false);

            // 准备SQL并添加到队列中
            String sql = "update account set balance = balance -? where id = ?;";
            preparedStatement = connection.prepareStatement(sql);
            // 转出
            preparedStatement.setDouble(1,100);
            preparedStatement.setDouble(2,1);
            preparedStatement.executeUpdate();
            // 转入
            preparedStatement.setDouble(1,-100);
            preparedStatement.setDouble(2,2);
            preparedStatement.executeUpdate();

        } catch (ClassNotFoundException | SQLException e) {
            // 语句执行异常,在catch中进行回滚事务
            if(null != connection){
                try {
                    connection.rollback();
                } catch (SQLException ex) {
                    ex.printStackTrace();
                }
            }

            e.printStackTrace();
        } finally {
            // 在关闭资源之前进行提交,无论是否执行回滚,都需要进行提交,所以将提交放在finally里面
            if(null != connection){
                try {
                    connection.commit();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }

            if(null!=preparedStatement){
                try {
                    preparedStatement.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if(null!=preparedStatement){
                try {
                    connection.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

## 回滚点

- 在进行大批量操作的时候,可能由于最后几条数据有问题导致出现异常,直接回滚会导致前面的大量数据丢失
- JDBC中可以设置回滚点,指定回滚操作需要回滚到哪个回滚点
- 这样可以保证即使程序出现异常,也有部分数据能够被正常保存下来,减少数据丢失
- 使用`connection.setSavepoint()`方法获取回滚点
- 在回滚的时候`connection.rollback(sp);`方法中传入回滚点可以设置回滚到哪个回滚点

```java
package com.shanlei.test05;

import java.sql.*;
import java.util.LinkedList;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class TestTransaction2 {
    private static String url = "jdbc:mysql://localhost/mytestdb?useSSL=false&useUnicode=true&charcterEncoding=UTF-8&serverTimezone=Asia/Shanghai&useServerPrepStmts=true&cachePrepStmts=true&rewriteBatchedStatements=true";
    private  static String user = "root";
    private static String password ="123456";
    private static String driver = "com.mysql.cj.jdbc.Driver";
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        testAddBatch();

    }
    public static void testAddBatch(){
        /*
        设置回滚点,实现大批量操作的时候,就算出错也能保证部分数据成功执行
         */
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        // 定义一个savePrint 的LinkedList,用来存放每一个回滚点
        LinkedList<Savepoint> linkedList = new LinkedList<>();

        try {
            //注册驱动
            Class.forName(driver);
            // 获取连接
            connection = DriverManager.getConnection(url, user, password);
            // 准备SQL并添加到队列中
            String sql = "insert into dept values (default,?,?)";
            preparedStatement = connection.prepareStatement(sql);
            for (int i = 0; i < 100856; i++) {
                preparedStatement.setString(1,"成都分部");
                preparedStatement.setString(2,"chengdu");
                preparedStatement.addBatch();  // 每循环一次就将一句sql语句放入批次中
                if(i%1000 == 0) {// 每当在批次中设置了1000条数据后,就开始执行一次并设置回滚点
                    // 执行SQL,设置回滚点
                    preparedStatement.executeBatch();//执行批处理中的语句
                    preparedStatement.clearBatch();// 清理批处理中的数据
                    linkedList.add(connection.setSavepoint()); // 设置回滚点,并将回滚点放到集合中
                }
            }
        } catch (ClassNotFoundException | SQLException e) {
            // 语句执行异常,在catch中进行回滚事务
            if(null != connection){
                try {
                    // 获取最后回滚点,用于指定到具体回滚点
                    Savepoint sp = linkedList.getLast();
                    if(null != sp){ // 如果指定的回滚点不等于null,那么久回滚到回滚点,否则就全部回滚
                        connection.rollback(sp);
                    }else{
                        connection.rollback();
                    }
                } catch (SQLException ex) {
                    ex.printStackTrace();
                }
            }
            e.printStackTrace();
        } finally {
            // 在关闭资源之前进行提交,无论是否执行回滚,都需要进行提交,所以将提交放在finally里面
            if(null != connection){
                try {
                    connection.commit();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if(null!=preparedStatement){
                try {
                    preparedStatement.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if(null!=preparedStatement){
                try {
                    connection.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}


```

