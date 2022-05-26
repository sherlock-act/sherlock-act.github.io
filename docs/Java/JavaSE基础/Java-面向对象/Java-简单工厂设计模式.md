# Java-简单工厂设计模式

- 在java中，不仅可以使用父类作为方法的形参，也可以使用父类作为返回值类型，真实返回的对象可以是该类的任意一个子类对象
- 简单工厂设计模式的作用：大量创建对象的一种解决方案
- 将创建与使用分开，工厂负责创建，使用者直接调用就可以了
- 简单工厂模式的基本要求
  - 定义一个`static`方法，通过类名直接调用
  - 返回值必须是父类类型，返回的可以是任意子类对象
  - 传入创建子类的参数，工厂根据参数创建子类产品

```java
public class Test {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {

        Animal an = PetStore.getAnimal("狗");
        g.play(an);
    }
}
```

```java
public class PetStore {
    // 宠物店类
    // 提供动物
    public static Animal getAnimal(String petName){
        Animal an = null;
        if("猫".equals(petName)){
            an = new Cat();
        }else if("狗".equals(petName)){
            an = new Dog();
        }else if("猪".equals(petName)){
            an = new Dog();
        }

        return an;
    }
}
```

