# Java流程控制--分支结构--if

## 单分支

- 结构：

```
if(条件表达式，这个表达式的结果是布尔值：要么是false，要么是true){
    //如果上面()中的表达式返回结果是true，那么执行{}中代码
    //如果上面()中的表达式返回结果是false ，那么不执行{}中代码
    //PS:{}中的代码是否执行，取决于()中表达式的返回结果
}
```

- 单分支之间，每一个选择是独立的，依次判断执行的
- if后面的()中的条件，要按照自己需求尽量完善
- {}可以省略不写,但是一旦省略，这个if就只负责后面的一句话，所以我们不建议初学者省略

```java
public class TestIf01{
	public static void main(String[] args){
		// 实现功能：根据所得分数，判断获得的奖项
		int num1 = 6;
		int num2 = 6;
		int num3 = 6;
		
		// 对分数进行求和
		int sum = 0;
		sum += num1;
		sum += num2;
		sum += num3;
		
		// 判断获得的奖项
		if(sum>=14){
			System.out.println("恭喜获得一等奖，lucky guy");
		}
		if(sum>=10&&sum<14){
			System.out.println("恭喜获得二等奖，good");
		}
		if(sum>=6&&sum<10){
			System.out.println("恭喜获得三等奖，just ok");
		}
		if(sum<6){
			System.out.println("真糟糕，你获得的是安慰奖，bad luck");
		}
		
	}
}

```

## 多分支-if--else

- 结构

```
if(布尔表达式1) {
        语句块1;
} else if(布尔表达式2) {
        语句块2;
}……
else if(布尔表达式n){
        语句块n;
} else {
        语句块n+1;
}
```

- 当布尔表达式1为真时，执行语句块1；否则，判断布尔表达式2，当布尔表达式2为真时，执行语句块2；否则，继续判断布尔表达式3······；如果1~n个布尔表达式均判定为假时，则执行语句块n+1，也就是else部分
- ==多分支：好处：只要满足一个 分支以后，后面的分支就不需要判断了 --》效率高==

```
import java.util.Scanner;
public class TestIf05{
	public static void main(String[] args){
		/*
		小朋友搬桌子：
		年龄大于7岁，可以搬桌子；
		如果年龄大于5岁，性别是男，可以搬桌子；
		否则不可以搬动桌子，提示：你还太小了
		*/
		Scanner sc = new Scanner(System.in);
		System.out.print("请输入小朋友的年龄");
		if(sc.hasNextInt()){
			int age = sc.nextInt();
			if(age>=7){
				System.out.println("小朋友已经可以搬桌子了");
			}else if(age>=5){
				System.out.print("小朋友的年龄不到7岁，小朋友的性别是？1、男孩 2、女孩");
				if(sc.hasNextInt()){
					int gender = sc.nextInt();
					if(gender == 1){
						System.out.println("虽然小朋友年龄不到7岁，但是男孩子可以搬桌子");
					}else{
						System.out.println("小女孩还太小了，不适合搬桌子");
					}
				}else{
					System.out.println("您的输入有误");
				}
			}else{
				System.out.println("小朋友太小了，不适合搬桌子");
			}
		}else{
			System.out.println("请输入正确的年龄");
		}
	}
}
```

# Java流程控制--分支结构--switch

- 语法结构

```
switch(){
                        case * :
                        case * :
                        .......
                }
```

- switch后面是一个()，()中表达式返回的结果是一个等值，这个等值的类型可以为：int,byte,short,char,String,枚举类型
- 这个()中的等值会依次跟case后面的值进行比较，如果匹配成功，就执行:后面的代码
- 为了防止代码的“穿透”效果：在每个分支后面加上一个关键词break，遇到break这个分支就结束了
- 类似else的“兜底”“备胎”的分支：default分支
- default分支可以写在任意的位置上，但是如果没有在最后一行，后面必须加上break关键字，如果在最后一行的话，break可以省略
- 相邻分支逻辑是一样的，那么就可以只保留最后一个分支，上面的都可以省去不写了
- switch分支和if分支区别：
  - 表达式是等值判断的话--》if ，switch都可以
  - 如果表达式是区间判断的情况---》if最好
- switch应用场合：就是等值判断，等值的情况比较少的情况下

```java
public class TestSwitch{
	public static void main(String[] args){
		/*
		实现一个功能：
		根据给出的学生分数，判断学生的等级：
		>=90  -----A
		>=80  -----B
		>=70  -----C
		>=60  -----D
		<60   -----E
		*/
		int score = (int)(Math.random()*100)+1;
		System.out.println("学生成绩："+score+"分");
		switch(score/10){
			case 10 :
			case 9 :
				System.out.println("A等");
				break;
			case 8 :
				System.out.println("B等");
				break;
			case 7 :
				System.out.println("C等");
				break;
			case 6 :
				System.out.println("D等");
				break;
			case 5 :
			case 4 :
			case 3 :
			case 2 :
			case 1 :
			case 0 :
				System.out.println("E等");
				break;
			default:
				System.out.println("成绩错误");
		}
	}
}
```

