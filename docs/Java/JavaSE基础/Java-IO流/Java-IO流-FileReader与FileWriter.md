# Java-IO流-FileReader与FileWriter

- FileReader，字符输入流，完成文件内容读取
  - FileReader.read()括号中不加任何参数，是单个字符得读取文件内容
  - 可以使用缓冲数组一次读取多个字符，FileReader.read(ch)，ch是char类型的数组
  - FileReader.read()的返回值是int类型，如果返回值为-1的时候表示已经读完了整个文件
- FileWriter，字符输出流，完成向文件内写入数据操作
  - FileWriter.writer()方法可以向文件中写入数据
    - 可以一个字符一个字符的进行输出
    - 可以直接写入一个char类型的数组
    - 也可以直接写入一个字符串
  - 文件的覆盖于追加
    - 文件的覆盖于追加指的是在不同的流之间的操作，在同一个流中进行的输出操作，都是追加
    - new FileWriter(f)   相当于对原文件进行覆盖操作。
    - new FileWriter(f,false)  相当于对源文件进行覆盖操作。不是追加。
    -  new FileWriter(f,true)   对原来的文件进行追加，而不是覆盖。

- 示例：完成文本文件复制

```java
public class Test03 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws IOException {
        // 实现文件的复制
        // 创建源文件对象
        File f1 = new File("E:\\Study\\java_train_code\\JavaSE基础\\TestIO\\test.txt");
        // 创建目标文件对象
        File f2 = new File("E:\\Study\\java_train_code\\JavaSE基础\\TestIO\\demo.txt");
        // 创建FileReader流
        FileReader fr = new FileReader(f1);
        // 创建FileWriter流
        FileWriter fw = new FileWriter(f2);
        // 创建缓冲数组
        char[] ch = new char[5];
        // 创建变量len
        int len = 0;
        // 复制 
        // while((len = fr.read(ch))!=-1){// 返回值len是数组的有效长度
            // 写入数据
            // 方法1，将数组转为字符串，直接写入字符串
            // String str = new String(ch, 0, len);
            // 转为字符串的时候指定从0到len的长度是为了保证不多复制
            // 数组中保留了每一次读取的所有字符，每次读取的时候一次替换，当最后一次读取的时候，有效长度的数组内容被替换为读取数据，但是有效长度后面的字符仍是上一次读取的内容
            // fw.write(str);

            // 方法2 直接写入一个数组
            fw.write(ch,0, len);
        // }
        // 方法3，一个字符一个字符的复制，效率低
        while((len = fr.read()) != -1){// 返回值len是字符的编码，如果返回-1则表示文件读取完了
            fw.write((char)len);
        }
        // 关闭流
        fw.close();
        fr.close();
    }
}
```

