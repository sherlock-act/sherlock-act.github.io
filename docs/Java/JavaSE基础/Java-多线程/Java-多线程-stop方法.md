# Java-多线程-stop方法

- 见名知意，stop方法就是直接停止掉当前线程的方法
- 示例

```java
public class Test01 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        for (int i = 1; i <=100; i++) {
            // 使用stop方法，使线程在满足某个条件的时候直接结束掉
            if( i == 7){
                Thread.currentThread().stop(); // stop方法是一个过期|废弃方法，不建议使用
            }
            System.out.println(i);
        }
    }
}
```

