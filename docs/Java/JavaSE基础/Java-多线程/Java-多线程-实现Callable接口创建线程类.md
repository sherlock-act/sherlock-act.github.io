# Java-多线程-实现Callable接口创建线程类

- 不论是继承自`Thread`类创建的线程，还是实现`Runnable`接口创建的线程，都必须重写`run`方法，但是`run`方法有两个缺点
  - 不能有返回值
  - 不能抛出异常
- 所以JDK1.5之后，又有了实现Callable接口创建线程对象的方法
  - 实现`Callable`接口，可以不带泛型，如果不带泛型，那么call方法的返回值就是Object类型
  - 如果带了泛型，那么`call`的返回值就是泛型对应的类型
  - 从`call`方法看，方法有返回值，可以抛出异常
  - 要创建线程比较麻烦
    - 要先创建线程类对象
    - 然后将这个对象作为参数传给`FutureTask`类创建对象
    - 最后才能使用`FutureTask`类对象才能创建`Thread`对象，才能启动线程
  - 接收返回值的时候，需要使用`FutureTask`类的对象的`get`方法才能接收到；

- 示例

```java
public class RandomNum implements Callable<Integer> {
    /*
    1、实现Callable接口，可以不带泛型，如果不带泛型，那么call方法的返回值就是Object类型
    2、如果带了泛型，那么call的返回值就是泛型对应的类型
    3、从call方法看，方法有返回值，可以抛出异常
     */
    @Override
    public Integer call() throws Exception {
        // 返回10以内的随机数
        return new Random().nextInt(10);
    }
}

class Test{
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        // 创建线程对象
        RandomNum rdn = new RandomNum();
        // 想要创建Thread启动线程还必须创建FutureTask对象
        FutureTask ft = new FutureTask(rdn);
        // 然后才能使用FutureTask对象才能创建Thread对象
        Thread t = new Thread(ft);

        // 启动线程
        t.start();

        // 获取线程返回值, 必须要使用FutureTask对象才能获取到
        System.out.println(ft.get());
    }
}
```

