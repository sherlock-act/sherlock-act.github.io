# Java--代码块

- 类的组成：属性、方法、构造器、代码块、内部类

- 代码块的分类：普通块、构造块、静态块、同步块（多线程学习，后续更新）

- 代码块的执行顺序

  - 静态块-->构造块-->构造器-->方法中的普通块

  - 静态块只在第一次加载类的时候运行一次

  - 静态块多用于创建工厂，数据库的初始化信息都放入静态块。一般用于执行一些全局性的初始化操作。

  - 构造块，在每次创建对象的时候，都会先与构造器执行

  - ```java
    package com.shanlei7;
    
    /**
     * @Auther: shanlei
     * @Date: 2020/12/4 - 12 - 04 - 12:42
     * @Description: com.shanlei7
     * @version: 1.0
     */
    public class Demo {
        int a;
        static int sa;
        public void method01(){
            System.out.println("----method01----");
            // 普通块限制了局部变量的作用范围
            int num = 10;
            System.out.println("这是普通块");
            System.out.println(num);
        }
    
        public static void method02(){
            System.out.println("--这是静态方法--");
        }
    
        // 构造块  类中方法外
        {
            System.out.println("-----这是构造块-----");
        }
    
        // 静态块
        static{
            System.out.println("--这是静态块--");
            //静态块中只能调用静态方法与静态属性
            System.out.println(sa);
            method02();
        }
    
        // 构造器
        public Demo(){
    
        }
    
        // 这是main方法，是实现程序主要逻辑
        public static void main(String[] args) {
            Demo d1 = new Demo();
            d1.method01();
    
            Demo d2 = new Demo();
            d2.method02();
        }
    
    }
    
    ```

  - 执行结果

  - ```java
    --这是静态块--
    0
    --这是静态方法--
    -----这是构造块-----
    ----method01----
    这是普通块
    10
    -----这是构造块-----
    ----method01----
    这是普通块
    10
    
    Process finished with exit code 0
    ```

  - 