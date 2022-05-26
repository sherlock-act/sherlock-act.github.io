# Java的反射机制

- JAVA反射机制是在==运行状态==中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意方法和属性；
- 这种动态获取信息以及动态调用对象方法的功能称为java语言的反射机制。
- 反射机制多用于程序运行后才能确定创建的类的场景
- 首先准备了两个类，一个接口与一个注解

```java
// 自定义注解
@Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE})
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation {
    String value();
}
```

```java
// 自定义接口
public interface MyInterface {
    // 自定义接口
    void myMethod();
}
```

```java
// Person类
public class Person implements Serializable {
    // attribute
    private int age;
    public String name;
    // method
    private void eat(){
        System.out.println("Person--eat");
    }
    public void sleep(){
        System.out.println("Person--sleep");
    }
}
```

```java
// Student类
@MyAnnotation("hello")
public class Student extends Person implements MyInterface {
    // 属性
    private int sno;//学号
    double height;//身高
    protected double weight;// 体重
    public double score;// 成绩
    
    // 方法
    public String showInfo(){
        return "我是一名三好学生";
    }

    @MyAnnotation("hi method")
    public String showInfo(int a, int b){
        return "我是一名三好学生,重载方法";
    }

    private void work(int a){
        System.out.println("好好工作，码农");
    }

    void happy(){
        System.out.println("做人要开心");
    }

    protected int getSno(){
        return sno;
    }

    // 构造器
    public Student(){

    }

    public Student(double weight, double height){
        this.weight = weight;
        this.height = height;
    }

    private Student(int sno){
        this.sno = sno;
    }

    Student(int sno, double height){
        this.sno = sno;
        this.height = height;
    }

    protected Student(int sno,double height,double weight){
        this.sno = sno;
        this.height = height;
        this.weight = weight;
    }

    @Override
    @MyAnnotation("hello mymethod")
    public void myMethod() throws RuntimeException{
        System.out.println("重写接口方法");
    }

    @Override
    public String toString() {
        return "Student{" +
                "sno=" + sno +
                ", height=" + height +
                ", weight=" + weight +
                ", score=" + score +
                '}';
    }
}
```

## 获取类的构造器与创建对象

- 反射机制中，无论是进行什么操作，首先都需要先获取字节码信息`xxx.class`，然后才能通过字节码信息完成后续操作

```java
public class Test01 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
        // 获取字节码信息
        Class cls = Student.class;

        // 通过字节码信息获取构造器
        // getConstructors() 只能获取当前运行时类被public修饰的构造器
        Constructor[] c1 = cls.getConstructors();

        for(Constructor c:c1){
            System.out.println(c);
        }
        System.out.println("---------------------------");

        // getDeclaredConstructors() 获取运行时，类的全部修饰符的构造器
        Constructor[] c2 = cls.getDeclaredConstructors();

        for(Constructor c: c2){
            System.out.println(c);
        }
        System.out.println("---------------------------");

        // 获取指定的构造器
        // 什么都不传的话，会获得public修饰的空参构造器
        Constructor con1 = cls.getConstructor();
        System.out.println(con1);

        // 获取两个参数的public修饰的有参构造器
        Constructor con2 = cls.getConstructor(double.class, double.class);
        System.out.println(con2);

        // 获取一个参数的private修饰的有参构造器
        Constructor con3 = cls.getDeclaredConstructor(int.class);
        System.out.println(con3);

        // 使用构造器创建对象
        Object o1 = con1.newInstance();
        System.out.println(o1);

        Object o2 = con2.newInstance(120.5, 180.4);
        System.out.println(o2);
    }
}
```

## 获取类的属性并进行赋值

```java
public class Test02 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws NoSuchFieldException, IllegalAccessException, InstantiationException {
        // 获取字节码信息
        Class cls = Student.class;
        
        // 获取属性
        // getFields() 获取运行时类和父类中被public修饰的属性，包含父类
        Field[] fields = cls.getFields();
        for(Field f:fields){
            System.out.println(f);
        }
        System.out.println("________________________________");

        // getDeclaredFields 获取运行时类中的所有属性，不包含父类
        Field[] declaredFields = cls.getDeclaredFields();
        for(Field f:declaredFields){
            System.out.println(f);
        }
        System.out.println("________________________________");

        // 获取指定属性
        Field score = cls.getField("score");
        System.out.println(score);

        Field sno = cls.getDeclaredField("sno");
        System.out.println(sno);
        System.out.println("________________________________");

        // 属性的具体结构
        // 获取修饰符
        int modifiers = sno.getModifiers();
        System.out.println(modifiers);
        System.out.println(Modifier.toString(modifiers));
        // 获取属性的数据类型
        Class type = sno.getType();
        System.out.println(type.getName());
        // 获取属性的名字
        System.out.println(sno.getName());
        System.out.println("________________________________");

        // 给属性赋值 给属性赋值，必须要有这个类的对象，首先要创建对象才行
        Field sco = cls.getField("score");
        Object obj = cls.newInstance();
        sco.set(obj, 98);
        System.out.println(obj);

    }
}
```

## 获取方法并调用方法

```java
public class Test03 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws NoSuchMethodException, IllegalAccessException, InstantiationException, InvocationTargetException {
        // 首先获取字节码信息
        Class cls = Student.class;

        // 获取public修饰的方法 包含父类
        Method[] me1 = cls.getMethods();
        for(Method m:me1){
            System.out.println(m);
        }
        System.out.println("________________________");

        // 获取所有的方法,不包含父类
        Method[] me2 = cls.getDeclaredMethods();
        for(Method m:me2){
            System.out.println(m);
        }
        System.out.println("________________________");

        // 获取指定方法(无参）
        Method showInfo = cls.getMethod("showInfo");
        System.out.println(showInfo);

        // 获取指定方法(有参）
        Method showInfo2 = cls.getMethod("showInfo",int.class,int.class);
        System.out.println(showInfo2);

        //获取private修饰的方法
        Method work = cls.getDeclaredMethod("work",int.class);
        System.out.println(work);
        System.out.println("________________________");

        // 获取方法的具体结构
        /*
        @注解
        修饰符 返回值类型 方法名(参数列表) throws XXXX{}
         */
        // 方法名
        System.out.println(work.getName());
        // 修饰符
        int modifiers = work.getModifiers();
        System.out.println(Modifier.toString(modifiers));
        // 返回值
        System.out.println(work.getReturnType());
        // 参数列表
        Class[] parameterTypes = work.getParameterTypes();
        for(Class c:parameterTypes){
            System.out.println(c);
        }
        // 注解
        Method myMethod = cls.getMethod("myMethod");
        Annotation[] annotations = myMethod.getAnnotations();
        for(Annotation a:annotations){
            System.out.println(a);
        }
        // 异常
        Class[] exceptionTypes = myMethod.getExceptionTypes();
        for(Class c:exceptionTypes){
            System.out.println(c);
        }
        System.out.println("________________________");

        // 调用方法
        Object o = cls.newInstance();
        myMethod.invoke(o);

        System.out.println(showInfo2.invoke(o, 12, 14));
    }
}
```

## 获取类的结构相关信息

```java
public class Test04 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        // 获取字节码信息
        Class cls = Student.class;

        // 获取运行时类的接口
        Class[] interfaces = cls.getInterfaces();
        for(Class c:interfaces){
            System.out.println(c);
        }
        System.out.println("____________________________");

        // 获取父类的接口
        // 先得到父类的字节码信息
        Class superclass = cls.getSuperclass();
        // 获取父类接口
        Class[] interfaces1 = superclass.getInterfaces();
        for(Class c:interfaces1){
            System.out.println(c);
        }
        System.out.println("____________________________");

        // 运行时类所在包
        Package aPackage = cls.getPackage();
        System.out.println(aPackage);
        System.out.println(aPackage.getName());
        System.out.println("____________________________");

        // 运行时类的注解
        Annotation[] annotations = cls.getAnnotations();
        for(Annotation a:annotations){
            System.out.println(a);
        }
    }
}
```

