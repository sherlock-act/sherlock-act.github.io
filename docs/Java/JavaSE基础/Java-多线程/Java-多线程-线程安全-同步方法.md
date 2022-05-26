# Java-多线程-线程安全-同步方法

- 在多个线程都在争抢公共资源的时候，可能会出现抢到公共资源后，还没有完成所有操作就被其他线程抢走了，这可能导致程序运行结果不符合我们的意愿的情况
- 为了解决线程安全的问题，可以在可能出现线程危险的地方整体提取为一个方法，然后使用`synchronized`修饰该方法，这样这个方法就变成了同步方法，可以解决线程安全问题
- 但是在使用的时候也要注意，在使用同步代码块的时候，不要多包了代码，不然影响代码的执行效率
- 示例：

```java
public class BuyTicketThread extends Thread {
    // 使用构造器给线程命名
    public BuyTicketThread(String name) {
        super(name);
    }
    // 一共还有10张机票，使用static修饰的变量才能保障，各子线程之间共用该变量
    private static int ticketNum = 10;

    // 线程主要逻辑，实现各窗口之间抢票
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
                a();
        }
    }
    public static synchronized void a(){ // 加上static保证锁是同一把锁
        if (ticketNum > 0) {
            System.out.println("我在" + Thread.currentThread().getName() + "买到了从西藏到成都的第" + ticketNum-- + "张机票");
        }
    }
}
class Test01 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        // 创建三个线程对象
        BuyTicketThread t1 = new BuyTicketThread("窗口1");
        BuyTicketThread t2 = new BuyTicketThread("窗口2");
        BuyTicketThread t3 = new BuyTicketThread("窗口3");
        // 启动线程
        t1.start();
        t2.start();
        t3.start();
    }
}
```

