# Java-多线程-继承Thread类创建线程

- 在Java中，创建子线程的一种方式就是让一个类继承`Thread`类
- 一个类在继承自`Thread`之后，还必须要重写`run`方法，实现的业务逻辑必须写在`run`方法中才能创建子线程
- 创建的子线程对象不能直接调用`run`方法，直接调用`run`方法，实际上是将`run`方法当做普通方法来执行
- 要启动子线程必须使用`子线程名.start()`的方式进行启动
- 示例：
  - 首先创建一个类，继承自`Thread`类

```java
public class TestThread extends Thread{// 继承了Thread类之后，才具备争抢资源的能力
    // 这个线程要执行的任务要放在run方法
    // 但是这个方法，必须是重写Thread类中的run方法，线程的逻辑要写在run方法中
    @Override
    public void run() {
        for (int i = 1; i < 11; i++) {
            System.out.println(this.getName()+i);
        }
    }
}
```

  - 然后，在`main`方法中创建线程对象，并启动线程
```java
public class Test {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {//主线程也要输出10个数
        // 制造其他线程，跟主线程争抢资源
        TestThread td = new TestThread();// 具体的线程对象
        // td.run(); // run方法不能直接被调用，调用了就会被当做一个普通的方法
        // 线程要起作用必须要启动县城
        td.start();

        for (int i = 1; i < 11; i++) {
            System.out.println("main----"+i);
        }

    }
}
```