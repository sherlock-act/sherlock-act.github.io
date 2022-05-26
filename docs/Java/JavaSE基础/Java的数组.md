# 什么是数组

- 数组是用来存储数据的容器，在程序设计中，为了处理方便，数组用来将相同类型的若干数据组织起来。

# 数组的定义

```java
int[] arr;
int arr[];
// 以上两种方式定义数组均可以，看个人习惯
int arr[] = null; //定义数组的时候赋值null，和只定义，不赋值是不同的效果，赋值null会开辟空间，但是只定义不赋值不会开辟空间
int arr[] = new int[4]; // 定义一个长度为4的数组 arr
```

## 数组有默认的初始化值

- 基本数据类型的默认初始化值
  - `byte[]` -->0
  - short[]` -->0
  - `int[]` -->0
  - `long[]` -->0
  - `float[]` -->0.0
  - `double[]` -->0.0
  - `char[]` -->'\u0000' 就是unicode中对用的一个空格
  - `boolean[]` -->flase
- 引用数据类型的默认初始值
  - 引用数据类型的默认初始值都是null

# 数组的赋值

```java
arr[0] = 12;
arr[1] = 65;
arr[2] = 45;
arr[3] = 85;
```

# 数组的使用

```java
// 直接使用 数组名[索引] 就可以取出数组中对应索引的数据
arr[2];
// 取出来的数据可以进行各种符合数据类型使用方法的操作
System.out.println(arr[2]);
System.out.println(arr[2]+100);
```

# 数组的五个特点

- 数组一定被创建后，长度就是固定的，大小不可以该表
- 数组内的元素数据类型必须是相同类型，不允许出现混合类型
- 数组类型可以是任何数据类型，包括基本数据类型和引用数据类型
- 数组的索引从0开始，到 数组.length-1结束
- 数组变量属于引用类型，数组也是对象

# 数组的遍历

- 数组的遍历有以下两种方法
- 通过for循环进行遍历

```java
// 方式一：通过for循环进行数组遍历
for(int i=0;i<10;i++){
	System.out.println("第"+(i+1)+"个学生的成绩是："+arr[i]);
}
```

- 增强型for循环

```java
// 方式二：通过for循环进行数组遍历
for(int num:arr){
	System.out.println("学生的成绩是："+num);
}
```

- 增强型for循环的有点与缺点
  - 优点：代码简单
  - 缺点：单纯的增强for循环不能涉及跟索引相关的操作

# 数组的初始化

- 静态初始化

```java
int[] arr = {45,65,85,65,21};
int[] arr = new int[]{45,65,98,65,21};
// 直接在定义数组的时候同时，直接赋值，new int[]{}  中括号内不能写数组长度，不然会报错
```

- 动态初始化

```java
int[] arr = new int[4];
arr[0] = 34;
arr[1] = 65;
arr[2] = 94;
arr[3] = 41;
// 先定义数组，确定数组长度，然后再进行赋值
```

- 默认初始化

```java
int[] arr = new int[4];
// 定义数组，确认长度，数组内的值是各类型的默认值
```

# 求数组中的最值的方法

```java
public class TestArray04{
	public static void main(String[] args){
		// 求数组的最值
		/*
		int[] arr = {12,56,34,78,33,8,98};
		int maxNum=0;
		for(int i=0;i<arr.length;i++){
			if(arr[i]>maxNum){
				maxNum=arr[i];
			}
		}
		System.out.println("数组的最大值是："+maxNum);
		*/
		int[] arr = {12,56,34,78,33,8,98};
		int maxNum = maxSel(arr);
		System.out.println("数组的最大值是："+maxNum);
		
	}
	//将求最大值的方法提取出来
	public static int maxSel(int[] arr){
		int maxNum=0;
		for(int i=0;i<arr.length;i++){
			if(arr[i]>maxNum){
				maxNum=arr[i];
			}
		}
		return maxNum;
	}
}
```

#  数组的查询操作

```java
public class TestArray05{
	public static void main(String[] args){
		int[] arr = {45,65,78,14,92,83,76};
		// 查询数组对应索引的值
		System.out.println(arr[4]);
		// 查询数组中某个数字对应的索引值
		int index = getIndex(arr,666);
		if(index!=-1){
			System.out.println("索引是："+index);
		}else{
			System.out.println("查无此数");
		}
	}
	// 遍历数组，查询数值对应的索引
	public static int getIndex(int[] arr,int num){
		int index = -1;
		for(int i=0;i<arr.length;i++){
			if(arr[i]==num){
				index = i;
				break;
			}
		}
		return index;
	}
}
```

# 数组的添加操作

```java
import java.util.Scanner;
public class TestArray06{
	public static void main(String[] args){
		// 实现给一个数组中添加一个元素
		// 定义一个数组
		int[] arr = {12,56,78,43,67,12,87};
		// 遍历数组
		System.out.print("添加前的数组为：");
		for(int i=0;i<arr.length;i++){
			if(i!=arr.length-1){
				System.out.print(arr[i]+",");
			}else{
				System.out.print(arr[i]);
			}
		}
		System.out.println();
		// 添加元素
		Scanner sc = new Scanner(System.in);
		System.out.print("请输入索引：");
		int index=sc.nextInt();
		System.out.println("请输入要添加的元素：");
		int ele=sc.nextInt();
		insetEle(arr,index,ele);
		
		// 遍历添加后的数组
		System.out.print("添加后的数组为：");
		for(int i=0;i<arr.length;i++){
			if(i!=arr.length-1){
				System.out.print(arr[i]+",");
			}else{
				System.out.print(arr[i]);
			}
		}
	}
	// 定义处理添加元素的方法
	public static void insetEle(int[] arr,int index,int ele){
		for(int i=arr.length-1;i>index;i--){
			arr[i] = arr[i-1];
		}
		arr[index]=ele;
	}
}
```

# 数组的删除操作

```java
import java.util.Scanner;
import java.util.Arrays;
public class TestArray07{
	public static void main(String[] args){
		// 实现删除数组中的元素
		// 定义数组
		int[] arr={12,3,456,7,42,45,677,12,3,4,5};
		// 遍历删除前的数组
		// Arrays.tostring 方法，将数组变成字符串
		System.out.println("删除前的数组为："+Arrays.toString(arr));
		/*
		for(int i=0;i<arr.length;i++){
			if(i!=arr.length-1){
				System.out.print(arr[i]+",");
			}else{
				System.out.println(arr[i]);
			}
		}
		*/

		// 删除数组中的元素
		Scanner sc = new Scanner(System.in);
		System.out.print("请输入要删除的索引：");
		int index = sc.nextInt();
		delEle(arr,index);
		// 遍历删除后的数组
		System.out.println("删除后的数组为："+Arrays.toString(arr));
		/*
		for(int i=0;i<arr.length;i++){
			if(i!=arr.length-1){
				System.out.print(arr[i]+",");
			}else{
				System.out.println(arr[i]);
			}
		}
		*/
	}
	// 定义删除元素的方法
	public static void delEle(int[] arr,int index){
		for(int i=index;i<arr.length-1;i++){
			arr[i] = arr[i+1];
		}
		arr[arr.length-1] = 0;
	}
}





import java.util.Scanner;
import java.util.Arrays;
public class TestArray08{
	public static void main(String[] args){
		// 实现删除数组中的指定的值
		// 定义数组
		int[] arr={12,3,456,7,42,45,677,12,3,4,5};
		// 遍历删除前的数组
		// Arrays.tostring 方法，将数组变成字符串
		System.out.println("删除前的数组为："+Arrays.toString(arr));
		/*
		for(int i=0;i<arr.length;i++){
			if(i!=arr.length-1){
				System.out.print(arr[i]+",");
			}else{
				System.out.println(arr[i]);
			}
		}
		*/

		// 删除数组中的元素
		Scanner sc = new Scanner(System.in);
		System.out.print("请输入要删除的值：");
		int ele = sc.nextInt();
		// 循环遍历找到数组中要删除至的索引
		int index=-1;
		for(int i=0;i<arr.length;i++){
			if(arr[i]==ele){
				index=i;
			}
		}
		if(index!=-1){
			delEle(arr,index);
		}else{
			System.out.println("查无此数");
		}
		
		// 遍历删除后的数组
		System.out.println("删除后的数组为："+Arrays.toString(arr));
		/*
		for(int i=0;i<arr.length;i++){
			if(i!=arr.length-1){
				System.out.print(arr[i]+",");
			}else{
				System.out.println(arr[i]);
			}
		}
		*/
	}
	// 定义删除元素的方法
	public static void delEle(int[] arr,int index){
		for(int i=index;i<arr.length-1;i++){
			arr[i] = arr[i+1];
		}
		arr[arr.length-1] = 0;
	}
}
```

# Arrays类的使用

```java
import java.util.Arrays;
public class TestArray10{
	public static void main(String[] args){
		int[] arr = {1,2,3,6,5,7};
		// toString
		System.out.println(Arrays.toString(arr));
		
		// sort排序
		Arrays.sort(arr);
		System.out.println("排序后的数组为："+Arrays.toString(arr));
		
		// binarySearch binarySearch是针对有序的数组进行查找，无序的输出查出的索引是错误的，需要使用sort排序
		System.out.println(Arrays.binarySearch(arr,6));
		
		// copyOf 复制数组
		int[] arr1 = Arrays.copyOf(arr,4);
		System.out.println(Arrays.toString(arr1));
	
		// copyOfRange 区间复制
		int[] arr2 = Arrays.copyOfRange(arr,1,4);
		System.out.println(Arrays.toString(arr2));
		
		//equals 比较两个数组中的元素是否相同
		int[] arr3 = {1,2,3,5,6,7};
		System.out.println(Arrays.equals(arr,arr3));
		System.out.println(arr == arr3);
		
		// fill 数组填充
		int[] arr4 = new int[6];
		Arrays.fill(arr4,2);
		System.out.println(Arrays.toString(arr4));
		
		
	}
}
```

# 数组的复制

```java
import java.util.Arrays;
public class TestArray11{
	public static void main(String[] args){
		// System.copyarray 复制数组到另一个数组，共需要传5个参数，分别为源数组，源数组复制的起始位置，目标数组，目标数组的起始位置，复制多少个元素
		int[] arr1 = {1,2,3,4,5,6,7,8,9,10};
		int[] arr2 = new int[10];
		System.arraycopy(arr1,1,arr2,4,4);
		System.out.println(Arrays.toString(arr2));
		
	}
}
```

