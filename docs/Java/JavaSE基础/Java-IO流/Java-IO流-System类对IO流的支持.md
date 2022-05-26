# Java-IO流-System类对IO流的支持

- System类对IO流的支持
- System.in\System.out
  - System.in------>从键盘获取输入
    - Syste.in的read方法会导致程序阻塞，等待键盘录入
  - System.out------>将内容输出到控制台

- 示例：

```java
public class Test01 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws IOException {
        // System类对IO流的支持
        // System.in\System.out
        // System.in------>从键盘获取输入
        InputStream in = System.in;
        int n = in.read(); // in.read()会阻塞程序，等待键盘录入
        System.out.println(n);

        // 所以使用Scanner(System.in)扫描器扫描键盘录入信息的时候，实际上接收键盘输入的是System.in
        // Scanner只是一个扫描器，当然Scanner也能扫描其他流输入的数据
        File f = new File("E:\\Study\\java_train_code\\JavaSE基础\\test.txt");
        FileReader fr = new FileReader(f);
        Scanner sc = new Scanner(fr);
        while(sc.hasNext()){
            System.out.print(sc.next());
        }
        System.out.println();

        // System.out------>将内容输出到控制台
        PrintStream out = System.out;
        out.println("你好Java");
        out.print("你好Python，");
        out.println("你好C++");
        // 实际上，上面的代码就是平常使用的System.out.print()与System.out.println();
        System.out.println("你好Java");
        System.out.print("你好Python，");
        System.out.println("你好C++");
    }
}
```

