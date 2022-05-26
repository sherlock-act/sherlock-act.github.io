# Java-IO流-FileInputStream与FileOutputStream

- FileInputStream，字节输入流，完成文件内容读取
  - FileInputStreamr.read()括号中不加任何参数，是单个字节得读取文件内容
  - 可以使用缓冲数组一次读取多个字节，FileInputStream.read(b)，b是byte类型的数组
  - FileInputStream.read()的返回值是int类型，如果返回值为-1的时候表示已经读完了整个文件
- FileOutputStream，字节输出流，完成向文件内写入数据操作
  - FileOutputStream.writer()方法可以向文件中写入数据
    - 可以一个字节一个字节的进行输出
    - 可以直接写入一个byte类型的数组
  - 文件的覆盖于追加
    - 文件的覆盖于追加指的是在不同的流之间的操作，在同一个流中进行的输出操作，都是追加
    - new FileOutputStream(f)   相当于对原文件进行覆盖操作。
    - new FileOutputStream(f,false)  相当于对源文件进行覆盖操作。不是追加。
    -  new FileOutputStream(f,true)   对原来的文件进行追加，而不是覆盖。
- ==注意：不要用字节流去操作文本文档==

- 示例：完成非文本文件复制

```java
public class Test02 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws IOException {
        // 字节流实现非文本文档复制
        // 源文件对象
        File f1 = new File("E:\\Study\\java_train_code\\JavaSE基础\\CHICO.jpg");
        // 目标文件对象
        File f2 = new File("E:\\Study\\java_train_code\\JavaSE基础\\CHICO_copy.jpg");
        // 读取文件字节流
        FileInputStream fis = new FileInputStream(f1);
        // 输出文件字节流
        FileOutputStream fos = new FileOutputStream(f2);
        // 复制操作
        // 一个字节一个字节得读取
        /*int n = 0;
        while ((n = fis.read())!=-1){// 如果返回值为-1就表示文件读取完了
            fos.write(n);
        }*/
        // 缓冲数组进行复制
        byte[] b = new byte[1024*8];
        int len = 0;
        while((len = fis.read(b)) != -1){// 如果返回值为-1，就表示文件读取完了
            fos.write(b, 0, len);
        }
        // 关闭流
        fos.close();
        fis.close();
    }
}
```

