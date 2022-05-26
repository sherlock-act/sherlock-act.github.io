# Java常用类-Math

- Math所属包围java.lang 可以不用导包直接使用
- Math被final修饰，不能有子类继承
- Math的构造器被private修饰，不能被创建对象
- Math所有的方法都被static修饰，可以直接类名+方法名使用
- 常用的方法：

```java
// 静态导入
import static java.lang.Math.*;

public class Test01 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        // 常用属性
        System.out.println(PI);
        // 常用方法
        // 随机数,[0.0, 1.0)
        System.out.println("随机数"+random());

        // 绝对值
        System.out.println("绝对值"+abs(-80));

        // 向上取值
        System.out.println("向上取值"+ceil(9.1));

        // 向下取值
        System.out.println("向下取值"+floor(9.9));

        // 四舍五入
        System.out.println("四舍五入"+round(3.6));

        // 最值
        System.out.println("最大值"+max(3, 6));
        System.out.println("最小值"+min(3, 6));
    }
}
```

