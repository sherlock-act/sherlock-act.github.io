# Java常用类-Random

- 随机数Random类中有两个构造器，一个有参构造器，一个无参构造器
  - 有参构造器需要传入一个long类型的数字，用有参构造器创建的对象，会根据传入的long类型的数字不同生成不同的随机数，但是如果传入的long类型的数字相同的话，生成的随机数也相同
  - 无参构造器，表面是在调用无参数构造器，实际底层还是调用了带参构造器
- Random类的常用方法
  - nextInt 这个方法会返回一个整数，如果不传参数的话，返回的是int表数范围内的一个随机整数，如果传入一个正整数的话，就会返回一个0至这个正整数之前的随机数
  - nextDouble 这个方法会返回一个[0.0, 1.0)质检的随机小数

```java
public class Test02 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        System.out.println("随机数"+Math.random());

        // Random
        // 带参数的构造器创建的对象
        // 带参数的构造器需要传一个L类型的数字
        Random r1 = new Random(System.currentTimeMillis());
        System.out.println(r1.nextInt());

        //利用空参构造器创建对象
        Random r2 = new Random();
        // nextInt 带参数，就会返回0至这个数之间的一个随机数
        System.out.println(r2.nextInt(50));
        // nextDouble 返回一个[0.0, 1.0)之间的随机数
        System.out.println(r2.nextDouble());
    }
}
```

