# Java-IO流-BufferedReader与BufferedWriter

- BufferedReader 缓冲输入字符流
- BufferedWriter 缓冲输出字符流
- 上面两种流都是输出处理流，都需要嵌套其他流进行使用；
- 缓冲流实现了减少硬盘访问次数，底层实际上是有两个缓冲区
  - 在读取数据的时候，一次先将文件内容都读入缓冲区内，然后，程序再去缓冲区中读取
  - 在输出数据的时候，先将所有的数据都写入到缓冲区中，然后，程序再一次性将数据写入到文件中

- 底层原理参照[Java-IO流-BufferedInputStream与BufferedOutputStream](https://www.cnblogs.com/shanlei/p/14278148.html)

- 示例

```java
public class Test04 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws IOException {
        //缓冲字符流实现文本文件复制
        // 源文件
        File f1 = new File("E:\\Study\\java_train_code\\JavaSE基础\\test.txt");
        // 目标文件
        File f2 = new File("E:\\Study\\java_train_code\\JavaSE基础\\demo.txt");
        // 输入字符流
        FileReader fr = new FileReader(f1);
        // 输出字符流
        FileWriter fw = new FileWriter(f2);
        // 缓冲输入字符流
        BufferedReader br = new BufferedReader(fr);
        // 缓冲输出字符流
        BufferedWriter bw = new BufferedWriter(fw);
        // 执行操作
        int len = 0;
        char[] ch = new char[20];
        while((len = br.read(ch))!=-1){
            bw.write(ch,0,len);
        }

        // 关闭流
        br.close();
        bw.close();
    }
}
```



