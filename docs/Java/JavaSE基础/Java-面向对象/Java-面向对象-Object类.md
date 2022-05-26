# Object类

- Object类是有所类的根基类，如果定义类的时候没有指定继承类的时候，实际上都是默认继承自object类

- - |    方法返回类型    | 方法作用解释                                                 |
    | :----------------: | :----------------------------------------------------------- |
    | `protected Object` | `clone()`  创建并返回此对象的副本。                          |
    |     `boolean`      | `equals(Object obj)`  指示一些其他对象是否等于此。           |
    |  `protected void`  | `finalize()`  当垃圾收集确定不再有对该对象的引用时，垃圾收集器在对象上调用该对象。 |
    |      `类<?>`       | `getClass()`  返回此 `Object`的运行时类。                    |
    |       `int`        | `hashCode()`  返回对象的哈希码值。                           |
    |       `void`       | `notify()`  唤醒正在等待对象监视器的单个线程。               |
    |       `void`       | `notifyAll()`  唤醒正在等待对象监视器的所有线程。            |
    |      `String`      | `toString()`  返回对象的字符串表示形式。                     |
    |       `void`       | `wait()`  导致当前线程等待，直到另一个线程调用该对象的 [`notify()`](../../java/lang/Object.html#notify--)方法或 [`notifyAll()`](../../java/lang/Object.html#notifyAll--)方法。 |
    |       `void`       | `wait(long timeout)`  导致当前线程等待，直到另一个线程调用 [`notify()`](../../java/lang/Object.html#notify--)方法或该对象的 [`notifyAll()`](../../java/lang/Object.html#notifyAll--)方法，或者指定的时间已过。 |
    |       `void`       | `wait(long timeout,  int nanos)`  导致当前线程等待，直到另一个线程调用该对象的 [`notify()`](../../java/lang/Object.html#notify--)方法或 [`notifyAll()`](../../java/lang/Object.html#notifyAll--)方法，或者某些其他线程中断当前线程，或一定量的实时时间。 |

- `toString`

  - 返回对象的字符串表示形式。一般来说，  `toString`方法返回一个“textually代表”这个对象的字符串。结果应该是一个简明扼要的表达，容易让人阅读。建议所有子类覆盖此方法。

  - 该`toString`类方法`Object`返回一个由其中的对象是一个实例，该符号字符`的类的名称的字符串`@`  ”和对象的哈希码的无符号的十六进制表示。 换句话说，这个方法返回一个等于下列值的字符串： 

  - `Object`中的`toString`方式在实际工作中常被进行重写为我们需要的方法。
  
  - ```java
  getClass().getName() + '@' + Integer.toHexString(hashCode())
    ```
  
  - ```java
    public class Test {
        // 这是main方法，是实现程序主要逻辑
        public static void main(String[] args) {
            Student s = new Student("feifei", 19, 160.7);
            System.out.println(s.getAge());
            System.out.println(s);
            System.out.println(s.toString());
        }
    }
    
    // 运行结果：
    /*
    19
    com.shanlei01.Student@1b6d3586
    com.shanlei01.Student@1b6d3586
  */
    
    ```
  
  // 在类中重写toString方法
    @Override
    public String toString() {
        return "Phone{" +
            "brand='" + brand + '\'' +
            ", price=" + price +
            ", year=" + year +
            '}';
    }
  
    ```
  
    ```
  
- `equals`方法

  - 指示一些其他对象是否等于此

  - `Object`类中，默认的是还是进行 `==`判断，无法满足判断两个对象是否相等的需求，所以一般工作中也对`equals`方法进行重写；

  - ```java
    public boolean equals(Object obj) {
    	/*
    	在对传入的对象进行判断之前，首先判断是否是这个类创建的实例对象，如果是才做比较，不是就是返回false
    	instanceof就是判断obj是否是Phone的实例对象
    	*/
        if(obj instanceof Phone){ // instanceos 判断obj是否是Phone的实例对象，如果是返回true，如果不是返回false
            // 将obj转为Phone类型
            Phone other = (Phone)obj;
            if(this.getBrand() == other.getBrand() & this.getPrice() == other.getPrice() & this.getYear() == other.getYear()){
                return true;
            }
        }
        return false;
    }
    ```

  - 

