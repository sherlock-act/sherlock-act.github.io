# Java泛型的使用

- 泛型其实就是一个标签，用来限制集合中数据类型，方便数据的管理；
- Collection<E>, List<E>， ArrayList<E> 这个<E>就是类型参数，即泛型。
- 泛型实际就是 一个<>引起来的 参数类型，这个参数类型  具体在使用的时候才会确定具体的类型。
- 使用了泛型以后，可以确定集合中存放数据的类型，在编译时期就可以检查出来。
- 泛型的类型：都是引用数据类型，不能是基本数据类型。
- JDK1.7之后，可以写成`ArrayList<Integer> al = new ArrayList<>(); `后面`<>`号里面可以不指明数据类型，会根据前面的数据类型确定，这种`<>`称为`钻石运算符`

## 泛型类与接口

- 定义泛型类与接口就是在类名或接口名后面加上`<>`就可以了

```java
public class GenericTest<E> {
}    
public interface GenericInterfaceTest<E> {
}
```

- 子类(实现类)继承自父类(实现接口)的时候，如果父类或接口指定了泛型的数据类型，那么子类与实现类就不用再指定泛型类型了

```java
public class SubGenericTest extends GenericTest<Integer> implements GenericInterfaceTest<Integer> {
}
```

- 子类(实现类)继承自父类(实现接口)的时候，如果父类或接口没有指定了泛型的数据类型，那么子类与实现类也必须需要定义为泛型类

```java
public class SubGenericTest2<E> extends GenericTest<E> implements GenericInterfaceTest<E> {

}
```

## 泛型方法

- 不是带泛型的方法就是泛型方法
- 泛型方法对应的那个泛型参数类型 和  当前所在的这个类 是否是泛型类，泛型是啥  无关
- 泛型方法定义的时候，修饰符后面需要加上<数据类型>，不然程序会出错
- 泛型方法的数据类型在调用的时候才确定
- 正是因为泛型方法的数据类型是在调用的时候才确定，所有泛型方法可以定义为静态方法

```java
public class Person<E> {
    // 非泛型方法
    public void a(E e){
        System.out.println("a方法不能算泛型方法");
    }

    // 泛型方法
    public static<T> void b(T t){
        System.out.println("b方法是泛型方法");
    }
}
```

## 泛型的通配符

- 使用泛型的时候，只是在编译期进行限制，实际上，底层都是Object类型的数据；
- 所以，就算A 和 B是子类父类的关系，G<A>和G<B>也不存在子类父类关系，他们是并列存在的
- 为了可以使泛型使用父类子类关系，所以可以使用G<?>通配符?来指定类型
- 这样G<?>就变成了 G<A>和G<B>的父类

```java
public class Demo {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        List<Object> list1 = new ArrayList<>();
        List<String> list2 = new ArrayList<>();
        List<Integer> list3 = new ArrayList<>();
        /*
        list1 = list2;
        list1 = list3;
        A 和 B是子类父类的关系，G<A>和G<B>不存在子类父类关系，是并列的
         */

        List<?> list = new ArrayList<>();
        list = list1;
        list = list2;
        list = list3;
        /*
        加入通配符？后，G<?>就变成了 G<A>和G<B>的父类
         */
    }
}
```

## 泛型受限

- 泛型受限就是规定使用通配符的泛型数据类型的范围
- 有上限与下限两种限制方式
  - 上限规定后包括了指定的数据类型
  - 下行规定后不包括指定的数据类型

```java
public class Test {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        List<Object> a = new ArrayList<>();
        List<Person> b = new ArrayList<>();
        List<Student> c = new ArrayList<>();

        // 泛型的上限
        List<? extends Person> list1 = new ArrayList<>();
        /*
        List<? extends Person> 相当于泛型里面的数据类型继承自Person，通配符里面的数据类型可以是Person以及Person的所有子类
         */

        // 泛型的下限
        List<? super Student> list2 = new ArrayList<>();
        /*
        List<? super Student>相当于泛型里面的数据类型是所有Student的直接父类与间接父类
         */
    }
}
```

