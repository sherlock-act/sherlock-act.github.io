# Java的运算符

- 算术运算符

```
+    (加)
-    (减)
*    (乘)
/    (除)
%    (取余)
++    (自增) // 参与运算的时候 ++在后，先运算，再+1    ++在前，先加1，再进行运算
--    (自减)// 参与运算的时候 --在后，先运算，再-1    --在前，先减1，再进行运算
```



- 赋值运算符

```
=   (将等号右侧的值，赋值给等号左侧)
```



- 扩展赋值运算符

```java
/*
+=
-+
*=
/=

a += b    可读性较差，但是编译效率高, 底层自动进行类型转换
a = a + b 可读性好，但是编译效率不如 a += b ，必须手动转换类型

*/

public class TestOpe07{
	public static void main(String[] args){
		// 实现功能：给出三个数，求和
		// 给出三个数
		int num1 = 10;
		int num2 = 20;
		int num3 = 30;
		
		// 求和
		// int sum = num1+num2+num3;
		// 定义一个变量，接收∑
		int sum = 0;
		// sum = sum + num1;
		// sum = sum + num2;
		// sum = sum + num3;
		//等效与下面的代码
		sum += num1;
		sum += num2;
		sum += num3;
		// 输出
		System.out.println(sum);
	}
}
```

- 关系运算符

```
>  大于
<  小于
>= 大于等于
<= 小于等于
== 相等
!= 不相等
```

- 逻辑运算符

```
&  与
|  或
&& 短路与  效率较高，只要第一个表达式是false，结果就是false，后面就不再计算了
|| 短路或  效率较高，只要第一个表达式是true，true，后面就不再计算了
!  逻辑非
^  逻辑异或  两个操作数一样，结果为false  两个操作数不一样，结果为true
```

- 条件运算符

```java
//?:  条件运算符，又叫三元运算法、三目运算符
//a?b:c  a是一个布尔类型的表达式，通过a的结果来确定最终表达式的结果，如果a为true，则结果为b，如果a的结果为false，则结果为c

import java.util.Scanner;


public class TestOpe12{
	public static void main(String[] args){
		// 实现功能，男孩女孩选择晚饭吃什么，如果一件一样，听男生的，如果一件不一样，听女生的
		Scanner sc = new Scanner(System.in);
		System.out.println("请选择今晚吃啥？1、火锅 2、烧烤 3、麻辣烫 4、西餐");
		// 俩人做选择
		System.out.print("请男孩作出选择");
		int boyChoice = sc.nextInt();
		System.out.print("请女孩作出选择");
		int girlChoice = sc.nextInt();
		
		// 判断
		System.out.println(boyChoice==girlChoice?"听男孩的，选择"+boyChoice:"听女孩的，选择"+girlChoice);
	}
}
```

- 位运算符

```
怎么区分位运算符和逻辑运算符？
逻辑运算符：左右两边是布尔类型的操作数
位运算符：左右两边是两个具体的数值

& 与
| 或
^ 异或
~ 反
>>  右移
<<  左移
>>> (了解！！！)
```

- 运算符的优先级别

赋值<三目<逻辑<关系<算术<单目