# Java-File类

## 对文件进行操作

- File类对文件进行操作

```java
public class Test01 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) throws IOException {
        File f = new File("test.txt");
        // f.exists 判断文件是否存在
        if(!f.exists()){
            // f.createNewFile 创建新的文件
            f.createNewFile();
        }
        //常用方法
        System.out.println("文件是否可读："+f.canRead());
        System.out.println("文件是否可写："+f.canWrite());
        System.out.println("文件名称："+f.getName());
        System.out.println("上级目录名称："+f.getParent());
        System.out.println("是否是目录："+f.isDirectory());
        System.out.println("是否是文件："+f.isFile());
        System.out.println("是否隐藏："+f.isHidden());
        System.out.println("文件大小："+f.length());

        // 路径相关方法
        // 获取文件绝对路径
        System.out.println("绝对路径："+f.getAbsolutePath());
        System.out.println("绝对路径："+f.getAbsoluteFile());
        // 获取文件相对路径
        System.out.println("相对路径："+f.getPath());
        System.out.println("相对路径："+f/*.toString()*/);
    }
}
```

## 对目录进行操作

- File类对目录进行操作

```java
package com.shanlei.TestFile;

import java.io.File;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class Teso02 {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        File f = new File("E:\\Study\\java_train_code\\JavaSE基础");
        // 创建单层目录
        //f.mkdir();
        File f2 = new File("E:\\Study\\java_train_code\\JavaSE基础\\test\\a\\b\\c");
        // 创建多层目录
        //f2.mkdirs();

        //常用方法
        System.out.println("目录是否可读："+f.canRead());
        System.out.println("目录是否可写："+f.canWrite());
        System.out.println("目录名称："+f.getName());
        System.out.println("上级目录名称："+f.getParent());
        System.out.println("是否是目录："+f.isDirectory());
        System.out.println("是否是文件："+f.isFile());
        System.out.println("是否隐藏："+f.isHidden());
        System.out.println("目录大小："+f.length());

        // 路径相关方法
        // 获取文件绝对路径
        System.out.println("绝对路径："+f.getAbsolutePath());
        System.out.println("绝对路径："+f.getAbsoluteFile());
        // 获取文件相对路径
        System.out.println("相对路径："+f.getPath());
        System.out.println("相对路径："+f/*.toString()*/);
        // delete删除文件夹 只会删除一层，且为空的文件夹
        //f2.delete();

        // f.list 获取目录下所有的子目录与文件的名字的数组
        String[] list = f.list();
        for(String s:list){
            System.out.println(s);
        }

        // f.listFiles() 获取目录下所有的子目录与文件的File对象的数组
        File[] file = f.listFiles();
        for(File f3:file){
            System.out.println(f3.getName()+","+f3.getPath());
        }
    }
}

```

