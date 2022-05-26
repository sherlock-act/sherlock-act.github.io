# Java-面向对象-封装

- 封装的好处就是==提高代码的安全性==
- 程序的设计追求是“高内聚”与“低耦合“
  - 高内聚：类的内部数据操作细节自己完成，不允许外部干涉
  - 低耦合：仅对外暴露少量的方法用于使用
- 隐藏对象内部的复杂性，只对外公开简单的接口便于调用，提高系统的可扩展性、可维护性
- 通俗的说，就是把改隐藏的隐藏起来，该暴露的暴露出来，这就是封装的设计思想
- 封装的修饰符：`private`、`protected`、`public`、`default`

```java
package com.shanlei02;

/**
 * @Auther: shanlei
 * @Date: 2020/12/4 - 12 - 04 - 18:19
 * @Description: com.shanlei02
 * @version: 1.0
 */
public class Student {
    // 私有化属性
    private String name;
    private int age;
    private String gender;

    // alt+inset  使用快捷键创建getter和setter方法

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getGender() {
        return gender;
    }

    public void setGender(String gender) {
        if("男".equals(gender) || "女".equals(gender)){
            this.gender = gender;
        }else{
            this.gender = "男";
        }
    }

    // 构造器
    public Student(){

    }

    public Student(String name, int age, String gender){
        this.name = name;
        this.age = age;
        this.setGender(gender);
    }
}

```

```java
package com.shanlei02;

/**
 * @Auther: shanlei
 * @Date: 2020/12/4 - 12 - 04 - 18:25
 * @Description: com.shanlei02
 * @version: 1.0
 */
public class Test {

    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        Student s1 = new Student();
        s1.setName("殃奕");
        s1.setAge(18);
        s1.setGender("女");

        System.out.println(s1.getName()+"-------"+s1.getGender()+"------"+s1.getAge());

        Student s2 = new Student("敏敏", 18, "女");
        System.out.println(s2.getName()+"-------"+s2.getGender()+"------"+s2.getAge());
    }
}

```



