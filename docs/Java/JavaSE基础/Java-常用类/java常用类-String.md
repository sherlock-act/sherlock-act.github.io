# Java常用类-String

- String类在底层其实就是一个char类型的数组，数组里面存的是每一个字符
- String类的常用方法
  - `length`返回字符串的长度，实际上就是底层的数组的长度
  - `isEmpty`判断字符串是否为空，实际上就是底层的数组是否为空
  - `charAt`返回字符串对应下表的字符，实际上就是对底层的数组按照下标进行取值
  - `euqals` 判断字符串是否想等
  - `compareTo` 按字典顺序比较两个字符串
    - 按照两个字符串中较短的那个长度n为准，对两个字符串的每一位进行比较
    - 如果两个字符串的前n为都相等，那么就返回调用方法的字符串长度减去传入参数的字符串长度的值
    - 如果两个字符串前n为中有不相等的，那么就返回第一次不想的的两个字符的Asics码值的差值
  - `substring`对字符串进行截取
    - 如果只传入一个int类型的参数，就表示从传入参数的那一位开始截取，一直到这个字符串的最后一位
    - 如果传入两个int类型的参数，表示从第一个参数的位数开始截取，到第二个参数位置结束， 左边包含，右边不包含
  - `concat`字符串的拼接
  - `replace` 对字符串中的字符进行替换，返回一个新的字符串
  - `split` 对字符串进行分割，返回一个字符串类型的数组
  - `toUpperCase` 将字符串全部变为大写
  - `toLowerCase`,将字符串全部变为小写
  - `trim` 将字符串两头的空格删除掉

```java
public class Test01 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        // String类
        String str = "abc";
        System.out.println(str);

        // 通过构造器创建String类的对象
        // 实际上就是给底层的对象的数组进行赋值
        String s1 = new String();
        String s2 = new String("abc");
        String s3 = new String(new char[]{'a','b','c'});

        //length 返回字符串的长度，实际上就是底层的数组的长度
        System.out.println(str.length());

        // isEmpty 判断字符串是否为空，实际上就是底层的数组是否为空
        System.out.println(s1.isEmpty());
        System.out.println(s2.isEmpty());

        // charAt 返回String对象数组对应下标的字符
        System.out.println(str.charAt(1));

        // euqals 判断字符串是否想等
        System.out.println(str.equals(s3));

        // compareTo 按字典顺序比较两个字符串
        // 按照两个字符串中较短的那个长度n为准，对两个字符串的每一位进行比较
        // 如果两个字符串的前n为都相等，那么就返回调用方法的字符串长度减去传入参数的字符串长度的值
        // 如果两个字符串前n为中有不相等的，那么就返回第一次不想的的两个字符的Asics码值的差值
        String s4 = "abc";
        String s5 = "acc";
        System.out.println(s4.compareTo(s5)); // 结果为-1

        // 对字符串进行截取
        // 如果只传入一个int类型的参数，就表示从传入参数的那一位开始截取，一直到这个字符串的最后一位
        // 如果传入两个int类型的参数，表示从第一个参数的位数开始截取，到第二个参数位置结束， 左边包含，右边不包含
        String s6 = "abcdefghk";
        System.out.println(s6.substring(3));
        System.out.println(s6.substring(3, 6));

        // concat 拼接字符串
        // 将传入的字符串拼接到调用方法的字符串的后面，返回一个新的字符串
        System.out.println(s6.concat("ppppppp"));

        // replace 对字符串中的字符进行替换，返回一个新的字符串
        // 所有满足条件的字符都会被替换
        String s7 = "aaaaaaa";
        System.out.println(s7.replace('a', 'u'));

        // split 对字符串进行分割，返回一个字符串类型的数组
        String s8 = "a-b-c-d-e-f";
        String[] split1 = s8.split("-");
        System.out.println(Arrays.toString(split1)); // [a, b, c, d, e, f]

        // toUpperCase 将字符串全部变为大写
        System.out.println(str.toUpperCase());

        //toLowerCase,将字符串全部变为小写
        String s9 = "ABCDEFGH";
        System.out.println(s9.toLowerCase());

        //trim 将字符串两头的空格删除掉
        String s10 = "    a   b        c     ";
        System.out.println(s10.trim());
    }
}
```

