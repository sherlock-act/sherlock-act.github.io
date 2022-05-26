# Java-面向对象-继承

- 类是对对象的抽象，那么继承就是对类的抽象
- 直白的理解就是将多个类中相同部分提取出来，作为父类，然后让子类继承自父类，那么子类就能继承父类所有的属性与方法；
- 代码中，先写父类，然后再写子类
- 继承的好处
  - 继承的好处就是提高代码的复用性，父类中定义的内容，子类可以直接继承使用；
  - 便于代码的扩展
  - ==注意==：父类`private`修饰的内容，子类实际上也继承，只是因为封装的特性阻碍，不能直接调用，但是提供了间接调用的方式。
- 继承的注意：
  - 父类`private`修饰的内容，子类也会继承过来
  - 父类可以有多个子类
  - 一个子类只能有一个直接父类
  - 没有写`extends`继承的类，实际上都是继承至`Object`类

# 示例

- 父类

```java
package com.shanlei3;

/**
 * @Auther: shanlei
 * @Date: 2020/12/5 - 12 - 05 - 16:51
 * @Description: com.shanlei3
 * @version: 1.0
 */
 // 父类
public class Person {
    private int age;
    private String name;
    private double height;
    private double weight;

    // 构造器
    public Person(){

    }
    public Person(int age, String name, double height, double weight){
        this.age = age;
        this.name = name;
        this.height = height;
        this.weight = weight;
    }

    // setter\getter方法

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getHeight() {
        return height;
    }

    public void setHeight(double height) {
        this.height = height;
    }

    public double getWeight() {
        return weight;
    }

    public void setWeight(double weight) {
        this.weight = weight;
    }

    public void eat(){
        System.out.println("可以吃饭");
    }
    public void sleep(){
        System.out.println("可以睡觉");
    }
}

```

- 子类

```java
package com.shanlei3;

/**
 * @Auther: shanlei
 * @Date: 2020/12/5 - 12 - 05 - 17:02
 * @Description: com.shanlei3
 * @version: 1.0
 */
public class Student extends Person{ // 使用extends表示Student类继承自Person类
    private int sNum;

    // 构造器
    public Student(){

    }
    public Student(int sNum){
        this.sNum = sNum;
    }

    public int getsNum() {
        return sNum;
    }

    public void setsNum(int sNum) {
        this.sNum = sNum;
    }

    public void study(){
        System.out.println("应该坚持学习");
    }
}

```

- 

