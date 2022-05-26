# Java-IO流-对象流操作自定义类对象

- 对象流可以将内存中的对象序列化写入本地文件中，也可以从本地文件中反序列化读取对象到内存中
- 但是，对于自定义类来说，想要实现序列化，必须要实现Serializable接口
- 如果没有实现Serializable接口的类在进行序列化的时候会出`没有序列化异常 NotSerializableException`
- 序列化号（serialVersionUID）：
  - 实现Serializable接口的类，都有一个标识序列化版本标识符的静态常量`serialVersionUID`
  - `private static final log serialVersionUID;`
  - `serialVersionUID`用来表明类的不同版本间的兼容性。简言之，其目的是以序列化对象进行版本控制，有关各版本反序加化时是否兼容
  - 如果类没有显示定义这个静态变量，它的值是Java运行时环境根据类的内部细节自动生成的。若类的实例变量做了修改，serialVersionUID 可能发生变化。故建议，显式声明
  - Java的序列化机制是通过在运行时判断类的serialVersionUID来验证版本一致性的。在进行反序列化时，JVM会把传来的字节流中的serialVersionUID与本地相应实体类的serialVersionUID进行比较，如果相同就认为是一致的，可以进行反序列化，否则就会出现序列化版本不一致的异常。(InvalidCastException)

示例：

- 首先，先准备一个自定义类

```java
public class Person implements java.io.Serializable{
    // 属性
    private int age;
    private String name;
    // 序列号
    private static final long serialVersionUID = 1234567894561263L;
    // set get 方法
    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    // 构造器
    public Person() {
    }

    public Person(int age, String name) {
        this.age = age;
        this.name = name;
    }

    // 重写toString方法

    @Override
    public String toString() {
        return "Person{" +
                "age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}
```

- 然后使用对对象进行序列化与发序列化

```java
public class Test01 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws IOException {
        // 序列化 将内存中的对象写入文件中
        // 创建Person对象
        Person p1 = new Person(19, "lili");
        // 输出对象流
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(new File("E:\\Study\\java_train_code\\JavaSE基础\\demo4.txt")));
        // 输出
        oos.writeObject(p1);
		// 输入对象流
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream(new File("E:\\Study\\java_train_code\\JavaSE基础\\demo4.txt")));

        // 读取到内存中
        Person p1 = (Person)(ois.readObject());
        System.out.println(p1);
        // 关闭流
        ois.close();
        oos.close();
    }
}
```

