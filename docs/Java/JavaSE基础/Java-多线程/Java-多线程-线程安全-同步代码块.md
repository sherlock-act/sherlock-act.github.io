# Java-多线程-线程安全-同步代码块

- 在多个线程都在争抢公共资源的时候，可能会出现抢到公共资源后，还没有完成所有操作就被其他线程抢走了，这可能导致程序运行结果不符合我们的意愿的情况
- 例如示例所示，在没有加同步代码块的时候，可能出现买到重复的票或者买到第0、-1张票的情况
- 为了解决线程安全的问题，可以在可能出现线程危险的地方加上同步代码块，就是使用`synchronized(this){}`将可能出现问题的代码包裹住
- 但是在使用的时候也要注意，在使用同步代码块的时候，不要多包了代码，不然影响代码的执行效率
- 示例：

```java
public class BuyTicketThread implements Runnable{
    private int ticketNum = 10;
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            synchronized (this) {
                // 加上了同步代码块之后，相当于在各个争抢公共资源的时候，一个线程抢到了，那么其他线程至少要等这个线程完成一次代码块中的语句，才能继续争抢资源
                // 相当于抢到资源后就加了一把锁，不让其他线程抢公共资源了
                if (ticketNum > 0) {
                    System.out.println("我在" + Thread.currentThread().getName() + "买到了西藏到成都的第" + ticketNum-- + "张机票");
                }
            }
        }
    }
}
```

