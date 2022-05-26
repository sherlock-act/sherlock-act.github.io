# Java枚举类

- 创建自定义枚举类

```java
public class Season {
    // 属性
    private final String seasonName;
    private final String seasonDesc;

    // 构造器私有化，外接不能调用这个构造器
    private Season(String seasonName, String seasonDesc) {
        this.seasonName = seasonName;
        this.seasonDesc = seasonDesc;
    }

    public static Season SPRING = new Season("春天","春暖花开");
    public static Season SUMMER = new Season("夏天","烈日炎炎");
    public static Season AUTUMN = new Season("秋天","硕果累累");
    public static Season WINTER = new Season("冬天","冰天雪地");

    public String getSeasonName() {
        return seasonName;
    }

    public String getSeasonDesc() {
        return seasonDesc;
    }

    @Override
    public String toString() {
        return "Season{" +
                "seasonName='" + seasonName + '\'' +
                ", seasonDesc='" + seasonDesc + '\'' +
                '}';
    }
}
```

- 在java中，可以使用enum关键字直接创建枚举类，比使用自定义创建枚举类更加方便

```java
public enum Season {
    // 使用enum创建枚举类，创建对象（常量）必须放在代码块最开始的位置
    // 多个对象之间用逗号隔开；
    SPRING("春天","春暖花开"),
    SUMMER("夏天","烈日炎炎"),
    AUTUMN("秋天","硕果累累"),
    WINTER("冬天","冰天雪地");

    // 属性
    private final String seasonName;
    private final String seasonDesc;

    // 构造器私有化，外接不能调用这个构造器
    private Season(String seasonName, String seasonDesc) {
        this.seasonName = seasonName;
        this.seasonDesc = seasonDesc;
    }

    public String getSeasonName() {
        return seasonName;
    }

    public String getSeasonDesc() {
        return seasonDesc;
    }
}
```

- 一般在使用枚举类的时候，都不回添加属性与get方法等，直接就写对象名就可以了

```java
public enum Season {
    // 如果枚举类没有属性和get方法等，就可以直接如下面一样，只写常量名就可以了
    // 多个对象之间用逗号隔开；
    SPRING,
    SUMMER,
    AUTUMN,
    WINTER;
}
```

- 枚举类如果实现了接口后，可以在每一个常量后面重新不同的抽象方法，实现不同的逻辑

```java
public enum Season implements TestInterface{
    // 如果枚举类没有属性和get方法等，就可以直接如下面一样，只写常量名就可以了
    // 多个对象之间用逗号隔开；
    // 枚举类实现接口后，可以将接口的抽象方法在常量后面的{}代码块中重写，达到每个对象重写的方法实现不同逻辑
    SPRING{
        @Override
        public void show() {
            System.out.println("春天来了····");
        }
    },
    SUMMER{
        @Override
        public void show() {
            System.out.println("夏天来了····");
        }
    },
    AUTUMN{
        @Override
        public void show() {
            System.out.println("秋天来了····");
        }
    },
    WINTER{
        @Override
        public void show() {
            System.out.println("冬天来了····");
        }
    };
}
```

- 实际应用1，限制输入

```java
// 创建枚举类，限制gender
public enum Gender {
    boy,
    girl;
}
```

```java
public class Person {
    private int age;// 姓名
    private String name;// 年龄
    private Gender gender;// 性别

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
    
    public Gender getGender() {
        return gender;
    }

    public void setGender(Gender gender) {
        this.gender = gender;
    }


    @Override
    public String toString() {
        return "Person{" +
                "age=" + age +
                ", name='" + name + '\'' +
                ", gender='" + gender + '\'' +
                '}';
    }
}
```

```java
public class Student {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        Person s1 = new Person();
        s1.setAge(18);
        s1.setName("nana");
        s1.setGender(Gender.girl);// 使用枚举类，限制了输入的性别
        System.out.println(s1);
    }
}
```

- 实际应用2，配合switch

```java
public class Test {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        Gender boy = Gender.boy;

        switch(boy){
            case boy:
                System.out.println("男孩");
                break;
            case girl:
                System.out.println("女孩");
                break;
        }
    }
}
```

