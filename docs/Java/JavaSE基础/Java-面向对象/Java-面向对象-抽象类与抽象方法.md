# Java-面向对象-抽象类与抽象方法

- 抽象类的作用
  - 在抽象类中，定义抽象方法，目的就是为了给子类定义通用模板，先重写父类的抽象方法，然后扩展自己的内容
  - 抽象类避免子类设计的随意性，子类设计更加严格
- 抽象类与抽象方法的特点
  - 抽象类与抽象方法都需要用`abstract`进行修饰
  - 一个抽象类中可以有0个或者多个抽象方法
  - 但是有抽象方法，就必须是抽象类，不然代码报错
  - 抽象类可以被其他类继承
  - 继承自抽象类的类，必须==定义为抽象类，或者必须重写父类的所有抽象方法==不然代码报错
  - 一般不会把子类定义为抽象类
  - 抽象类不可以创建对象

```java
public abstract class Person {
    // 一个类中，如果有一个方法是抽象方法，那么这个类也要变成一个抽象类
    // 在一个类中，会有一类方法，子类对这个方法非常满意，无需重写
    public void eat(){
        System.out.println("一顿不吃饿得慌");
    }
    // 在一个类中，会有一个方法，子类对这个方法永远不满意，会对方法进行重写
    // 一个方法的方法体去掉，被abstract修饰，那么这个方法就是抽象方法
    public abstract void say();
}
class Strudent extends Person{
    @Override
    public void say() {
        System.out.println("全世界都在说普通话");
    }
}
class Test{
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        // Person p = new Person(); // 抽象类不能被创建对象
    }
}
```

