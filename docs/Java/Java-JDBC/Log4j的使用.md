# Log4j日志框架使用

## Log4j的配置文件

- 想要使用Log4j,需要在项目目录下创建一个`lib`文件夹,在文件夹中导入`Log4j`的jar包



- 然后,在`src`目录下创建`log4j.properties`配置文件,需要将配置文件进行配置然后才能正常使用,一般Log4j配置文件内容如下:

```
log4j.rootLogger=error,stdout
## error 代表日志输出的级别，error及以上级别才输出  logfile表示将日志写入到文件，这里可以添加多个参数，添加stdout在控制台输出，用逗号隔开

log4j.appender.stdout=org.apache.log4j.ConsoleAppender
## 上面的代码表示日志输出到控制台
log4j.appender.stdout.Target=System.err
## 上面的代码配置输出的类
log4j.appender.stdout.layout=org.apache.log4j.SimpleLayout
##上面的代码表示输出时的格式的设置
## stdout  这个名称可以修改，但是要保证所有的地方保持一致，这里的配置表示使用控制台输出日志的配置

log4j.appender.logfile=org.apache.log4j.FileAppender
## 上面的代码表示日志输出的类
log4j.appender.logfile.File=d:/msb.log
## 上面一行代码是日志文件地址的配置
log4j.appender.logfile.layout=org.apache.log4j.PatternLayout
## 上面的代码表示输出时格式的类
log4j.appender.logfile.layout.ConversionPattern=%d{yyyy-MM-dd   HH:mm:ss} %l %F %p %m%n
## 上面一行代码是日志输出格式的配置
## logfile  这个名称可以修改，但是要保证所有地方保持一致，这里的配置表示写入到日志文件的配置
```

## Log4j日志的级别

- FATAL：指出现非常严重的错误事件，这些错误可能导致应用程序异常中止
- ERROR：指虽有错误，但仍允许应用程序继续运行
- WARN：指运行环境潜藏着危害
- INFO：指报告信息，这些信息在粗粒度级别上突出显示应用程序的进程
- DEBUG：指细粒度信息事件，对于应用程序的调试是最有用的

## Log4j的日志格式化字符含义

- %p：输出日志信息的优先级，即DEBUG，INFO，WARN，ERROR，FATAL。
- %d：输出日志时间点的日期或时间，默认格式为ISO8601，也可以在其后指定格式，如：%d{yyyy/MM/dd HH:mm:ss,SSS}。
- %r：输出自应用程序启动到输出该log信息耗费的毫秒数。
- %t：输出产生该日志事件的线程名。
- %l：输出日志事件的发生位置，相当于%c.%M(%F:%L)的组合，包括类全名、方法、文件名以及在代码中的行数
- %c：输出日志信息所属的类目，通常就是所在类的全名。
- %M：输出产生日志信息的方法名。
- %F：输出日志消息产生时所在的文件名称。
- %L:：输出代码中的行号。
- %m:：输出代码中指定的具体日志信息。
- %n：输出一个回车换行符，Windows平台为"rn"，Unix平台为"n"。
- %x：输出和当前线程相关联的NDC(嵌套诊断环境)，尤其用到像java servlets这样的多客户多线程的应用中。
- %%：输出一个"%"字符

## Java代码中使用Log4j

```java
package com.shanlei;


import org.apache.log4j.Logger;

/**
 * @author: shanlei
 * @version: 1.0
 */
public class TestLog4j {
    // 这是main方法，实现程序主要逻辑
    public static void main(String[] args) {
        Logger logger = Logger.getLogger(TestLog4j.class);
        // 创建logger对象,注意导包的时候,需要导org.apache.log4j.Logger这个包

        logger.fatal("这是fatal级别：严重错误警告");
        logger.error("这是error级别：错误警告");
        logger.warn("这是warn级别：提醒警告");
        logger.info("这是inroad级别：信息");
        logger.debug("这是debug级别：调试级别");
    }
}
```

