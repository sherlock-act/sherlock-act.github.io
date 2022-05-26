# Java-多线程-给线程命名

- 在Java中，通过继承Thread创建的线程，有以下两种方式可以给线程命名；
- 通过构造器命名
  - 因为线程类继承自Thread类，所有也继承了Thread的name属性，可以通过super的方法调用父类构造器，将name传给构造器完成线程的命名

```java
public class TestThread extends Thread{// 继承了Thread类之后，才具备争抢资源的能力
    // 给线程命名，弄一个有参的构造器, 调用父类的构造器，将name传过去
    public TestThread(String name) {
        super(name);
    }
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

- 通过set方法进行命名
  - 因为线程类继承自Thread类，所有也继承了Thread的name属性与set和get方法，可以通过调用set方法来完成线程的命名

```java
public class TestThreadName {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        // 方法一，使用构造器给线程命名
        // TestThread t1 = new TestThread("子线程");
        // 方法二：使用set方法，给线程命名
        TestThread t1 = new TestThread();
        t1.setName("子线程");
        t1.start();
    }
}
```