# Java的异常处理

- 异常就是在程序正常运行中，出现不正常的现象，阻止程序正常运行；

## try-catch 捕获异常

- 使用try-catch，可以对try所包裹的代码块进行异常捕获；
- 如果try中没有异常，那么catch中的代码就不会执行；
- 如果try所包裹的代码执行出现异常，catch就会对异常进行捕获，如果异常类型与catch的异常类型能匹配到，那么久执行catch中的代码；
- 如果catch指定的异常类型与出现的异常类型不匹配，程序依然会直接出现异常报错；
- 捕获异常后，try-catch后面的代码依然可以正常执行；

```java
public class Test01 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        try{// try所包裹的代码块中，如果运行出现异常，就会将异常捕获，然后执行catch代码块的语句
            Scanner sc = new Scanner(System.in);
            System.out.println("两个整数相除，求商");
            System.out.println("请输入第一个数");
            int num1 = sc.nextInt();
            System.out.println("请输入第二个数");
            int num2 = sc.nextInt();
            System.out.println("两个数的商为："+num1/num2);
        }catch(Exception ex){// catch捕获到异常，然后执行代码块中的语句
            System.out.println("输入值非法");
        }
        // 异常捕获后，try catch后面的语句依然可以正常执行
        System.out.println("捕获了异常后，代码依然可以往后执行");
    }
}
```

### catch捕获异常后的处理方式

```java
// 异常处理的几种方法
// 第一种 什么都不写，捕获异常后什么都不处理

// 第二种，进行友好性提示
System.out.println("输入值非法");

// 第三种，打印异常信息
// (1) 调用toString方法，显示异常类名
System.out.println(ex);
System.out.println(ex.toString());
// (2) 使用getMessage方法，打印异常描述信息
System.out.println(ex.getMessage());
// （3） ，打印堆栈信息，即打印完整的异常信息，这种方法最常用
ex.printStackTrace();

// 第四种 抛出异常 即程序默认的处理方式，直接将异常抛出来
throw ex;
```

###   finally

- 在try-catch中如果遇到以下情况，那么后面的代码就不行再执行了
  - throw抛出异常
  - chatch没有正常捕获到异常
  - try中遇到了return
- 但是在try-catch中，如果一定要后面的代码无论如何都要执行的话，那么久需要使用finally
- finally一般是使用在以下场景
  - 关闭数据库资源
  - 关闭IO流资源
  - 关闭socket资源等场景
- 但是也有一句代码可以终止finally的运行
  - System.exit()括号中需要传入一个参数，随便传入 0， 1,2,3,4都可以
  - 这句代码的意思就是停止当前虚拟机的运行

```java
public class Test01 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        try{// try所包裹的代码块中，如果运行出现异常，就会将异常捕获，然后执行catch代码块的语句
            Scanner sc = new Scanner(System.in);
            System.out.println("两个整数相除，求商");
            System.out.println("请输入第一个数");
            int num1 = sc.nextInt();
            System.out.println("请输入第二个数");
            int num2 = sc.nextInt();
            System.out.println("两个数的商为："+num1/num2);
            System.exit(0);// 终止当前虚拟机的运行
            return;
        }catch(InputMismatchException ex){
            throw ex;
        }finally {//  finally中的代码一定会被执行
            System.out.println("finally中的代码无论如何都会执行");
        }
    }
}
```

### 多重catch

- try中出现异常以后，将异常类型跟catch中的类型一次比较
- 一旦异常类型匹配后，后面其他的catch语句就会被忽略了
- 在安排catch语句顺序的时候，一般将特殊异常放在前面，最后将一个兜底的异常放在最后例如Exception
- 可以写多个catch语句，也可以将多个异常并列写在一个catch中，中间用 `|`进行连接。

```java
public class Test02 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        try{// try所包裹的代码块中，如果运行出现异常，就会将异常捕获，然后执行catch代码块的语句
            Scanner sc = new Scanner(System.in);
            System.out.println("两个整数相除，求商");
            System.out.println("请输入第一个数");
            int num1 = sc.nextInt();
            System.out.println("请输入第二个数");
            int num2 = sc.nextInt();
            System.out.println("两个数的商为："+num1/num2);
            System.exit(0);// 终止当前虚拟机的运行
            return;
        }catch(InputMismatchException ex){
            System.out.println("输入的值不是int类型");
        }catch (ArithmeticException ex){
            System.out.println("除数不能为0");
            
        /*
        多个catch，也可以使用catch中使用多个异常类型
        catch(InputMismatchException | ArithmeticException ex){
        	````````
        }
        */
        }catch(Exception ex){
            System.out.println("程序出现异常");
        }finally {//  finally中的代码一定会被执行
            System.out.println("finally中的代码无论如何都会执行");
        }
    }
}
```

### throw和throws的区别

throw 与 throws都是抛出异常，但是他们的应用场景是有区别的，具体区别如下：

- 位置不同
  - throw 的位置是在方法内部
  - throws 的位置在方法的签名处，即方法的声明出
- 内容不同
  - throw 后面接的是异常的对象（可以是检查异常，也可以是运行时异常）
  - throws 后面加的是异常的名称，异常的类型
- 作用不同
  - throw 异常出现的源头，制造异常
  - throws 在方法的声明处，告诉方法的调用者，这个方法中可能出现我声明的异常，然后调用者对异常进行处理

```java
public class Test3 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        // 实现两个出相除，当除数为0的时候，程序出现异常
        // 方法内的检查异常向上抛出，需要调用者处理，可以继续向上抛，也可以直接处理
        try {
            devide();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    public static void devide() throws Exception {
        Scanner sc = new Scanner(System.in);
        System.out.println("两个整数相除，求商");
        System.out.println("请输入第一个数");
        int num1 = sc.nextInt();
        System.out.println("请输入第二个数");
        int num2 = sc.nextInt();
        if(num2 ==0){
            // 制造运行时异常
            // throw new RuntimeException();

            // 检查异常，可以在方法内部自己处理：如下
            /*
            try {
                throw new Exception();
            } catch (Exception e) {
                e.printStackTrace();
            }
             */

            // 检查异常，也可以直接像上抛出异常，让调用者去处理异常
            // 这种方法 会在方法后面加上throw 加异常名称
            throw new Exception();
        }else {
            System.out.println("两个数的商为：" + num1 / num2);
        }
    }
}
```

### 自定义异常

- 自动以异常可以继承自运行时异常，也可以继承自检查异常
- 继承自运行时异常，不用额外处理
- 检查异常，需要try-catch进行捕获或者throws向上抛

```java
public class MyException extends RuntimeException {
    static final long serialVersionUID = -70348971;

    public MyException() {
    }

    public MyException(String msg){
        super(msg);
    }
}
```



