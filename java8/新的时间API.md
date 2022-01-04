新的时间API

java.time包

Temporal接口





LocalDate

- final class
- 用于表示日期

常用的方法

```
// 创建LocalDate实例
LocalDate date = LocalDate.of(2022,1,4);

// 获取当前日日期
LocalDate today = LocalDate.now();

date.getYear();
date.getMonth();
date.getDayOfYear();
date.getDayOfMonth();
date.getDayOfWeek();
date.lengthOfMonth();
date.isLeapYear();
date.get(ChronoField.YEAR);
date.get(ChronoField.MONTH_OF_YEAR);
```

LocalDate

- final class
- 用于表示时间

```
LocalTime time = LocalTime.of(23,40,33);
time.getHour();
time.getMinute();
time.getSecond();
```

字符串转日期

```
LocalDate.parse("2022-10-4");
LocalDate.parse("23:42:00");
```

LocalDateTime

```
LocalDate date = LocalDate.of(2022,1,4);
LocalTime time = LocalTime.of(23,40,33);
LocalDateTime dt = LocalDateTime.of(date,time);
dt = date.atTime(time);
LocalDate date1 = dt.toLocalDate();
LocalTime localTime = dt.toLocalTime();
```

Instant

- 表示机器日期和时间格式
- 以Unix元年时间开始所经历的秒数开始计算，

```
Instant now = Instant.now();
Instant instant = Instant.ofEpochSecond(2);
```



duration 

- 持续时间
- 以秒和纳秒衡量时间长短
- 不可变对象



period

- 一段时间
- 以年、月、日、衡量时间长短
- 不可变对象





如何创建可修改版本的日期



temporalAdjuster方法





打印输出解析日期对象

DateTimeFormatter

以一定格式创建代表特定日期或时间的字符串

线程安全

ofPattern方法

Locale





DateTimeFormatterBuilder

