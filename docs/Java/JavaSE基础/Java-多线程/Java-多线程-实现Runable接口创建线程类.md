# Java-多线程-实现Runnable接口创建线程类

- 在Java中，创建子线程的一种方式就是让一个类实现Runnable接口
- 一个类在实现了Runnable之后，还必须要重写`run`方法，实现的业务逻辑必须写在`run`方法中才能创建子线程
- 通过实现Runnable接口创建的子线程对象没有`start`方法，想要启动线程，就必须创建`Thread`对象，并将实现了Runnable接口的类的对象，作为参数传过去，`Thread`的对象才能调用`start`方法
- 示例：
  - 先准备一个实现了`Runnable`接口的类

```java
public class TestThread implements Runnable {
    @Override
    public void run() {
        // 输出1-10
        for (int i = 1; i < 11; i++) {
            System.out.println(Thread.currentThread().getName()+"输出了"+i);
        }
    }
}
```
  - 再创建线程与启动线程
```java
public class Test {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        TestThread tt = new TestThread();
        // 实现自Runnable接口的类的对象，没有start方法，需要创建Thread类才能使用start启动线程
        // 传入tt的时候，也可以传入线程名字，对线程进行命名
        Thread t = new Thread(tt,"子线程");
        t.start();

    }
}
```
