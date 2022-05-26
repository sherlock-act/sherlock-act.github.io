# While循环

- 语法结构

```java
while (布尔表达式) {
            循环体;
}
```

- 循环作用：将部分代码重复执行。
- 循环只是提高了程序员编写代码的效率，但是底层执行的时候依然是重复执行。
- 循环四要素：
  - 条件初始化 -- > 布尔表达式中的判断变量的初始化
  - 判断条件 --> while中的布尔表达式
  - 循环体 --> 每次循环需要执行的语句
  - 迭代 --> 判断条件进行迭代

```java
public class TestWhile{
	public static void main(String[] args){
		// 功能 1+2+3+4+5
		int num = 1;
		int sum = 0;
		while(num<=5){
			sum += num++;
		}
		System.out.println(sum);
	}
}
```

# do-while循环

- 语法结构

```java
do {
            循环体;
    } while(布尔表达式) ;
```

- do-while循环结构会先执行循环体，然后再判断布尔表达式的值，若条件为真，执行循环体，当条件为假时结束循环。
- ==do-while循环的循环体至少执行一次==

```java
public class TestDoWhile{
	public static void main(String[] args){
		// 1+2+3+4+5+6......+100
		int num1 = 1;
		int sum1 = 0;
		do{
			sum1 += num1++;
		}while(num1<=100);
		System.out.println(sum1);
		
		// while与dowhile的区别
		int num2 = 101;
		int sum2 = 0;
		while(num2<=100){
			sum2 += num2++;
		}
		System.out.println("while的结果"+sum2);
		
		int num3 = 101;
		int sum3 = 0;
		do{
			sum3 += num3++;
		}while(num3<=100);
		System.out.println("dowhile的结果"+sum3);
	}
}
```

# for循环

- 语法结构

```java
for (初始表达式; 布尔表达式; 迭代因子) {
          循环体;
}
```

- for循环语句是支持迭代的一种通用结构，是最有效、最灵活的循环结构
- for循环在第一次反复之前要进行初始化，即执行初始表达式；随后，对布尔表达式进行判定，若判定结果为true，则执行循环体，否则，终止循环；最后在每一次反复的时候，进行某种形式的“步进”，即执行迭代因子

```java
public class TestFor{
	public static void main(String[] args){
		// 1+2+3+4+5...+100
		int sum =0;
		for(int i = 1;i<=100;i++){
			sum += i;
		}
		System.out.println(sum);
	}
}
```

# 停止循环break

- 在循环中可以在任何地方使用`break`，当程序运行到`break`的时候，就会退出当前循环

```java
public class TestFor02{
	public static void main(String[] args){
		// 求1-100的和，当第一次超过300就停止
		int sum = 0;
		for(int i = 0;i <= 100;i++){
			sum += i;
			if(sum<=300){
				
				System.out.println(sum);
			}else{
				break;//停止循环
			}
			
		}
	}
}
```

- ==break停止循环的时候，默认是停止当前最近的循环==

- ==要让break停止我们需要的循环，可以在循环前加上标签，然后使用`break 标签`停止对应的循环==

```java
public class TestFor03{
	public static void main(String[] args){
		int sum = 0;
		outer: // 给for循环一个叫outer的标签，标签也可以写在for循环前面（outer:for(){}）
		for(int i = 0;i <= 100;i++){
			sum += i;
			while(sum>300){
				break outer;// 停止标签名为outer的循环，不然默认停止的是当前的while循环
			}
			System.out.println(sum);
		}
	}
}
```

# 停止循环continue

- 在循环中可以在任何地方使用`continue`，当程序运行到`continue`的时候，就会==退出本次循环，然后执行下一次循环。==

```java
public class TestFor04{
	public static void main(String[] args){
		for(int i = 1;i <= 100; i++){
			if(i==36){
				continue;//当i等于36的时候，退出本次循环，并开始下一次循环，控制台输出为1-100不包含36
			}
			System.out.println(i);
		}
	}
}
```

- ==continue停止循环的时候，默认是停止当前最近的循环==

```java
public class TestFor04{
	public static void main(String[] args){
		for(int i = 1;i <= 100; i++){
			if(i==36){
				continue;//当i等于36的时候，退出本次循环，并开始下一次循环，控制台输出为1-100不包含36
			}
			System.out.println(i);
		}
	}
}
```

- ==要让continue停止我们需要的循环，可以在循环前加上标签，然后使用`continue 标签`停止对应的循环==

```java
public class TestFor05{
	public static void main(String[] args){
		outer: // 给for循环一个叫outer的标签，标签也可以写在for循环前面（outer:for(){}）
		for(int i=1;i<=100;i++){
			while(i==36){
				continue outer;// 停止标签名为outer的循环，不然默认停止的是当前的while循环
			}
			System.out.println(i);
		}
	}
}
```

# 停止当前方法 return

- 当程序执行遇到`return`的时候，直接退出当前方法，然后将return后面的东西返回给调用这个方法的语句，`return`后面不加东西就是返回空值

```java
public class TestFor06{
	public static void main(String[] args){
		for(int i=1;i<=100;i++){
			if(i==36){
				return;// 直接退出当前main方法，main方法中最后一句输出不会执行
			}
			System.out.println(i);
		}
		System.out.println("--return直接停止当前main方法，本次不会输出--");
	}
}
```

