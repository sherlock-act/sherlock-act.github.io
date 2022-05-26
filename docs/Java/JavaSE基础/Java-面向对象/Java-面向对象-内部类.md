# Java-面向对象-内部类

- 类的组成：属性、方法、构造器、代码块（普通块，构造块，静态块，同步块）、内部类
- 什么是内部类：一个类内部定义的类，叫做内部类
- 内部类的组成：属性、方法、构造器等
- 内部类的修饰符：private、default、protect、public、final、abstract  所有类的修饰符，内部类都可以使用
- 内部类的分类：
  - 成员内部类
    - 成员内部类是定义在外部类的方法（代码块）外的内部类
  - 局部内部类
    - 定义在外部类的方法等中的内部类
    - 局部内部类的位置：方法中、块中、构造器中
- 内部类与外部类属性重名的时候，在内部类中调用外部类的属性，使用外部类名.this.属性名调用

##  成员内部类

  - 成员内部类分为静态内部类与非静态内部类

  - 静态内部类 静态内部类只能访问外部类中被static修饰的内容

  - 创建静态内部类可以直接`外部类名.内部类名 对象名 = new 外部类名.内部类名 `

  - 而创建非静态的内部类的时候，必须现有外部类才能创建

  - ```java
    TestOuter to = new TestOuter();
    TestOuter.D d = to.new D();
    ```

```java
public class TestOuter {
    int age =10;

    class D{ // 成员内部类
        String name;
        int age = 20;

        public void method(){
            // 内部类可以访问外部类的内容
//            System.out.println(age);
//            a();
            // 内部类与外部类属性重名的时候，在内部类中调用外部类的属性，使用外部类名.this.属性名调用
            int age = 30;
            System.out.println(age); // 30
            System.out.println(this.age); // 20
            System.out.println(TestOuter.this.age); // 10
        }
    }

    static class E{ // 静态内部类 静态内部类只能访问外部类中被static修饰的内容
//        System.out.println(age);
//        a();
    }


    public void a(){
        System.out.println("a方法");
        {// 方法中
            System.out.println("这是普通块");
            class B{// 块中的内部类

            }
        }

        // 外部类中要访问内部类的内容，需要先实例化内部类的对象
        D d = new D();
        System.out.println(d.name);
        d.method();

        class A{// 这是方法中的内部类

        }
    }

    {// 类中方法外
        System.out.println("这是构造块");
    }

    static { // 类中方法外，被static修饰
        System.out.println("这是静态块");
    }

    public TestOuter(){
        class C{ // 构造器中的内部类

        }
    }

    public TestOuter(int age) {
        this.age = age;
    }
}

class Demo{
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        //  创建外部类对象
        TestOuter to = new TestOuter();
        to.a();

        // 创建静态内部类对象
        TestOuter.E e = new TestOuter.E();

        // 创建非静态内部类对象
        // 创建非静态内部类的时候，必须要现有外部类
        TestOuter.D d = to.new D();
    }
}
```

## 局部内部类

```java
public class TestOuter {
    int num = 10;
    public void method(){
        class A{// 方法中的局部内部类
            public void a(){
                // num = 20;
                // JDK1.8之后，能够直接在内部类中访问外部类的属性，但是不能修改
                // 1.8之前，想要在内部类中方位外部类的属性，那么那个属性必须是被final修饰
                System.out.println(num);
            }
        }
    }

    // 如果在一个项目中，B类只是用一次的话，就没有必要单独创建一个B类，是用内部类就可以了
    public Comparable method02(){
        class B implements Comparable{
            @Override
            public int compareTo(Object o) {
                return 100;
            }
        }
        return new B();
    }

    // 匿名内部类，不用创建类，直接返回一个实现接口的类的对象
    public Comparable method03(){
        return new Comparable(){
            @Override
            public int compareTo(Object o) {
                return 100;
            }
        };
    }
    
    // 下面这种方法实际上与上面的方法是一样的
    public void test(){
        Comparable com = new Comparable(){
            @Override
            public int compareTo(Object o) {
                return 0;
            }
        };

        com.compareTo("asdf");
    }
}
```

