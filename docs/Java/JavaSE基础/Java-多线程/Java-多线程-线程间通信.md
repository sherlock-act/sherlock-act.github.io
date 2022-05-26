# Java-多线程-线程间通信

- 在Java对象中，有两个池：锁池与等待池
  - 锁池：Synchronized，
  - 等待池：`wait(),notify(),notifyAll()`
- 一个线程如果调用了某个对象的`wait()`，那么，该线程就立即进入带该对象的等待池中（并且将锁释放掉）
- 在未来的某个时刻，另一个线程调用了同一个对象的`notify()`或者`notifyAll()`方法，那么在等待池中的线程就会被唤起，然后进入到该对象的锁池中去获取该对象的锁
- 当获得锁之后，该线程就会沿着`wait()`方法之后的语句继续执行，==注意，是沿着`wait()`之后的语句执行==
- `wait()与notify()`方法，必须放在同步方法或者同步代码块中才能生效（因为只有在同步的基础上线程通信才是有效的）
- `sleep与wait`的区别
  - sleep进入阻塞状态没有释放锁
  - wait进入阻塞状态但是同时释放了锁
- 示例代码
- 创建商品类

```java
public class Product {
    // 品牌
    private String brand;
    // 名字
    private String name;
    // 使用标识表示是否有产品 false标识没有商品，true表示有商品
    boolean flag = false;

    // set&get方法
    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public synchronized void setProduct(String brand, String name){
        if(flag){
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        this.setBrand(brand);
        this.setName(name);
        System.out.println("生产者生产了" + this.getBrand() + "-----" + this.getName());
        // 生产了产品之后，将flag设置为true，并通知另一个线程
        flag = true;
        notify();
    }

    public synchronized void getProduct(){
        if(!flag){
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("消费者消费了：" + this.getBrand() + "----" + this.getName());
        // 消费了商品之后，将flag设置为false，并通知另一个线程
        flag = false;
        notify();
    }
}

```

  - 创建生产者类
```java
public class ProducerThread implements Runnable {
    // 共享商品
    private Product p;

    public ProducerThread(Product p){
        this.p = p;
    }

    @Override
    public void run() {
        for (int i = 1; i <= 10 ; i++) {
            synchronized (p){
                if(i%2 == 0){
                  p.setProduct("哈尔滨", "啤酒");
                }else{
                    p.setProduct("费列罗", "巧克力");
                }
            }
        }
    }
}
```
  - 创建消费者类
```java
public class CustomerThread implements Runnable {
    // 公共商品
    private Product p;

    public CustomerThread(Product p){
        this.p = p;
    }

    @Override
    public void run() {
        for (int i = 1; i <=10 ; i++) {
            synchronized (p) {
                p.getProduct();
            }
        }
    }
}
```
  - 创建线程，并启动线程
```java
public class Test {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        // 创建线程对象
        Product p = new Product();
        ProducerThread pt = new ProducerThread(p);
        CustomerThread ct = new CustomerThread(p);
        Thread prt = new Thread(pt);
        Thread cut = new Thread(ct);

        // 启动线程
        prt.start();
        cut.start();
    }
}
```
  - 运行结果
```
生产者生产了费列罗-----巧克力
消费者消费了：费列罗----巧克力
生产者生产了哈尔滨-----啤酒
消费者消费了：哈尔滨----啤酒
生产者生产了费列罗-----巧克力
消费者消费了：费列罗----巧克力
生产者生产了哈尔滨-----啤酒
消费者消费了：哈尔滨----啤酒
生产者生产了费列罗-----巧克力
消费者消费了：费列罗----巧克力
生产者生产了哈尔滨-----啤酒
消费者消费了：哈尔滨----啤酒
生产者生产了费列罗-----巧克力
消费者消费了：费列罗----巧克力
生产者生产了哈尔滨-----啤酒
消费者消费了：哈尔滨----啤酒
生产者生产了费列罗-----巧克力
消费者消费了：费列罗----巧克力
生产者生产了哈尔滨-----啤酒
消费者消费了：哈尔滨----啤酒
```
