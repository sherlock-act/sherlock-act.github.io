# Java的构造器

## 构造器的作用

- 构造器的作用是对对象的属性进行赋值，而不是创建对象，因为在程序调用构造器的时候，对象已经被创建了

## 构造器的格式

```java
[修饰符] 构造器的名字(){
    
}
```

- 构造器中没有任何形参的构造器叫做空构造器

- 虽然构造器的作用是给对象的属性进行赋值，但是一般在空构造器中不会对属性进行赋值，因为那样就将每个对象的属性都写死了；

## 构造器与方法的区别

- 构造器没有方法的返回值类型
- 方法体内部不能有`return`语句
- 构造器的名字很特殊，必须跟类型一样

## 构造器的重载

- 在类中一般保证空构造器的存在，并且空构造器中不会进行属性的赋值操作
- 一般我们会重载构造器（类似方法的重载），在重载的构造器中进行属性赋值操作
- 构造器的重载可以定义多个，可以根据使用需求分别对应1个参数、2个参数、3个参数的构造器重载
- 在类中定义了构造器后，程序执行的时候就不会再分配空构造器了，要是此时类中没有空构造器的话，在不穿参数new 对象的话就会报错
- 当形参名字和属性名字重名的时候，会出现就近原则：
  对象的属性前加上this.来修饰 ，因为this代表的就是你创建的那个对象



```java
package com.objtest2;

/**
 * @Auther: shanlei
 * @Date: 2020/12/2 - 12 - 02 - 0:21
 * @Description: com.objtest2
 * @version: 1.0
 */
public class Person {
    // 定义成员变量
    String name;
    int age;
    double height;
    double weight;

    // 定义空构造器
    public Person(){

    }
    // 构造器的重载
    public Person(String name,int age, double height,double weight){
        this.name = name;
        this.age = age;
        this.height = height;
        this.weight = weight;

    }

    // 吃的方法
    public void eat(){
        System.out.println("我喜欢吃东西");
    }

    // 睡觉的方法
    public void sleep(){
        System.out.println("晚上要睡觉");
    }
}

```

