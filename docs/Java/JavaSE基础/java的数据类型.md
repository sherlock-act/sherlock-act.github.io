# Java的数据类型

- java是一种强类型语言，每个变量在定义的时候必须声明数据类型
- java数据类型有两种：基本数据类型（primitive date type）和引用数据类型（reference date type）
![](https://img2020.cnblogs.com/blog/2176336/202011/2176336-20201121191421085-2090912401.png)
## Java的整数类型
### 整数类型占用空间与取值范围
| 类型  | 占用空间 | 表数范围                             |
| ----- | -------- | ------------------------------------ |
| byte  | 1字节    | -2^7 ~ 2^7(-128~127)                 |
| short | 2字节    | -2^15 ~ 2^15-1(-32768~32767)         |
| int   | 4字节    | -2^31 ~ 2^31-1(大约正负21亿4千7百万) |
| long  | 8字节    | -2^63 ~ 2^63-1                       |
==注意：java中，整数类型默认的是int，所以就算前面声明变量类型为long的时候，要是数值超过了int的表数范围，就需要在数值后面加l或者L==
### 各种进制的整数申明方式
| 进制类型 | 声明方式           | 示例   |
| -------- | ------------------ | ------ |
| 十进制   | 没有特殊标识       | 99,100 |
| 八进制   | 要求以0开头        | 015,07 |
| 十六进制 | 要求以0x或0X开头   | 0X15   |
| 十进制   | 要求以0b后者0B开头 | 0b11   |
```java
public class TestVar05{
	public static void main(String[] args){
		// 定义整数类型变量：
		int num1 = 100 ; // 默认情况赋值就是十进制
		System.out.println(num1);
		int num2 = 012 ; // 前面加0  标识八进制
		System.out.println(num2);
		int num3 = 0x12; // 前面加0x或者0X 标识十六进制
		System.out.println(num3);
		int num4 = 0b10; // 前面加0b或者0B 标识二进制
		System.out.println(num4);
		// 给变量赋值的时候，值可以为不同的进制，但是底层运算的时候默认会转换成十进制
		byte b = 12; // 定义了一个名字叫b的byte类型变量，赋值为12
		// 如果赋值的时候，数值超过数据类型的表数范围，会报错
		System.out.println(b);
		short s = 30000;
		System.out.println(s);
		int i = 12345;
		System.out.println(i);
		long num5 = 1234567890L; // 给long类型赋值，需要在数字和面加l或者L
		System.out.println(num5);
		
	}
}
```
## Java的浮点类型
- float类型又被称为单精度类型，尾数可以精确到7为有效数字，很多情况下，float类型经度很难满足需求
- double数值经度约为float的两倍，所以又称为双精度类型
- ==浮点类型默认是double类型，所以float类型的数值赋值的时候要在后面加f或者F，没有的话默认类型为double==
- double默认情况不用特殊加后缀，但是也可以使用d或者D明确为double类型
### 浮点类型占用空间与取值范围
| 类型   | 占用空间 | 表数范围                                          |
| ------ | -------- | ------------------------------------------------- |
| float  | 4字节    | 大于±3.402823 47E+38F（有效位数为6-7位）          |
| double | 8字节    | 大于±1.797693134862315 70E+308（有效位数15-16位） |
==注意：有效数字，指的是从左往右第一个不为0的数到最后一个数，例如0.00521，有效数字就是3位==
==最好不要进行浮点类型的比较，精度不同，就算赋值的时候一样，但是比较的时候，值是不同的==
```java
public class TestVar06{
	public static void main(String[] args){
		// 浮点类型的常量有两种新市
		// 十进制形式：
		double num1 = 3.14;
		System.out.println(num1);
		// 科学计数形式
		double num2 = 314E-2;
		System.out.println(num2);
		
		// 浮点类型的变量
		//浮点类型默认是double类型，所以float类型的数值赋值的时候要在后面加f或者F，没有的话默认类型为double
		float f1 = 3.1412342131231234234123F;
		System.out.println(f1);
		//double默认情况不用特殊加后缀，但是也可以使用d或者D明确为double类型
		double d1 = 3.1412342131231234234123D;
		System.out.println(d1);
		
	}
}
```

## Java的字符型

- java中使用==单引号==来标识字符常量，char类型用来标识在Unicode编码表中的字符，Unicode编码被设计用来处理各种语言的文字，它占用2个字节，允许有65536个字符

### 转义字符

- 转移字符：就是将\后面的普通字符转换为特殊含义

| 转义符 |       含义        |
| :----: | :---------------: |
|   \b   | 退格（backspace） |
|   \n   |       换行        |
|   \r   |       回车        |
|   \t   |   制表符（tab）   |
|   \"   |      双引号       |
|   \'   |      单引号       |
|   \\   |      反斜杠       |

```java
public class TestVar07{
	public static void main(String[] args){
		// 定义字符类型的变量
		char ch1 = 'a';
		System.out.println(ch1);
		char ch2 = 'A';
		System.out.println(ch2);
		char ch3 = '4';
		System.out.println(ch3);
		char ch4 = '镡';
		System.out.println(ch4);
		char ch5 = '?';
		System.out.println(ch5);
		char ch6 = ' ';
		System.out.println(ch6);
		// java中无论字母、数字、符号、中文都是字符类型的常量，都占用2个字节
		//字符类型：单引号引起来的单个字符
		System.out.println("------------------------------");
		/*
		转移字符：
		将\后面的普通字符转换为特殊含义
		*/
		char ch7 = '\n';
		System.out.println("aaa" + ch7 + "bbb");
		
		System.out.println("aaa\nbbb");
		System.out.println("------------------------------");
		System.out.println("aaa\bbbb");
		System.out.println("aaa\rbbb");
		System.out.println("\"java\"");
	}
}
```

- ==字符在原样输出的时候，是字符本身，但是在在底层进行计算的时候，实际上是当做一个码来进行计算==

```java
public class TestVar08{
	public static void main(String[] args){
		char ch1 = 'A';
		System.out.println(ch1);
		System.out.println(ch1 + 90); // 155
		System.out.println(155 - ch1); // 90
		// char类型我们考到的样子就是它本身的字面常量，但是底层的计算实际是按照一个码来进行计算的
		// 这个码表就是ASSCII码表
		System.out.println("-------------------------");
		
		char ch2 = '镡';
		System.out.println(ch2);
		System.out.println(ch2 + 90); // 38331
		System.out.println(38331 - ch2); // 90
		
		System.out.println("-------------------------");
		System.out.println((int)ch2); // 38241
		System.out.println((char)38241);
		
		int num2 = '镡';
		System.out.println(num2);
		
		char ch5 = 38241;
		System.out.println(ch5);
	}
}
```

## Java的布尔类型

- boolean类型只有两个常量值，true和false 在内存中占一位（不是一个字符），==不可以使用0或者非0的整数代替true或者false==，这点和C语言与python语言不同。boolean用来判断逻辑条件。

```java
public class TestVar09{
	public static void main(String[] args){
		boolean flag1 = true;
		System.out.println(flag1);
		boolean flag2 = false;
		System.out.println(flag2);
		boolean flag3 = 5 == 9;
		System.out.println(flag3);
		boolean flag4 = 5 < 9;
		System.out.println(flag4);
		
	}
}
```

## 基本数据类型转换

- 数据类型转换有两种形式
  - 自动类型转换
  - 强制类型转换
- 进行数据计算的时候，数据类型转换的形式
  - 左 == 右   直接赋值
  - 左 <   右   强转
  - 左 >   右   直接自动转换
  - 但是在byte，short，char类型中，只要数据再表数范围内，赋值的时候就不需要进行强制类型转换
- 在同一个表达式中，有多个数据类型的时候（不能有布尔类型），机器按照表达式中级别最高的那个类型将其他类型的数据转换成最高的类型进行计算
  - 数据类型级别（从低到高）
  - byte,short,char-->int-->long-->float-->double

```java
public class TestVar10{
	public static void main(String[] args){
		double d = 5; //int --> double
		System.out.println(d); // 5.0
		//int i = 8.2;// double-->int
		// 错误: 不兼容的类型: 从double转换到int可能会有损失
		//System.out.println(i);
		int i = (int)8.2; // 强制类型转换
		System.out.println(i);
		System.out.println("-----------------------");
		//double d2 = 12 + 2134L + 0.5F + 3.81 + 'a'; + true  报错
		double d2 = 12 + 2134L + 0.5F + 3.81 + 'a';
		System.out.println(d2);
	}
}
```

### 修饰符final

- 一个变量被final修饰，这个变量就变成了常量，这个常量值就不能改变了，这个常量就是字符常量
- 约定俗称：字符常量的名字全部大写

```java
import java.util.Scanner; // 导入Scanner包, 在java.util下将Scanner导入

public class TestVar11{
	public static void main(String[] args){
		// 实现功能，求圆的周长和面积
		final double PI = 3.1415926;
		//让扫描器扫描键盘录入的int类型的数据
		Scanner sc = new Scanner(System.in);
		System.out.print("请录入半径：");
		int r = sc.nextInt();

		// 求周长
		double c = 2*PI*r;
		System.out.println("周长为：" + c);
		
		// 求面积
		double s = PI*r*r;
		System.out.println("面积为：" + s);
	}
}
```

