# Java-多线程-sleep方法

- Thread的sleep方法，可以认为得制造线程的阻塞，阻塞的时间就是传入的参数的时长，单位为毫秒

- 示例：

```java
public class Test02 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        // 定义一个时间格式
        DateFormat df = new SimpleDateFormat("HH:mm:ss");
        while (true){
            // 获取当前时间
            Date d = new Date();
            System.out.println(df.format(d));
            try {
                // time.sleep方法，强制让线程阻塞，时间是毫秒单位
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

    }
}
```

