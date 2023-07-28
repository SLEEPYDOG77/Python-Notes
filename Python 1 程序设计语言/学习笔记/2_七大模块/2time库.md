# 模块2：time库

[time库文档](https://docs.python.org/3/library/time.html)

## time库概述

time库是Python中处理时间的**标准库**。

```python
import time
#time.<b>()
```

- 计算机时间的表达
- 提供获取系统时间并格式化输出功能
- 提供系统级精确计时功能，**用于程序性能分析**



| 类别       | 函数                        |
| ---------- | --------------------------- |
| 时间获取   | time() / ctime() / gmtime() |
| 时间格式化 | strftime() / strptime()     |
| 程序计时   | sleep() / perf_counter()    |



## 时间获取

#### time()

> 获取当前时间戳，即计算机内部时间值，浮点数

```python
import time
time.time()
```

输出结果

```
1610434612.9377909
```



#### ctime()

> 获取当前时间并以易读方式表示，返回字符串

```python
import time
time.ctime()
```

输出结果：

```
'Tue Jan 12 14:57:21 2021'
```



#### gmtime()

> 获取当前时间，表示为计算机可处理的时间格式

```python
import time
time.gmtime()
```

输出结果：

```
time.struct_time(tm_year=2021, tm_mon=1, tm_mday=12, tm_hour=6, tm_min=57, tm_sec=42, tm_wday=1, tm_yday=12, tm_isdst=0)
```



## 时间格式化

将时间以合理的方式展示出来

- 格式化：类似字符串格式化，需要有展示模板
- 展示模板：由特定的格式化控制符组成



#### strftime()

```python
#time.strftime(tpl, ts)

#tpl：格式化模板字符串，用来定义输出效果
#ts：计算机内部时间类型变量
```

示例：

```python
import time
t = time.gmtime()
time.strftime("%Y-%m-%d %H:%M:%S" , t)
```

输出结果：

```python
'2021-01-12 07:01:08'
```



##### 格式化控制符

| 格式化字符串 | 日期/时间说明 | 值范围和实例                  |
| ------------ | ------------- | ----------------------------- |
| %Y           | 年份          | 0000 - 9999 如：1999          |
| %m           | 月份          | 01 - 12 如：7                 |
| %B           | 月份名称      | January - December 如：April  |
| %b           | 月份名称缩写  | Jan - Dec 如：Apr             |
| %d           | 日期          | 01 - 31 如：25                |
| %A           | 星期          | Monday - Sunday 如：Wednesday |
| %a           | 星期缩写      | Mon - Sun 如：Wed             |
| %H           | 小时（24h制） | 00 - 23 如：12                |
| %l           | 小时（12h制） | 01 - 12 如：7                 |
| %p           | 上/下午       | AM/PM 如：AM                  |
| %M           | 分钟          | 00 - 59 如：26                |
| %S           | 秒            | 00 - 59 如：26                |



#### strptime()

```python
#strptime(str, tpl)

#str：字符串形式的时间值
#tpl：格式化模板字符串，用来定义输入效果
```

示例：

```python
import time
timeStr = '2021-01-12 07:01:08'
time.strptime(timeStr, "%Y-%m-%d %H:%M:%S")
```

输出结果：

```python
time.struct_time(tm_year=2021, tm_mon=1, tm_mday=12, tm_hour=7, tm_min=1, tm_sec=8, tm_wday=1, tm_yday=12, tm_isdst=-1)
```



## 程序计时

程序计时指测试起止动作所经历时间的过程。

- 测量时间：perf_counter()
- 产生时间：sleep()



#### perf_counter()

返回一个CPU级别的精确时间计数值，单位为秒

> 由于这个计数值起点不确定，连续调用差值才有意义。



```python
import time
start = time.perf_counter()
end = time.perf_counter()
end - start
#13.3894754
```



#### sleep()

```python
import time
sleep(s)
#s：拟休眠的时间，单位是秒，可以是浮点数
```

示例：

```python
import time
def wait():
    time.sleep(3.3)
    
wait()
#程序将等待3.3秒后再退出
```

