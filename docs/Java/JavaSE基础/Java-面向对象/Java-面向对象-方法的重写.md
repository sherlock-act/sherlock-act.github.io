# Java-面向对象-方法的重写

- 当子类继承父类后，对父类定义的某些方法不满意的话，就需要对方法进行重写
- 方法重写的注意事项：
  - 方法名必须一样
  - 形参必须一样
  - 返回值：
    - 基础数据类型的返回值，数据类型必须一样
    - 引用数据类型的返回值，父类的返回值必须大于或等于子类
  - 修饰符：
    - 子类的修饰符权限必须大于或等于父类

```java
// 父类
public class Person {
    private Person eat(){
        System.out.println("吃东西");
        return new Person();
    }
}


//子类
public class Student {
    public Student eat(){
        // 引用数据类型的返回值，必须小于等于父类
        // 权限修饰符的权限，必须大于等于父类
        System.out.println("重写的吃方法");
        return new Student();
    }
}
```

