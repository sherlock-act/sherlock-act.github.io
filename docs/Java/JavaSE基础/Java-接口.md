# Java-接口

## 接口的作用

- 定义规则，实现功能，接口定义好规则后，实现类负责实现，与抽象类相似；
- 接口的使用方法
  - 接口使用 `interface`进行声明
  - JDK1.8之前，接口中只有两部分内容
    - 常量，固定修饰符： `public static final`
    - 抽象方法，固定修饰符：`public abstract`
  - JDK1.8之后，新增非抽象方法
    - 被`public default`修饰的非抽象方法
    - 静态方法
      - 静态方法不能进行重写
- 接口的注意事项
  - 类与接口是同一层次的两个不同概念的东西
  - 接口中没有构造器
  - 类与接口之间是实现关系，类实现接口
  - 接口中所有的方法都是抽象方法
  - 一个类实现了某个接口后，必须重写接口类中的所有抽象方法或将类定义为抽象类，不然代码报错
  - java的继承只有单继承：一个类只能直接继承自一个父类，但是java可以使用多实现：同一个类可以实现多个接口
  - 同时使用继承与接口的时候，继承必须写在实现接口之前
  - 接口中定义的`static`修饰的常量可以直接`接口名.常量名调用`

- JDK1.8之前：

```java
public interface TestInterface01 {
    // 常量
    public static final int NUM = 10;
    // 抽象方法
    /*public abstract*/ void a();
    public abstract void b(int num);
    public abstract int c(String name);
}

interface TestInterface02{
    public abstract void e();
    public abstract void f();
}

class Strudent implements TestInterface01, TestInterface02{
    @Override
    public void a() {
        System.out.println("---1");
    }

    @Override
    public void b(int num) {
        System.out.println("----2");
    }

    @Override
    public int c(String name) {
        return 100;
    }

    @Override
    public void e() {

    }

    @Override
    public void f() {

    }
}
class Test{
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        System.out.println(TestInterface01.NUM);
    }
}
```

- JDK1.8之后：

```java
public interface TestInterface02 {
    // 常量
    public static final int NUM = 10;
    // 抽象方法
    public abstract void a();

    public default void b(){
        System.out.println("接口中被public default修饰的方法");
    }

    // 静态方法
    public static void c(){
        System.out.println("接口中的静态方法");
    }
}

class Demo implements TestInterface02{
    @Override
    public void a() {
        System.out.println("重写a方法");
    }

}
class Test2{
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        TestInterface02.c();
    }
}
```

```java
public interface TestInterface {
    // 常量
    public static final int NUM=10;

    // 抽象方法
    public abstract void a();

    // 被public default 修饰的非抽象方法， default修饰符必须有
    public default void b(){
        System.out.println("这是被public default修饰的非抽象类");
    }
}

class Test implements TestInterface{
    @Override
    public void a() {
        System.out.println("实现接口的a方法");
    }

//    @Override
//    public void b() {
//
//    }
    public void c(){
        // 用接口中的b方法
        b(); // 直接使用方法名，可以直接调用非抽象方法
        // super.b(); 使用super.方法会报错

        TestInterface.super.b(); // 使用super调用接口方法，可以使用接口名.super.方法名调用
    }
}
```

