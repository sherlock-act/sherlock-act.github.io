# Java-IO流-ObjectInputStream与ObjectOutputStream

- 对象流ObjectInputStream，ObjectOutputStream
- ObjectInputStream:将文件中存储的Java对象读到内存中，这个过程也叫做反序列化
- ObjectOutputStream:  将内存中的Java对象写入到本地文件中，这个过程也较多序列化
- 序列化和反序列化
  - 把内存中的Java对象转换成平台无关的二进制数据，从而允许把这种二进制数据持久地保存在磁盘上，或通过网络将这种二进制数据传输到另一个网络节点。----》序列化
  - 用ObjectInputStream类 ： 当其它程序获取了这种二进制数据，就可以恢复成原来的Java对象。----》反序列化
- 示例：

```java
public class Test01 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        // 对象流，将对象写入或读取
        // ObjectInputStream\ObjectOutputStream
        // ObjectOutputStream
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(new File("E:\\Study\\java_train_code\\JavaSE基础\\demo2.txt")));
        // 执行写入
        oos.writeObject("你好");
        // 关闭流
        oos.close();

        // ObjectInputStream
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream(new File("E:\\Study\\java_train_code\\JavaSE基础\\demo2.txt")));
        // 读取
        String str = (String) (ois.readObject());
        System.out.println(str);
        // 关闭流
        ois.close();
    }
}
```
