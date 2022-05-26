# Java-IO流-BufferedInputStream与BufferedOutputStream

- BufferedIputStream 缓冲输入字节流
- BufferedOutputStream 缓冲输出字节流
- 上面两种流都是输出处理流，都需要嵌套其他流进行使用；
- 缓冲流实现了减少硬盘访问次数，底层实际上是有两个缓冲区
  - 在读取数据的时候，一次先将文件内容都读入缓冲区内，然后，程序再去缓冲区中读取
  - 在输出数据的时候，先将所有的数据都写入到缓冲区中，然后，程序再一次性将数据写入到文件中
- 原理图如下：

![Buffered](E:\Study\study_note\Java\JavaSE基础\Images\Buffered.png)

- 示例

```java
public class Test01 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws IOException {
        // 利用缓冲字节流，减少访问硬盘次数
        // 源文件对象
        File f1 = new File("E:\\Study\\java_train_code\\JavaSE基础\\CHICO.jpg");
        // 目标文件对象
        File f2 = new File("E:\\Study\\java_train_code\\JavaSE基础\\CHICO_copy.jpg");
        // 读取文件字节流
        FileInputStream fis = new FileInputStream(f1);
        // 输出文件字节流
        FileOutputStream fos = new FileOutputStream(f2);
        // 输入缓冲字节流
        BufferedInputStream bis = new BufferedInputStream(fis);
        // 输出缓冲字节流
        BufferedOutputStream bos = new BufferedOutputStream(fos);
        // 执行复制操作
        int len = 0;
        byte[] b = new byte[1024];
        while((len = bis.read(b))!=-1){
            bos.write(b,0,len);
        }
        // 关闭流 关闭流的时候只用关闭高级流，就能同时将套这的另一个流同时关闭
        bis.close();
        bos.close();
    }
}
```

