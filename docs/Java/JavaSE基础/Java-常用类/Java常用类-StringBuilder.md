# Java常用类-StringBuilder

- StringBuilder类创建的对象其实是可变的字符串
- StringBuilder的实例对象在调用append方法的时候，会对传入字符串的长度与当前剩余空位置的长度进行比较，如果char类型数组的长度不够存放的话，底层就会对数组进行扩容
- StringBuilder的append方法会return this，所以可以实现链式调用

```java
public class Test01 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        /*StringBuilder底层有两个重要的属性
        一个是char类型的数组，用来存储字符
        一个是int类型的count，用来对数组中被使用的长度进行计数
         */

        StringBuilder sb1 = new StringBuilder(); // 表面上是在调用空构造器，其实底层是对char类型数组进行初始化，并且默认长度为16

        StringBuilder sb2 = new StringBuilder(3); // 表面上是调用有参构造器，传入一个int类型的数，其实底层是对char类型的数组进行初始化，长度为传入的int类型的数

        StringBuilder sb3 = new StringBuilder("abc");

        sb3 = sb3.append("def").append("ghjk").append("uiowersdf").append("aaaaaa"); // 因为StringBuilder的append方法会return this 所以可以像前面这样进行链式调用
        // StringBuilder底层在执行append方法的时候，会对传入字符串的长度与当前剩余空位置的长度进行比较，如果char类型数组的长度不够存放的话，底层就会对数组进行扩容
        System.out.println(sb3);
    }
}
```

- 常用方法

```java
public class Test02 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        // StringBuilder的常用方法
        StringBuilder sb = new StringBuilder();
        // 增加
        sb.append("StringBuilder的增加方法");
        System.out.println(sb);

        // 删除
        sb.delete(0,14); // 删除[3,5)位置上的字符
        System.out.println(sb);

        // 改-插入
        sb.insert(2,"的");// 在下表为3的地方插入字符串
        System.out.println(sb);

        // 改--替换
        sb.replace(0,2,"练习"); //将[0,2)下表位置的字符替换为"练习"
        System.out.println(sb);
        sb.setCharAt(2,'得'); // 将指定下标的字符进行替换，只能传入单个字符
        System.out.println(sb);

        // 查
        for (int i = 0; i < sb.length(); i++) {
            System.out.println(sb.charAt(i));
        }

        // 截取
        String str = sb.substring(3,5);//截取[3,5)返回的是一个新的String，对StringBuilder没有影响
        System.out.println(str);
    }
}
```

