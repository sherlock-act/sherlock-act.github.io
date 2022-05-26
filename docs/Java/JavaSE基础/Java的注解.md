# Java的注解

- 注解其实就是代码里的==特殊标记==，这些标记可以在编译,类加载,运行时被读取,并执行相应的处理。==通过使用注解,可以在不改变原有逻辑的情况下，在源文件中嵌入一些补充信息==。代码分析工具、开发工具和部署工具可以通过这些补充信息进行验证或者进行部署。
- 注解的分类
  - 内部没有定义配置参数的注解-->标记
  - 内部定义配置参数的注解-->元数据

## 文档注解

- 文档注解就是==文档注释中使用的注解==，配合javadoc工具生成API中生成特殊信息
- java中的文档注解与使用方法如下：

| **标签**      |                        **描述**                        |                           **示例**                           |
| :------------ | :----------------------------------------------------: | :----------------------------------------------------------: |
| @author       |                    标识一个类的作者                    |                     @author description                      |
| @deprecated   |                 指名一个过期的类或成员                 |                   @deprecated description                    |
| {@docRoot}    |                指明当前文档根目录的路径                |                        Directory Path                        |
| @exception    |                  标志一个类抛出的异常                  |            @exception exception-name explanation             |
| {@inheritDoc} |                  从直接父类继承的注释                  |      Inherits a comment from the immediate surperclass.      |
| {@link}       |               插入一个到另一个主题的链接               |                      {@link name text}                       |
| {@linkplain}  |  插入一个到另一个主题的链接，但是该链接显示纯文本字体  |          Inserts an in-line link to another topic.           |
| @param        |                   说明一个方法的参数                   |              @param parameter-name explanation               |
| @return       |                     说明返回值类型                     |                     @return explanation                      |
| @see          |               指定一个到另一个主题的链接               |                         @see anchor                          |
| @serial       |                   说明一个序列化属性                   |                     @serial description                      |
| @serialData   | 说明通过writeObject( ) 和 writeExternal( )方法写的数据 |                   @serialData description                    |
| @serialField  |             说明一个ObjectStreamField组件              |              @serialField name type description              |
| @since        |               标记当引入一个特定的变化时               |                        @since release                        |
| @throws       |                 和 @exception标签一样.                 | The @throws tag has the same meaning as the @exception tag.  |
| {@value}      |         显示常量的值，该常量必须是static属性。         | Displays the value of a constant, which must be a static field. |
| @version      |                      指定类的版本                      |                        @version info                         |

## JDK内置的3个注解

### @Override

- @Override表示被标记的方法是重写父类的方法
- 只能修饰方法

```java
public class Student extends Person{
    /*
    @Override注解表示下面的方法是重写父类的方法，如果不是重写的话，会提示错误
    */
    @Override
    public void eat(){
        System.out.println("子类的eat方法");
    }
}
```

### @Deprecated

- @Deprecated表示被标记的对象是已经过时的东西
- 可以修饰类、方法、构造器、属性

```java
public class Student extends Person {
    /*
    @Deprecated注解表示下面的方法是过期方法，可以修饰类、方法、构造器、属性
     */
    @Deprecated
    public void study(){
        System.out.println("过时的study方法");
    }
}
```

### @SuppressWarnings

- @SuppressWarnings表示抑制被标记对象的编译器警告

```java
public class Test02 {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        /*
        这里int age 被@SuppressWarnings修饰，所以就算后面age没有使用，也不会有编译器警告，否则,就会想num一样，有编译器警告。
        */
        @SuppressWarnings("unused")
        int age = 10;
        
        int num = 20;

        @SuppressWarnings({"unused","rwatypes"})
        ArrayList al = new ArrayList();
    }
}
```

## 元注解

- 元注解是用于修饰其他注解的注解
- 元注解共有四种：Retention, Target, Documented, Inherited

### Retention

- Retention修饰注解来==限定注解的生命周期==，@Rentention包含一个RetentionPolicy枚举类型的成员变量,使用@Rentention时必须为该value成员变量指定值
- 如果注解没有特别加Retention修饰的话，其实默认是用`@Retention(etentionPolicy.CLASS)`修饰
- Retention的成员变量
  - RetentionPolicy.SOURCE:在源文件中有效(即源文件保留)
    - 编译器直接丢弃这种策略的注释，在.class文件中不会保留注解信息
  - RetentionPolicy.CLASS:在class文件中有效(即class保留)
    - 保留在.class文件中，但是当运行Java程序时，他就不会继续加载了，不会保留在内存中，JVM不会保留注解。
  - RetentionPolicy.RUNTIME:在运行时有效(即运行时保留)
    - 当运行 Java程序时，JVM会保留注释，加载在内存中了，那么程序可以通过反射获取该注释

### Target

- Target元注解修饰来指定注解的使用范围，用于指定被修饰的注解能用于修饰哪些程序元素；@Target也包含一个名为value的成员变量
- Target的成员变量
  - `TYPE` 表示注解可以修饰 类、接口（包括注释类型）或枚举声明
  - `FIELD` 表示注解可以字段声明（包括枚举常量）
  - `METHOD` 表示注解可以修饰方法
  - `PARAMETER` 表示注解可以修饰参数
  - `CONSTRUCTOR` 表示注解可以修饰构造器
  - `LOCAL_VARIABLE` 表示注解可以修饰局部变量
  - `ANNOTATION_TYPE` 表示注解可以注释类型声明
  - `PACKAGE` 表示注解可以修饰包

### Documented

- 用于指定被该元注解修饰的注解类将被javadoc工具提取成文档。默认情况下，javadoc是 不包括注解的，但是加上了这个注解生成的文档中就会带着注解了

### Inherited

- 被它修饰的Annotation将具有继承性。如果某个类使用了被@Inherited修饰的Annotation,则其子类将自动具有该注解;