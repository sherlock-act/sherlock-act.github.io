# Java-JDBC-查询获取数据库数据

- JDBC对数据库的操作也叫做CURD: 它代表创建（Create）、更新（Update）、读取（Retrieve）和删除（Delete）操作 
- 在JDBC中,使用查询语句获取到的是一个`resultSet`数据集
  - 这个数据集可以想象为一个表格,表头就是`SQL`语句查询的字段,每一行就是查询出来的每一条数据
  - `resultSet`数据集提供了一系列的`get`方法,可以获取数据集中的数据
  - `resultSet`数据集也有一个`next()`方法,这个方法实现的效果如果有下一行,就返回`true`并且游标往下移动一行,如果没有下一行数据,就返回`false`

## 如何使用JDBC完成数据库查询操作

- 在使用JDBC进行查询的时候,一般都先写一个实体类,这个实体类是为了完成将每一行数据封装为一个对象而创建,实体类中的每一个属性都对应`SQL`查询出来的每一个字段(实体类的具体注意事项见代码注释)

```java
package com.shanlei.entity;

import java.io.Serializable;
import java.util.Date;

/**
 * @author: shanlei
 * @version: 1.0
 */
/*
 * 实体类:
 * 和数据库表格名称和字段是一一对应的类
 * 该类的对象主要用处是存储从数据库中查询出来的数据
 * 除此之外,该类没有任何的其他功能
 * 要求
 * 1类名和表名保持一致  (见名知意)
 * 2属性个数和数据库的表的列数保持一致
 * 3属性的数据类型和列的数据类型保持一致
 * 4属性名和数据库表格的列名要保持一致
 * 5所有的属性必须都是私有的 (出于安全考虑)
 * 6实体类的属性推荐写成包装类
 * 7日期类型推荐写成java.util.Date
 * 8所有的属性都要有get和set方法
 * 9必须具备空参构造方法
 * 10实体类应当实现序列化接口 (mybatis缓存  分布式需要 )
 * 11实体类中其他构造方法可选
 * */
public class Emp implements Serializable {
    private int empno;
    private String ename;
    private String job;
    private int mgr;
    private Date hiredate;
    private double sal;
    private double comm;
    private int deptno;

    @Override
    public String toString() {
        return "emp{" +
                "empno=" + empno +
                ", ename='" + ename + '\'' +
                ", job='" + job + '\'' +
                ", mgr=" + mgr +
                ", hiredate=" + hiredate +
                ", sal=" + sal +
                ", comm=" + comm +
                ", deptno=" + deptno +
                '}';
    }

    // 空参构造器
    public Emp() {
    }
	
    // 有参构造器
    public Emp(int empno, String ename, String job, int mgr, Date hiredate, double sal, double comm, int deptno) {
        this.empno = empno;
        this.ename = ename;
        this.job = job;
        this.mgr = mgr;
        this.hiredate = hiredate;
        this.sal = sal;
        this.comm = comm;
        this.deptno = deptno;
    }
	
    // 下面都是set与get方法
    public int getEmpno() {
        return empno;
    }

    public void setEmpno(int empno) {
        this.empno = empno;
    }

    public String getEname() {
        return ename;
    }

    public void setEname(String ename) {
        this.ename = ename;
    }

    public String getJob() {
        return job;
    }

    public void setJob(String job) {
        this.job = job;
    }

    public int getMgr() {
        return mgr;
    }

    public void setMgr(int mgr) {
        this.mgr = mgr;
    }

    public Date getHiredate() {
        return hiredate;
    }

    public void setHiredate(Date hiredate) {
        this.hiredate = hiredate;
    }

    public double getSal() {
        return sal;
    }

    public void setSal(double sal) {
        this.sal = sal;
    }

    public double getComm() {
        return comm;
    }

    public void setComm(double comm) {
        this.comm = comm;
    }

    public int getDeptno() {
        return deptno;
    }

    public void setDeptno(int deptno) {
        this.deptno = deptno;
    }
}

```

- JDBC查询数据库数据代码

```java
package com.shanlei.test01;

import com.shanlei.entity.Emp;

import java.sql.*;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class Test04 {
    private static String driver = "com.mysql.cj.jdbc.Driver";
    private static String url = "jdbc:mysql://localhost/mytestdb?useSSL=false&useUnicode=ture&characterEncoding=UTF-8&serverTimezone=Asia/Shanghai";
    private static String user = "root", password = "123456";
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        List<Emp> emps = testQuery();
        for (Emp emp : emps) {
            System.out.println(emp);
        }
    }
    public static List<Emp> testQuery(){
        Connection connection = null;
        // Statement statement = null; 直接使用Statement执行查询语句可能遭到SQL注入攻击,推荐使用PreparedStatement
        PreparedStatement preparedstatement = null;
        ResultSet resultSet = null;
        List<Emp> emps = null;

        try {
            // 加载注册驱动
            Class.forName(driver);

            //2.获得链接 Connection
            connection = DriverManager.getConnection(url, user, password);

            // 3.准备SQL语句并执行
            /*
             * 1使用PreparedStatement语句对象防止SQL注入攻击
             * 2PreparedStatement 可以使用 ? 作为参数的占位符
             * 3使用?作为占位符,即使是字符串和日期类型,也不使用单独再添加 ''
             * 4connection.createStatement();获得的是普通语句对象 Statement
             * 5connection.prepareStatement(sql);可以获得一个预编译语句对象PreparedStatement
             * 6如果SQL语句中有?作为参数占位符号,那么要在执行CURD之前先设置参数
             * 7通过set***(问号的编号,数据) 方法设置参数
             * */
            String sql = "select * from emp";
            preparedstatement = connection.prepareStatement(sql);
            resultSet = preparedstatement.executeQuery();// 这里不需要再传入SQL语句

            // 如果不怕SQL注入的话也可以直接使用statement.executeQuery(sql)查询语句,代码如下
            /*
            // 3.获取语句对象
            statement = connection.createStatement();
            // 4.执行语句
            
            String sql = "select * from emp";
            resultSet = statement.executeQuery(sql);
             */

            // 4.获取结果并对结果进行遍历封装
            emps = new ArrayList<Emp>();
            while(resultSet.next()){
                int empno = resultSet.getInt("empno");
                String ename = resultSet.getString("ename");
                String job = resultSet.getString("job");
                int mgr = resultSet.getInt("mgr");
                Date hiredate = resultSet.getDate("hiredate");
                double sal = resultSet.getDouble("sal");
                double comm = resultSet.getDouble("comm");
                int deptno = resultSet.getInt("deptno");
                emps.add(new Emp(empno, ename, job, mgr, hiredate, sal ,comm, deptno));
            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }finally{
            // 5.关闭资源
            if(null != resultSet){
                try {
                    resultSet.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if(null != preparedstatement){
                try {
                    preparedstatement.close();
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
        return emps;
    }
}

```



