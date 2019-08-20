# MySQL 时间

### 时间戳函数

```sql
now()    -- 当前的日期和时间
curdate()    -- 当前的日期
curtime()    -- 当前的时间
current_time()    -- 当前时间
current_timestamp()    -- 当前时间戳
localtime()

```


### 计算函数
```text
date_sub() 函数 从日期减去指定的时间间隔
语法：
    DATE_SUB(date,INTERVAL expr type)

date_add() 函数 从日期加上指定的时间间隔
语法：
    DATE_ADD(date,INTERVAL expr type)

datediff(date1,date2) 函数 两个日期相减 date1 - date2，返回天数
timediff(time1,time2) 函数 两个日期相减 time1 - time2，返回 time 差值

    
date 参数：合法的日期表达式
expr 参数：时间间隔
type 参数：时间间隔类型

```

type 值 | 描述
---|---
MICROSECOND | 
SECOND | 
MINUTE | 
HOUR | 
DAY | 
WEEK | 
MONTH | 
QUARTER | 
YEAR | 
SECOND_MICROSECOND | 
MINUTE_MICROSECOND | 
MINUTE_SECOND | 
HOUR_MICROSECOND | 
HOUR_SECOND | 
HOUR_MINUTE | 
DAY_MICROSECOND | 
DAY_SECOND | 
DAY_MINUTE | 
DAY_HOUR | 
YEAR_MONTH | 


```sql
-- 例1： 前一天
DATE_SUB(CURDATE(),INTERVAL 1 DAY)

-- 例2： 前一天 的年份
YEAR(DATE_SUB(CURDATE(),INTERVAL 1 DAY))

-- 例3： 后一天
DATE_SUB(CURDATE(),INTERVAL -1 DAY)

```


### Extract（选取） 函数

```text
1. 选取日期时间的各个部分：日期、时间、年、季度、月、日、小时、分钟、秒、微秒

set @dt = '2008-09-10 07:15:30.123456';

select date(@dt);        -- 2008-09-10
select time(@dt);        -- 07:15:30.123456
select year(@dt);        -- 2008
select quarter(@dt);     -- 3
select month(@dt);       -- 9
select week(@dt);        -- 36
select day(@dt);         -- 10
select hour(@dt);        -- 7
select minute(@dt);      -- 15
select second(@dt);      -- 30
select microsecond(@dt); -- 123456


2. Extract() 函数，实现
set @dt = '2008-09-10 07:15:30.123456';

select extract(year                from @dt); -- 2008
select extract(quarter             from @dt); -- 3
select extract(month               from @dt); -- 9
select extract(week                from @dt); -- 36
select extract(day                 from @dt); -- 10
select extract(hour                from @dt); -- 7
select extract(minute              from @dt); -- 15
select extract(second              from @dt); -- 30
select extract(microsecond         from @dt); -- 123456

select extract(year_month          from @dt); -- 200809
select extract(day_hour            from @dt); -- 1007
select extract(day_minute          from @dt); -- 100715
select extract(day_second          from @dt); -- 10071530
select extract(day_microsecond     from @dt); -- 10071530123456
select extract(hour_minute         from @dt); --    715
select extract(hour_second         from @dt); --    71530
select extract(hour_microsecond    from @dt); --    71530123456
select extract(minute_second       from @dt); --      1530
select extract(minute_microsecond  from @dt); --      1530123456
select extract(second_microsecond  from @dt); --        30123456


3. MySQL dayof... 函数：dayofweek(), dayofmonth(), dayofyear()
   
分别返回日期参数，在一周、一月、一年中的位置。

set @dt = '2008-08-08';

select dayofweek(@dt);   -- 6
select dayofmonth(@dt);  -- 8
select dayofyear(@dt);   -- 221

日期 '2008-08-08' 是一周中的第 6 天（1 = Sunday, 2 = Monday, ..., 7 = Saturday）；一月中的第 8 天；一年中的第 221 天。


4. MySQL week... 函数：week(), weekofyear(), dayofweek(), weekday(), yearweek()

set @dt = '2008-08-08';

select week(@dt);        -- 31
select week(@dt,3);      -- 32
select weekofyear(@dt);  -- 32

select dayofweek(@dt);   -- 6
select weekday(@dt);     -- 4

select yearweek(@dt);    -- 200831

MySQL week() 函数，可以有两个参数，具体可看手册。 weekofyear() 和 week() 一样，都是计算“某天”是位于一年中的第几周。 weekofyear(@dt) 等价于 week(@dt,3)。

MySQL weekday() 函数和 dayofweek() 类似，都是返回“某天”在一周中的位置。不同点在于参考的标准， weekday：(0 = Monday, 1 = Tuesday, ..., 6 = Sunday)； dayofweek：（1 = Sunday, 2 = Monday, ..., 7 = Saturday）

MySQL yearweek() 函数，返回 year(2008) + week 位置(31)。


5. MySQL 返回星期和月份名称函数：dayname(), monthname()

set @dt = '2008-08-08';

select dayname(@dt);     -- Friday
select monthname(@dt);   -- August


6. MySQL last_day() 函数：返回月份中的最后一天。

select last_day('2008-02-01');  -- 2008-02-29
select last_day('2008-08-08');  -- 2008-08-31

MySQL last_day() 函数非常有用，比如我想得到当前月份中有多少天，可以这样来计算：

mysql> select now(), day(last_day(now())) as days;

```

### 转换函数
```text
time_to_sec(time)
sec_to_time(seconds)

to_days(date)
from_days(days)

str_to_date(str, format)

date_format(date,format)
time_format(time,format)

get_format()
语法：
    get_format(date|time|datetime, 'eur'|'usa'|'jis'|'iso'|'internal')

makdedate(year,dayofyear)
maketime(hour,minute,second)



```

#### （Unix 时间戳、日期）转换函数
```text
unix_timestamp(),
unix_timestamp(date),
from_unixtime(unix_timestamp),
from_unixtime(unix_timestamp,format)

```
#### 时间戳（timestamp）转换、增、减函数
```text
timestamp(date)
timestamp(dt,time)
timestampadd(unit,interval,datetime_expr)    -- 类似于 date_add()
timestampdiff(unit,datetime_expr1,datetime_expr2)

```