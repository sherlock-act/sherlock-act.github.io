# Java-多线程-线程安全-Lock锁

- JDK1.5后新增新一代的线程同步方式:Lock锁
- 与采用synchronized相比，lock可提供多种锁方案，更灵活
- synchronized是Java中的关键字，这个关键字的识别是靠JVM来识别完成的呀。是虚拟机级别的。
- 但是Lock锁是API级别的，提供了相应的接口和对应的实现类，这个方式更灵活，表现出来的性能优于之前的方式。
- 使用注意:
  - 打开锁就必须记得释放锁，不然其他线程就一直是阻塞状态
  - 建议使用try-catch-finally的方式，保证不管程序中间执行情况，最后一定会把锁释放
- 示例：

```java
public class BuyTicketThread implements Runnable{
    private int ticketNum = 10;
    Lock lock = new ReentrantLock();
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            // 打开锁
            lock.lock();
            try {
                if(ticketNum>0){
                    System.out.println("我在" + Thread.currentThread().getName() + "买到了西藏到成都的第" + ticketNum-- + "张机票");
                }
            }catch (Exception ex){
                ex.printStackTrace();
            }finally {
                // 释放锁
                lock.unlock();
            }
        }
    }
}
class Test {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        // 定义一个线程对象， 可以只创建一个线程对象
        BuyTicketThread btt = new BuyTicketThread();
        // 窗口1
        Thread t1 = new Thread(btt, "窗口1");

        // 窗口2
        Thread t2 = new Thread(btt, "窗口2");

        // 窗口3
        Thread t3 = new Thread(btt, "窗口3");

        // 启动线程
        t1.start();
        t2.start();
        t3.start();

    }
}
```

