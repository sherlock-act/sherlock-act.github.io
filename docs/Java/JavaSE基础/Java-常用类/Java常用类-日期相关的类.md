# java常用类-日期相关的类

## java.util.Date

```java
public class Test01 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        Date d = new Date();
        System.out.println(d);// Sun Dec 20 16:51:08 CST 2020
        System.out.println(d.toString());// Sun Dec 20 16:51:08 CST 2020
        System.out.println(d.toGMTString());//20 Dec 2020 08:51:08 GMT // 本初子午线的时间，方法中加了一个横线，意思是过期方法，过时方法，现在不建议使用
        System.out.println(d.toLocaleString()); // 2020-12-20 16:51:08
        System.out.println(d.getYear());// 120 这个获取的年份是当前年份减去1900的结果
        System.out.println(d.getMonth());// 11 这个月份是0至11之间，所以12月获取的结果是11
        System.out.println(d.getTime());// 1608454657031 时间戳 表示自1970年1月1日00:00:00 GMT 以来的毫秒数
        System.out.println(System.currentTimeMillis());// 1608454657095  这个方法与Date的getTime方法类似，都是返回时间戳
        long startTime = System.currentTimeMillis();
        for (int i = 0; i < 10000; i++) {
            System.out.println(i);
        }
        long endTime = System.currentTimeMillis();
        System.out.println(endTime - startTime);
    }
}
```

## java.sql.Date

```java
public class Test02 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        // java.sql.Date
        Date d = new Date(1608454657031L);
        System.out.println(d);

        // java.sql.Date 与 java.util.Date相互转换

        // util.Date 转 sql.Date
        java.util.Date date = new Date(1608454657031L);
        // 向下转型
        Date Date1 = (Date)date;
        // 创建新对象
        Date Date2 = new Date(date.getTime());

        // sql 转 util
        java.util.Date date3 = d;


        // String 转sql.Date
        Date date4 = Date.valueOf("2020-12-15");
    }
}
```

## SimpleDateFormat

- 定义日期时间的格式，可以转换String与Date数据类型

```java
public class Test04 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        // 日期转换
        // 定义格式化的标准
        DateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

        //String --> Date
        try {
            Date d = df.parse("2020-12-12 23:12:13");
            System.out.println(d); // Sat Dec 12 23:12:13 CST 2020
        } catch (ParseException e) {
            e.printStackTrace();
        }

        //Date --> String
        String format = df.format(new Date());
        System.out.println(format); // 2020-12-20 23:11:00
    }

}
```

## Calendar

```java
public class Test06 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        // calendar 是一个抽象类，不能创建对象
        // GregorianCalendar 是 calendarde 的子类
        Calendar cal = new GregorianCalendar();
        Calendar cal2 = Calendar.getInstance();
        System.out.println(cal);
        System.out.println("*****************************");
        /*
        java.util.GregorianCalendar[time=1608476949023,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",offset=28800000,dstSavings=0,useDaylight=false,transitions=31,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=2020,MONTH=11,WEEK_OF_YEAR=52,WEEK_OF_MONTH=4,DAY_OF_MONTH=20,DAY_OF_YEAR=355,DAY_OF_WEEK=1,DAY_OF_WEEK_IN_MONTH=3,AM_PM=1,HOUR=11,HOUR_OF_DAY=23,MINUTE=9,SECOND=9,MILLISECOND=23,ZONE_OFFSET=28800000,DST_OFFSET=0]
         */

        //常用的方法
        // 获取日期信息
        System.out.println(cal.get(Calendar.YEAR));
        System.out.println(cal.get(Calendar.MONTH));
        System.out.println(cal.get(Calendar.DATE));
        System.out.println(cal.get(Calendar.DAY_OF_MONTH));
        System.out.println("*****************************");
        /*
        2020
        11
        20
        20
         */

        //获取当月最大与最小天数
        System.out.println(cal.getActualMaximum(Calendar.DATE));
        System.out.println(cal.getActualMinimum(Calendar.DATE));
        System.out.println("*****************************");
        /*
        31
        1
         */

        // set方法
        cal.set(Calendar.YEAR,1990);
        cal.set(Calendar.MONTH,3);
        cal.set(Calendar.DATE,16);
        System.out.println(cal);
        System.out.println("*****************************");
        /*
        java.util.GregorianCalendar[time=?,areFieldsSet=false,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",offset=28800000,dstSavings=0,useDaylight=false,transitions=31,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=1990,MONTH=3,WEEK_OF_YEAR=52,WEEK_OF_MONTH=4,DAY_OF_MONTH=16,DAY_OF_YEAR=355,DAY_OF_WEEK=1,DAY_OF_WEEK_IN_MONTH=3,AM_PM=1,HOUR=11,HOUR_OF_DAY=23,MINUTE=9,SECOND=9,MILLISECOND=23,ZONE_OFFSET=28800000,DST_OFFSET=0]
         */

        // String --> calender
        // String --> java.sql.Date
        java.sql.Date date = java.sql.Date.valueOf("2020-7-29");
        // java.sql.Date --> calender
        cal.setTime(date);
        System.out.println(cal);
        System.out.println("*****************************");
        /*
        java.util.GregorianCalendar[time=1595952000000,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",offset=28800000,dstSavings=0,useDaylight=false,transitions=31,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=2020,MONTH=6,WEEK_OF_YEAR=31,WEEK_OF_MONTH=5,DAY_OF_MONTH=29,DAY_OF_YEAR=211,DAY_OF_WEEK=4,DAY_OF_WEEK_IN_MONTH=5,AM_PM=0,HOUR=0,HOUR_OF_DAY=0,MINUTE=0,SECOND=0,MILLISECOND=0,ZONE_OFFSET=28800000,DST_OFFSET=0]
         */
    }
}
```

## LocalDate / LocalTime / LocalDateTime

```java
public class Test10 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        // 实例化对象
        // now方法，获取当前的日期，时间，日期+时间
        LocalDate localDate = LocalDate.now();
        LocalTime localTime = LocalTime.now();
        LocalDateTime localDateTime = LocalDateTime.now();

        System.out.println(localDate);
        System.out.println(localTime);
        System.out.println(localDateTime);
        System.out.println("*******************************");
        /*
        2020-12-20
        23:05:37.623
        2020-12-20T23:05:37.623
         */

        // of方法 设置指定的日期，时间，日期+时间
        LocalDate dateOf = LocalDate.of(2010, 5, 6);
        LocalTime timeOf = LocalTime.of(12, 45, 12);
        LocalDateTime dateTimrOf = LocalDateTime.of(1990, 5, 7, 13, 42, 56);
        System.out.println(dateOf);
        System.out.println(timeOf);
        System.out.println(dateTimrOf);
        System.out.println("*******************************");
        /*
        2010-05-06
        12:45:12
        1990-05-07T13:42:56
         */

        // get方法
        System.out.println(localDateTime.getYear());
        System.out.println(localDateTime.getMonth());
        System.out.println(localDateTime.getMonthValue());
        System.out.println(localDateTime.getDayOfMonth());
        System.out.println(localDateTime.getDayOfWeek());
        System.out.println(localDateTime.getHour());
        System.out.println(localDateTime.getMinute());
        System.out.println(localDateTime.getSecond());
        System.out.println("*******************************");
        /*
        2020
        DECEMBER
        12
        20
        SUNDAY
        23
        5
        37
         */

        //with方法，类似与calendar中的set方法 with方法相当于重新创建了一个对象，不会对原对象做更改
        LocalDateTime localDateTime2 = localDateTime.withMonth(8);
        System.out.println(localDateTime);
        System.out.println(localDateTime2);
        System.out.println("*******************************");
        /*
        2020-12-20T23:05:37.623
        2020-08-20T23:05:37.623
         */

        // 日期的加减操作 会创建新对象，原对象不会有更改
        LocalDateTime localDateTime3 = localDateTime.plusMonths(4);
        System.out.println(localDateTime);
        System.out.println(localDateTime3);
        LocalDateTime localDateTime4 = localDateTime.minusMonths(5);
        System.out.println(localDateTime);
        System.out.println(localDateTime4);

        /*
        2020-12-20T23:05:37.623
        2021-04-20T23:05:37.623
        2020-12-20T23:05:37.623
        2020-07-20T23:05:37.623
        */
    }
}
```

## DateTimeFormatter

- 对LocalDateTime / LocalDate / LocalTime 对象进行对象与字符串质检的转换

```java
public class Test11 {
    // 这是main方法，是实现程序主要逻辑
    public static void main(String[] args) {
        //格式化类： DateTimeFormatter

        // 方式一: ISO_LOCAL_DATE_TIME/ ISO_LOCAL_DATE / ISO_LOCAL_TIME
        // df1 可以完成LocalDateTime和String之间的转换
        DateTimeFormatter df1 = DateTimeFormatter.ISO_LOCAL_DATE_TIME;
        LocalDateTime now = LocalDateTime.now();
        // LocalDateTime --> String
        String str1 = df1.format(now);
        System.out.println(str1); //2020-12-20T23:22:40.952
        // String --> LocalDateTime
        TemporalAccessor parse = df1.parse("2020-12-20T23:22:40.952");
        System.out.println(parse); // {},ISO resolved to 2020-12-20T23:22:40.952

        // 方式二：ofLocalizedDateTime / ofLocalizedDate / ofLocalizedTime
        //参数 FormatStyle.LONG / FormatStyle.MEDIUM / FormatStyle.SHORT
        // FormatStyle.LONG: 2020年12月20日 下午11时28分21秒
        // FormatStyle.MEDIUM:2020-12-20 23:29:01
        // FormatStyle.SHORT: 20-12-20 下午11:29
        DateTimeFormatter df2 = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.SHORT);
        // LocalDateTime --> String
        String str2 = df2.format(now);
        System.out.println(str2);

        // String --> LocalDateTime  parse中的字符串格式也必须与定义的参数的格式相同
        TemporalAccessor parse1 = df2.parse("20-12-20 下午11:29");
        System.out.println(parse1); // {},ISO resolved to 2020-12-20T23:29

        // 方式三：自定义格式，比如ofPattern("yyyy-MM-dd hh:mm:ss")
        DateTimeFormatter df3 = DateTimeFormatter.ofPattern("yyyy-MM-dd hh:mm:ss");
        // LocalDateTime --> String
        String str3 = df3.format(now);
        System.out.println(str3);//2020-12-20 11:34:57
        // String --> LocalDateTime
        TemporalAccessor parse2 = df3.parse("2020-12-20 11:34:57");
        System.out.println(parse2);//{MinuteOfHour=34, MilliOfSecond=0, HourOfAmPm=11, MicroOfSecond=0, SecondOfMinute=57, NanoOfSecond=0},ISO resolved to 2020-12-20
    }
}
```

