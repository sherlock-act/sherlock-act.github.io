# Java-多线程-Lock锁情况下线程通信

- 为了完成Lock锁情况下的线程之间的通信，从JDK1.5开始引入了`Condition`，它用来替代传统的Object的wait()、notify()实现线程间的协作，相比使用Object的wait()、notify()，使用Condition1的await()、signal()这种方式实现线程间协作更加安全和高效。
- `Condition`的优点：
  - 能够更加精细的控制多线程的休眠与唤醒
  - 对于同一个锁，我们可以创建多个Condition，在不同的情况下使用不同的Condition 
  - 一个Condition包含一个等待队列。一个Lock可以产生多个Condition，所以可以有多个等待队列
  - Lock（同步器）拥有一个同步队列和多个等待队列
- `Condition`对应的等待与通知方法：
  - Conditon中的await()对应Object的wait()；
  - Condition中的signal()对应Object的notify()；
  - Condition中的signalAll()对应Object的notifyAll()。
- 示例：

```java
public class Product {
    // 品牌
    private String brand;
    // 名字
    private String name;
    // 使用标识表示是否有产品 false标识没有商品，true表示有商品
    boolean flag = false;
    // 创建锁
    Lock lock = new ReentrantLock();
    // 创建生产者等待池（等待队列）
    Condition produceCondition = lock.newCondition();
    // 创建消费则等待队列
    Condition customeCondition = lock.newCondition();

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

    public void setProduct(String brand, String name){
        lock.lock();
        try {
            if(flag){
                try {
                    // Lock锁中，不用wait方法，而是使用await方法
                    //wait();
                    produceCondition.await();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            this.setBrand(brand);
            this.setName(name);
            System.out.println("生产者生产了" + this.getBrand() + "-----" + this.getName());
            // 生产了产品之后，将flag设置为true，并通知另一个线程
            flag = true;
            // Lock锁中，不再使用notify方法，而是使用signal方法
            //notify();
            customeCondition.signal();
        }catch(Exception e){
            e.printStackTrace();
        }finally {
            lock.unlock();
        }
    }

    public void getProduct(){
        lock.lock();
        try {
            if(!flag){
                try {
                    // Lock锁中，不用wait方法，而是使用await方法
                    //wait();
                    customeCondition.await();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            System.out.println("消费者消费了：" + this.getBrand() + "----" + this.getName());
            // 消费了商品之后，将flag设置为false，并通知另一个线程
            flag = false;
            // Lock锁中，不再使用notify方法，而是使用signal方法
            // notify();
            produceCondition.signal();
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            lock.unlock();
        }
    }
}
```

