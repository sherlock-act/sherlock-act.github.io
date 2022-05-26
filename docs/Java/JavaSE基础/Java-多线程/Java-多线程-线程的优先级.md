# Java-多线程-线程的优先级

- 不同的线程之间，可以有不同的优先级
- 但是也不能保证高优先级就百分之百被优先CPU执行
- 只是说高优先级的线程被CPU先执行的几率大
- Java中线程的优先级为1-10
- 线程默认的优先级都是5

```java
    /**
     * The minimum priority that a thread can have.
     */
    public final static int MIN_PRIORITY = 1;

   /**
     * The default priority that is assigned to a thread.
     */
    public final static int NORM_PRIORITY = 5;

    /**
     * The maximum priority that a thread can have.
     */
    public final static int MAX_PRIORITY = 10;
```

- 示例：

```java
public class TestThread implements Runnable{

    @Override
    public void run() {
        for (int i = 1; i < 10; i++) {
            System.out.println(Thread.currentThread().getName()+"输出："+i);
        }
    }
}

class Test {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        // 创建线程对象
        TestThread tt = new TestThread();
        // 创建Thread对象
        Thread t1 = new Thread(tt, "Thread-1-");
        Thread t2 = new Thread(tt, "Thread-2-");
        // 设置线程优先级
        t1.setPriority(10);
        t2.setPriority(1);
        // 启动线程
        t1.start();
        t2.start();
    }
}
```

- 输出结果：

```java
Thread-1-输出：1
Thread-1-输出：2
Thread-2-输出：1
Thread-1-输出：3
Thread-2-输出：2
Thread-1-输出：4
Thread-2-输出：3
Thread-1-输出：5
Thread-1-输出：6
Thread-1-输出：7
Thread-1-输出：8
Thread-1-输出：9
Thread-2-输出：4
Thread-2-输出：5
Thread-2-输出：6
Thread-2-输出：7
Thread-2-输出：8
Thread-2-输出：9
```

