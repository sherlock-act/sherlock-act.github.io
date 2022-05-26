# Java-IO流-DataInputStream与DataOutputStream

- 数据流DataInputStream，DataOutputStream
- DataInputStream:将文件中存储的基本数据类型和字符串  写入  内存的变量中
- DataOutputStream:  将内存中的基本数据类型和字符串的变量 写出  文件中
- 只能写入操作基本数据类型与字符串，对象需要使用对象流进行处理
- 读取的数据类型必须与写入的数据类型一致，不然程序会报错
- 示例：

```java
public class Test01 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws IOException {
        // 数据流DataInputStream，DataOutputStream
        // DataInputStream:将文件中存储的基本数据类型和字符串  写入  内存的变量中
        // DataOutputStream:  将内存中的基本数据类型和字符串的变量 写出  文件中
        // 创建DataOutputStream流
        DataOutputStream dos = new DataOutputStream(new FileOutputStream(new File("E:\\Study\\java_train_code\\JavaSE基础\\demo2.txt")));
        // 将数据写入文件中
        dos.writeUTF("你好Java");
        dos.writeBoolean(true);
        dos.writeDouble(9.88);
        dos.writeInt(99);
        //关闭流
        dos.close();
        System.out.println("完成写入操作");

        // 创建DataInputStream流
        DataInputStream dis = new DataInputStream(new FileInputStream(new File("E:\\Study\\java_train_code\\JavaSE基础\\demo2.txt")));
        // 开始读入
        System.out.println(dis.readUTF());
        System.out.println(dis.readBoolean());
        System.out.println(dis.readDouble());
        System.out.println(dis.readInt());

        // 关闭流
        dis.close();
    }
}
```

- 写入的文件如下图，这个数据是给程序识别的，程序员看着就是像乱码一样

![1610639983236](E:\Study\study_note\Java\JavaSE基础\Images\数据流练习.png)