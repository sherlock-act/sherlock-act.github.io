# Java-多线程-join方法

- 在Java中，如果一个线程调用了`join`方法，那么这个线程就会被优先执行，该线程执行结束之后，才执行其他的线程
- ==注意：==必须要调用了`start`方法之后，才能调用`join`方法，不然会出错

- 示例

```java
public class TestThread implements Runnable {
    @Override
    public void run() {
        for (int i = 1; i < 10; i++) {
            System.out.println(Thread.currentThread().getName()+"输出了："+i);
        }
    }
}

class Test{
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws InterruptedException {
        for (int i = 1; i < 40; i++) {
            if(i == 6){
                TestThread tt = new TestThread();
                Thread t = new Thread(tt, "SubThread-1");
                t.start();
                // 调用了join的线程会被优先执行
                t.join();
            }
            System.out.println(Thread.currentThread().getName()+"输出了："+i);
        }
    }
}
```

