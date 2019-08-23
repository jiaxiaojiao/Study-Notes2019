## MySQL查询用户连续登录天数
> 日期使用中用到的函数。

> 来源： https://www.jianshu.com/p/0ecbf2d71577

```sql
select uid
    ,max(days) incessancy_days
    ,min(ot) start_date
    ,max(ot) end_date
from
(
    select uid
        ,@cont_day :=
        (
            case when (@last_uid = uid and DATEDIFF(ot, @last_ot)=1) then
            (@cont_day + 1)
            when (@last_uid = uid and DATEDIFF(ot, @last_ot)<1) then
            (@cont_day + 0)
            else 1
            end
        ) as days
        ,(@cont_ix := (@cont_ix + if(@cont_day = 1, 1, 0))) AS cont_ix
        ,@last_uid := uid
        ,@last_ot := ot ot
    from
    (
        select uid
            ,login_date as ot
        from log
        where login_date >= '2017-01-01'
            and login_date < '2017-07-01'
        order by uid ,login_date
    ) as t1,
    (
        select @last_uid := '',
            @last_ot  := '',
            @cont_ix  := 0,
            @cont_day := 0
    ) as t2
) as t
group by uid

```