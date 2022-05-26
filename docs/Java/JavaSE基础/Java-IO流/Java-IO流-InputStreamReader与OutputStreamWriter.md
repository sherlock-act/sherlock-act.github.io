# Java-IO流-InputStreamReader与OutputStreamWriter

- 这两个流都是转换流，可以将字节流转换为字符流
- 转换流属于字符流
- InputSteamReader   将输入字节流------->输入字符流
- OutputStreamWriter  将输出字符流----->输出字节流
- 原理：



- 示例：

```java
public class Test01 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws IOException {
        // 使用转换流复制文本文件
        // 源文件
        File f1 = new File("E:\\Study\\java_train_code\\JavaSE基础\\test.txt");
        // 目标文件
        File f2 = new File("E:\\Study\\java_train_code\\JavaSE基础\\demo.txt");
        // 输入字节流
        FileInputStream fis = new FileInputStream(f1);
        // 输出字节流
        FileOutputStream fos = new FileOutputStream(f2);
        // 输入转换字符流
        InputStreamReader isr = new InputStreamReader(fis);
        // 输出转换字符流
        OutputStreamWriter osw = new OutputStreamWriter(fos);
        // 执行复制操作
        int len = 0;
        char[] ch = new char[20]; // 转换流中，使用缓冲数组需要使用字符类型的数组
        while((len = isr.read(ch))!=-1){
            osw.write(ch,0,len);
        }
        // 关闭流
        isr.close();
        osw.close();
    }
}
```

