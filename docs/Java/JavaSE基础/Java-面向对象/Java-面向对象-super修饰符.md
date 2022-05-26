# Java-面向对象-super修饰符

- `super`在子类中使用，表明调用父类
- `super`可以修饰属性也可以修饰方法，表示在子类中是调用父类的东西
- 如果子类中的属性与方法名和父类不冲突的时候，可以直接省略不写`super.` 但是当属性与方法名有冲突的时候，不加`super.`其实是就近原则调用子类的，这个时候要调用父类的属性与方法就必须加`super.`进行修饰
- `super`也可以修饰构造器，表明是去调用父类的构造器，格式是`super();`

```java
package com.shanlei05;

/**
 * @Auther: shanlei
 * @Date: 2020/12/5 - 12 - 05 - 22:50
 * @Description: com.shanlei05
 * @version: 1.0
 */
public class Student extends Person{
    int score;


    public Student(){

    }
    public Student(int age, int score){
        super.age = age; // super调用父类的属性
        this.score = score;
    }

    public void study(){
        System.out.println("努力学习");
        super.eat(); // 使用super显式的调用父类的eat方法，可以省略不写
    }
}

```