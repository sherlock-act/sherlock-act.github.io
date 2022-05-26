# Java的二维数组

- 在java中二维数组，本质上都是以为数组，只是在堆空间中，一个一维数组中每一个索引中存放的是另一个以为数组的内存地址

## 二维数组的定义与遍历

```java
public class TestArray12{
	public static void main(String[] args){
		// 二维数组的定义
		int[][] arr = new int[3][];
		int[] arr1 = {1,2,3};
		// 给索引为0的数组中放入另一个一维数组
		arr[0] = arr1;
		arr[1] = new int[]{4,5,6,7};
		arr[2] = new int[]{8,9,10};
		
		// 二维数组的遍历
		// 方式1:两层普通for循环
		for(int i1=0;i1<arr.length;i1++){
			for(int j1=0;j1<arr[i1].length;j1++){
				System.out.print(arr[i1][j1]+"\t");
			}
			System.out.println();
		}
		
		System.out.println("--------------------------");
		// 方式2:外层for循环，内层增强for循环
		for(int i2=0;i2<arr.length;i2++){
			for(int num1:arr[i2]){
				System.out.print(num1+"\t");
			}
			System.out.println();
		}
		
		System.out.println("--------------------------");
		// 方式3：两层增强for循环
		for(int[] a1:arr){
			for(int num2:a1){
				System.out.print(num2+"\t");
			}
			System.out.println();
		}
		
		System.out.println("--------------------------");
		// 方式4：外层增强for循环，内层普通for循环
		for(int[] a2:arr){
			for(int j3=0;j3<a2.length;j3++){
				System.out.print(a2[j3]+"\t");
			}
			System.out.println();
		}
	}
}
```



