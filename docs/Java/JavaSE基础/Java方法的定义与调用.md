#  定义与调用方法

- 定义方法（Method）就是一段用来完成某个特定功能而独立的一段代码片段，类似与其他语言中的函数（function）
- 方法的格式

```java
[修饰符1、修饰符2····] 返回值类型 方法名(形参){
    实现逻辑
}
```

- 方法最大的作用是提高代码的复用性，重复使用的独立功能建议封装为方法

```java
public class TestMethod{
	public static void main(String[] args){
		int num = add(25,47); // 调用方法，并给方法传递两个int类型的实参
		System.out.println(num);
		System.out.println(add(500,456));
	}
	public static int add(int num1, int num2){ // 定义名字为add的方法，放回int类型的值，有两个int类型的形参
		int sum=0;
		sum += num1;
		sum += num2;
		return sum;// 实现两个int类型数值想加，并返回给调用方法的地方
	}
}
```

# 方法的重载

- 在java中可以在同一个类中定义多个名字相同的方法，但是这些方法的形参不同，此时，在进行调用的时候，会根据传入的实参的不同，自动匹配对应的方法
- 本质上，重载实际上是不同的方法，只是方法的名称相同而已
- 构成重构的条件
  - 不同的含义
    - 形参类型不同
    - 形参个数不同
    - 形参顺序不同
  - 不同的修饰符与返回值不同，不具备构成重构的条件，是方法的重复定义
  - 只有形参名称不同，也不具备构成重构的条件

```
（1）个数不同
add()   add(int num1)   add(int num1,int num2)
（2）顺序不同
add(int num1,double num2)   add(double num1,int num2)
（3）类型不同
add(int num1)   add(double num1)
```

- 注意，当调用重构的方法的时候，如果传入的实参与形参数据类型完全匹配的方法会优先调用，如果没有完全匹配的方法，会根据数据类型运算级别决定调用优先级

# 方法的可变参数

- 可变参数是jdk1.5之后提供的功能，提供了一个方法，形参接收的参数个数是可变的，解决部分方法重载的问题
- 可变参数的使用方法：
  - `int...num`
  - `double...num`
  - `boolean...num`
- 方法的内部对可变参数的处理跟数组是一样的
- 可变参数和其他数据一起作为形参的时候，可变参数一定要放到最后

```java
public class TestArray09{
	public static void main(String[] args){
		method(1);
		method(1,2,3,4,5,6,7,8);
		method(1,new int[]{9,10,11,12,13,14,15});
	}
	public static void method(int num1,int...num2){// 定义可变参数与普通参数都定义的时候，可变参数一定要放在普通参数后面
		System.out.println("-----1");
		for(int i:num2){// 方法内部对可变参数的处理与数组一样
			System.out.println(i);
		}
		System.out.println(num2);
	}
}
```

