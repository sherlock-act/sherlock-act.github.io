# Java-final关键字

- Java中被final中修饰，就代表这个东西不能再被修改，被继承了
- final可以修饰的东西
  - final可以修饰属性
  - final可以修饰方法
  - final可以修饰类

## final修饰属性

- 代码中被final修饰属性，就代表这个属性就变成了字符常量，不能再进行修改

```java
package com.shanlei02;

/**
 * @Auther: shanlei
 * @Date: 2020/12/7 - 12 - 07 - 22:22
 * @Description: com.shanlei02
 * @version: 1.0
 */
public class Test {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        // final修饰基本数据类型
        final int Age = 10;
        // Age = 20; // 被final修饰的属性，就不能修改了，这句代码会报错

        // final 修饰引用数据类型
        final Dog d = new Dog();
        // d = new Dog(); // 被final修饰的引用数据类型，也不能再重新记性修改不
        // 但是可以对对象的属性进行修改
        d.age = 3;
        d.weight = 13.5;

        // final 修饰的引用数据类型，传递给另一个方法后，可以被修改
        // 修改的是方法内的变量，不是被final修饰的那个变量
        final Dog d2 = new Dog();
        a(d2);
        
        // 引用数据类型被传递给另一方法，如果那个方法的形参也被final修饰，那么这个变量也不能再修改了
        b(d2);
    }

    public static void a(Dog d){
        d = new Dog();
    }
    
    public static void b(final Dog d){
        //d = new Dog(); // 形参被final修饰，不能再进行修改
    }
}
```

## final修饰方法

- final修饰的方法，不能被子类重写

```java
package com.shanlei02;

/**
 * @Auther: shanlei
 * @Date: 2020/12/7 - 12 - 07 - 22:44
 * @Description: com.shanlei02
 * @version: 1.0
 */
public class Person {
    final public void sleep(){
        System.out.println("人到了晚上要睡觉");
    }
}

class girl extends Person{
    /*
    public void sleep(){
        System.out.println("晚上上床睡觉");
    }
     */
    // girl继承自Person，Person中被final修饰的方法不能再子类中重写
}

```

## final修饰类

- 被final修饰的类不能被其他类继承

```java
package com.shanlei02;

/**
 * @Auther: shanlei
 * @Date: 2020/12/7 - 12 - 07 - 22:44
 * @Description: com.shanlei02
 * @version: 1.0
 */
final public class Person {
    public void sleep(){
        System.out.println("人到了晚上要睡觉");
    }
}

/* 被final修饰的类，不能被其他类继承
class girl extends Person{
    /*
    public void sleep(){
        System.out.println("晚上上床睡觉");
    }
     */
    // girl继承自Person，Person中被final修饰的方法不能再子类中重写
}
*/
```

