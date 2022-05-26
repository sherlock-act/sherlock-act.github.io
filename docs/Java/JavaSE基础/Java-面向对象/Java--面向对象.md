# 面向对象

- 面向对象与面向过程
  - 面向过程：完成某个功能中每一步需要怎么完成，具体到事件的步骤与过程
  - 面向对象：完成某个功能的实施者，将功能封装进具体的对象中

- 面向对象的三个阶段
  - 面向对象分析OOA------>Object Oriented Analysis
  - 面向对象设计OOD------>Object Oriented Design
  - 面向对象编程OOP------>Object Oriented Programming

## 创建类

- 类中有方法和属性
  - 属性就是对对象的"名词"描述，比如人的姓名，性格等描述
  - 方法就是对对象的"动词"描述，比如跑，跳，走

- 创建类

  - 属性

    - `[修饰符]  属性类型  属性名 = [默认值] ;`一般不进行默认值赋值

  - 方法

    - ```
      [修饰符]  方法返回值类型  方法名(形参列表) {
              // n条语句
      }
      ```

```java
package com.shanlei;

/**
 * @Auther: shanlei
 * @Date: 2020/12/1 - 12 - 01 - 17:11
 * @Description: com.shanlei
 * @version: 1.0
 * 创建人类
 */
public class Person {
    // 名词-->属性（只把有需要的内容写到代码里，不相关的东西不要放在代码中）
    int age;// 年龄
    String name;// 姓名
    double height; // 身高
    double weight; // 体重

    // 动词-->方法
    // 吃饭的方法
    public void eat(){
        System.out.println("我喜欢吃饭");
    }
    //睡觉的方法
    public void sleep(String address){
        System.out.println("我在"+address+"睡觉");
    }
    // 自我介绍
    public String introduce(){
        return "我的名字是"+name+"，我的年龄是"+age+"岁，身高"+height+"米，体重"+weight+"公斤";
    }
}

```

## 创建对象

- 通过同一个类创建的对象，属性是私有的，方法是公共的；
- 在创建对象的时候，第一次会进行类的加载，再次用这个类创建对象的时候，不会再进行类加载
- 初始化对象的时候，如果没有给对象的属性进行赋值，会自动赋默认值

```java
package com.shanlei;

/**
 * @Auther: shanlei
 * @Date: 2020/12/1 - 12 - 01 - 17:54
 * @Description: com.shanlei
 * @version: 1.0
 */
public class Test {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        // 创建人类对象
        // Person 属于引用数据类型
        Person zs = new Person();
        // 可以对对象的属性进行读取与修改
        // 对对象的属性进行修改赋值
        zs.name = "张三";
        zs.age = 19;
        zs.height = 180.3;
        zs.weight = 62.3;
        
        // 读取输出对象的属性
        System.out.println(zs.name);

        // 调用对象的方法
        zs.sleep("家");
        System.out.println(zs.introduce());
		
        // 通过同一个类创建的对象，属性是私有的，方法是公共的
    }
}

```

## this的应用

- `this`其实就是指的当前创建的对象

- `this`修饰属性

  - 当属性名字与形参或局部变量发生重名的时候，会发生就近原则，访问的都是局部变量，需要指定属性的时候，就需要使用`this`进行修饰

  - `this.属性`

  - ```java
    package com.shanlei2;
    
    /**
     * @Auther: shanlei
     * @Date: 2020/12/4 - 12 - 04 - 11:19
     * @Description: com.shanlei2
     * @version: 1.0
     */
    public class Person {
        int age;
        String name;
        double height;
        double weight;
    
        // 空构造器
        public Person(){
    
        }
        // 有参构造器
        public Person(int age, String name, double height, double weight){
            /*
            age = age;
            name = name;
            height = height;
            weight = weight;
            这样进行赋值就会发生就近原则，实际上进行赋值的使用的都是传入的形参，所以需要使用this进行修饰，保证用的是属性
             */
            this.age = age;
            this.name = name;
            this.height = height;
            this.weight = weight;
        }
    }
    
    ```

- `this`修饰方法

  - 在同一个类中，方法可以互相调用，`this.`可以省略不写

  - ```java
    package com.shanlei3;
    
    import java.sql.SQLOutput;
    
    /**
     * @Auther: shanlei
     * @Date: 2020/12/4 - 12 - 04 - 11:26
     * @Description: com.shanlei3
     * @version: 1.0
     */
    public class Person {
        String name;
        int age;
        double height;
        double weight;
    
        //空构造器
        public Person(){
    
        }
        // 有参构造器
        public Person(String name, int age, double height, double weight){
            this.name = name;
            this.age = age;
            this.height = height;
            this.weight = weight;
        }
    
        public void eat(){
            System.out.println("i like eat meat");
        }
    
        public void play(){
            //System.out.println("i like eat meat");
            // 与eat方法中逻辑相同，可以直接调用eat方法
            eat(); // eat(); 等效于this.eat(); this 指的就是当前的对象
            System.out.println("i like play games");
        }
    }
    
    ```

- `this`修饰构造器

  - 同一个类中，构造器可以互相用`this`调用，==this修饰构造器必须放在第一行==

  - ```java
    	package com.shanlei4;
    
    /**
     * @Auther: shanlei
     * @Date: 2020/12/4 - 12 - 04 - 11:35
     * @Description: com.shanlei4
     * @version: 1.0
     */
    public class Person {
        String name;
        int age;
        double height;
        double weight;
    
        // 空构造器
        public Person(){
    
        }
    
        // 一个参数的构造器
        public Person(String name, int age, double height, double weight){
            this(name, age, height);// this 修饰构造器，实际就是调用三个参数的构造器，必须放在第一行
            this.weight = weight;
        }
    
        // 一个参数的构造器
        public Person(String name, int age, double height){
            this(name, age);// this 修饰构造器，实际就是调用两个参数的构造器，必须放在第一行
            this.height = height;
        }
    
        // 两个参数的构造器
        public Person(String name, int age){
            this(name); // this 修饰构造器，实际就是调用一个参数的构造器，必须放在第一行
            this.age = age;
        }
        // 一个参数的构造器
        public Person(String name){
            this.name = name;
        }
    
        public void eat(){
            System.out.println("i like eat meat");
        }
    }
    
    ```

## static的应用

- `static` 可以修改：属性、方法、代码块、内部类

- 实际上，第一次使用类创建对象的时候，在创建对象之前，会首先在内存的方法区中加载字节码信息，==如果在类中有被`static`修饰的东西的时候，也会在方法区中开辟出静态域，静态域中的东西被整个类创建的所有对象共享==

- `static`修饰属性

  - 在类加载的时候一起加载如方法区中

  - 先于对象存在

  - 访问方式

    - 对象名.属性名
    - 类名.属性名（推荐使用）

  - ```java
    package com.shanlei5;
    
    /**
     * @Auther: shanlei
     * @Date: 2020/12/4 - 12 - 04 - 11:53
     * @Description: com.shanlei5
     * @version: 1.0
     */
    public class Demo {
        int a;
        static int b; // 属性b被static修饰，在静态域中保存，被这个对象创建出来的所有类共享
    
        // 空构造器
        public Demo(){
    
        }
    
        // 这是main方法，是实现程序主要逻辑
        public static void main(String[] args) {
            Demo t1 = new Demo();
            t1.a = 10;
            t1.b = 10;
    
            Demo t2 = new Demo();
            t2.a = 20;
            t2.b = 20;
    
            Demo t3 = new Demo();
            t3.a = 30;
            t3.b = 30;
    
            System.out.println(t1.a); // 输出结果 10
            System.out.println(t2.a); // 输出结果 20
            System.out.println(t3.a); // 输出结果 30
            System.out.println("+--------------------------------------------+");
            System.out.println(t1.b); // 输出结果 30
            System.out.println(t2.b); // 输出结果 30
            System.out.println(t3.b); // 输出结果 30
            
            // 被static修饰的属性可以直接使用类名.属性名来访问
            System.out.println(Demo.b);
        }
    }
    
    ```

- `static`修饰

  - 静态方法中不能直接使用非静态属性

  - 静态方法中不能直接使用非静态方法

  - 静态方法中不能使用this关键字

  - public和static都是修饰符，没有先后区分

  - 静态方法中要调用非静态属性，需要先创建对象，使用对象.属性访问

  - 静态方法可以直接使用 对象.方法、类名.方法调用，比较推荐使用 类名.方法调用

  - 在同一个类中，可以直接调用

  - ```java
    package com.shanlei6;
    
    /**
     * @Auther: shanlei
     * @Date: 2020/12/4 - 12 - 04 - 12:08
     * @Description: com.shanlei6
     * @version: 1.0
     */
    public class Demo {
        int id;
        static int sid;
    
        public Demo(){
    
        }
    
        public void method2(){
            System.out.println("i like eat meat");
        }
    
        // public 和 static 都是修饰符，并没有前后区分
        static public void method1(){
            // System.out.println(this.id); // 报错，静态方法中不能使用this关键字
            // a(); //报错，静态方法中不能直接使用非静态方法
            // System.out.println(id); //报错，静态方法中不能直接使用非静态属性
            System.out.println(sid);
        }
    
        // 这是main方法，是实现程序主要逻辑
        public static void main(String[] args) {
            Demo d = new Demo();
            System.out.println(d.id); // 在静态方法中要调用非静态属性，需要先创建对象，使用对象.属性访问
    
            // 静态方法可以使用对象.方法 调用， 也可以使用类名.方法 调用  在同一个类中，可以直接调用
            Demo.method1();
            d.method1();
            method1();
        }
    }
    
    ```

  - 

