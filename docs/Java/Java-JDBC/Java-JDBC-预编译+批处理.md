# Java-JDBC-预编译+批处理

- 什么是批处理:批处理就是将一个SQL语句集合发给数据库执行,也就是发送一批SQL给数据库,而不是一条一条得发送给数据库执行,这样可以大大减少访问数据库次数,从而提高SQL执行效率;
- 预编译(`preparedStatement`)+批处理的优点
  - 优点：语句只编译一次，减少编译次数。提高了安全性（阻止了SQL注入）
  - 原理：相似SQL只编译一次，减少编译次数
  - 注意:  需要同时设置开启预编译`useServerPrepStmts=true&cachePrepStmts=true`与批处理`rewriteBatchedStatements=true`

```java
package com.shanlei.test04;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class Test01 {
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
        使用AddBatch实现批处理
         */
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        try {
            //注册驱动
            Class.forName(driver);
            // 获取连接
            connection = DriverManager.getConnection(url, user, password);
            // 准备SQL并添加到队列中
            String sql = "insert into dept values (default,?,?)";
            preparedStatement = connection.prepareStatement(sql);
            for (int i = 0; i < 1000; i++) {
                preparedStatement.setString(1,"成都分部");
                preparedStatement.setString(2,"chengdu");
                preparedStatement.addBatch();  // 每循环一次就将一句sql语句放入批次中
            }
            // 执行SQL
            int[] ints = preparedStatement.executeBatch();//执行批处理中的语句
            /*
             * 整数数组中的元素代表执行的结果代号
             * SUCCESS_NO_INFO -2
             * EXECUTE_FAILED  -3
             * */
            /*int[] ints = */
            preparedStatement.clearBatch();// 清理批处理中的数据

        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        } finally {
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

