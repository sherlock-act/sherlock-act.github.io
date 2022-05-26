# Java-面向对象-多态

- 多态与属性无关，多态指的是方法的多态
- 多态就是同一个方法，传入不同的对象（子类）可以有不同的表现
- 多态的好处
  - 提高代码的扩展性，符合面向对象的设计原则：开闭原则
  - 开闭原则：扩展是开放的，修改是关闭的
- 多态的要素
  - 继承：要有子类继承自父类
  - 重写：子类要对父类的方法进行重写
  - 父类引用指向子类对象

```java
public class Girl {
    public void play(Animal an){
        an.shout();
    }
}
```

```java
// 父类
public class Animal {
    public void shout(){
        System.out.println("小动物开始的叫了起来");
    }
}
```

```java
// 子类
public class Cat extends Animal{
    public void shout(){
        System.out.println("喵喵喵");
    }
    public void eat(){
        System.out.println("小猫爱吃鱼");
    }
}
```

```java
// 子类
public class Dog extends Animal {
    public void shout(){
        System.out.println("汪汪汪");
    }
}
```

```java
public class Test {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        Girl g = new Girl();
        Cat c = new Cat();
        Dog d = new Dog();

        // 在代码中，让猫与狗继承自动物类
        //在创建动物对象的时候，让动物对象等于实际的狗或者猫的对象，然后给女孩对象传递动物作为实参
        // 这样在女孩的play方法就不用多次重载，只用写成父类动物类就可以了
        Animal an = c;

        g.play(an);
    }
}

// 运行结果
/*
喵喵喵
*/
```

## 向下转型，向上转型

```java
 // 向下转型，父类类型转为子类类型
Pig pig = (Pig)an;
    
// 向上转性，子类类型转为父类类型
Animal an = p;
```

