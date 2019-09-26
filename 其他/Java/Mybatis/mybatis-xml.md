# XML中的大于小于等于

> 有两种方法

```text
第一种方法：
    用转义字符把">"和"<"替换掉。
    
XML转义字符
<      &lt;      小于
<=     &lt;=     小于等于
>      &gt;      大于
>=     &gt;=     大于等于
&      &amp;     和
'      &apos;    单引号
"      &quot;    双引号

例如：
create_date_time &gt;= #{startTime} and create_date_time &lt;= #{endTime}


第二种写法：
    因为这个是xml格式的，所以不允许出现类似">"这样的字符，但是可以使用<![CDATA[ ]]>符号进行说明，将此类符号不进行解析。

大于等于      <![CDATA[ >= ]]>
小于等于      <![CDATA[ <= ]]>

例如：
create_date_time <![CDATA[ >= ]]> #{startTime} and create_date_time <![CDATA[ <= ]]> #{endTime}
```