# Java-多线程-伴随线程

- `setDaemon`方法可以将子线程设置为主线程的伴随线程
- 意思就是当主线程运行结束之后，不管子线程是否运行完毕，都直接将子线程强制结束掉
- 示例：

```java
public class TestThread implements Runnable{
    @Override
    public void run() {
        for (int i = 1; i <=1000 ; i++) {
            System.out.println(Thread.currentThread()+"输出了："+i);
        }
    }
}
class Test{
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        // 创建线程
        TestThread tt = new TestThread();
        Thread t = new Thread(tt, "Thread-1");
        // 设置伴随线程
        t.setDaemon(true);
        t.start();

        // 主线程循环打印
        for (int i = 1; i <=10; i++) {
            System.out.println(Thread.currentThread()+"输出了："+i);
        }
    }
}
```

- ==注意：==当设置了伴随线程之后，主线程结束的时候，子线程还会=="垂死挣扎"==一下

- 示例代码运行结果如下：

```java
Thread[main,5,main]输出了：1
Thread[Thread-1,5,main]输出了：1
Thread[main,5,main]输出了：2
Thread[Thread-1,5,main]输出了：2
Thread[main,5,main]输出了：3
Thread[Thread-1,5,main]输出了：3
Thread[main,5,main]输出了：4
Thread[Thread-1,5,main]输出了：4
Thread[main,5,main]输出了：5
Thread[Thread-1,5,main]输出了：5
Thread[main,5,main]输出了：6
Thread[Thread-1,5,main]输出了：6
Thread[Thread-1,5,main]输出了：7
Thread[Thread-1,5,main]输出了：8
Thread[Thread-1,5,main]输出了：9
Thread[Thread-1,5,main]输出了：10
Thread[Thread-1,5,main]输出了：11
Thread[Thread-1,5,main]输出了：12
Thread[Thread-1,5,main]输出了：13
Thread[main,5,main]输出了：7
Thread[main,5,main]输出了：8
Thread[Thread-1,5,main]输出了：14
Thread[Thread-1,5,main]输出了：15
Thread[main,5,main]输出了：9
Thread[Thread-1,5,main]输出了：16
Thread[Thread-1,5,main]输出了：17
Thread[main,5,main]输出了：10
Thread[Thread-1,5,main]输出了：18
Thread[Thread-1,5,main]输出了：19
Thread[Thread-1,5,main]输出了：20
Thread[Thread-1,5,main]输出了：21
Thread[Thread-1,5,main]输出了：22
Thread[Thread-1,5,main]输出了：23
Thread[Thread-1,5,main]输出了：24
Thread[Thread-1,5,main]输出了：25
Thread[Thread-1,5,main]输出了：26
Thread[Thread-1,5,main]输出了：27
Thread[Thread-1,5,main]输出了：28
Thread[Thread-1,5,main]输出了：29
Thread[Thread-1,5,main]输出了：30
Thread[Thread-1,5,main]输出了：31
Thread[Thread-1,5,main]输出了：32
Thread[Thread-1,5,main]输出了：33
```

