# 模块1：turtle库

[turtle库文档](https://docs.python.org/3/library/turtle.html)

### turtle库简介

> turtle（海龟）库是turtle绘图体系的Python实现。
>
> turtle绘图体系诞生于1969年，主要用于程序设计入门。
>
> turtle库是Python语言的**标准库**之一，是入门级的图形绘制函数库。



### turtle的原理

> 有一只海龟，在窗体正中心，在画布上游走。走过的轨迹形成了绘制的图形。海龟由程序控制，可以变换颜色、改变宽度等。



### turtle基础

#### turtle绘图窗体布局

调用turtle库进行绘画，会在电脑屏幕上新建一个窗口，即这里所说的绘图窗体。

绘图窗体是turtle的一个画布空间，最小单位是像素。

```python
turtle.setup(width, height, startx, starty) #后两个参数可选
```

可以用 `setup()` 函数修改绘图窗体的布局。（若不设置，则默认在屏幕正中）

<img src="assets/turtle-1.jpg" />





示例：

<img src="assets/turtle-2.jpg" />





#### turtle空间坐标体系

##### （一）绝对坐标

以绘图窗体正中为坐标原点（0,0）

```python
turtle.goto(x, y)
```

<img src="assets/turtle-3.jpg" />

示例：

```python
import turtle
turtle.goto(100, 100)
turtle.goto(100, -100)
turtle.goto(-100, -100)
turtle.goto(-100, 100)
turtle.goto(0,0)
```



##### （二）海龟坐标

以海龟前进的方向。海龟头的朝向为前进方向，屁股朝向为后退方向，左手边为左侧方向，右手边为右侧方向。

<img src="assets/turtle-4.jpg" />

```python
#根据半径radius绘制extent角度的弧形
turtle.circle(radius, extent)
#回退
turtle.bk(d)
#前进
turtle.fd(d)
```

<img src="assets/turtle-5.jpg" />

#### turtle角度坐标体系

##### （一）绝对角度

与数学中坐标系的定义一致。

<img src="assets/turtle-6.jpg" />

```python
turtle.seth(angle)
#seth() 改变海龟行进方向，但不行进
#angle为绝对角度
```



##### （二）海龟角度

以海龟头朝向的方向，向左或向右转向相应的角度。

<img src="assets/turtle-7.jpg" />

```python
import turtle
turtle.left(45)
turtle.fd(150)
turtle.right(135)
turtle.fd(300)
turtle.left(135)
turtle.fd(150)
```



#### RGB色彩体系

##### 简介

> R(red) G(green) B(blue) 指红绿蓝三个通道的颜色组合。能覆盖视力所能感知的所有颜色。
>
> RGB每色取值范围 0-255 整数或 0-1 小数。



##### 常用RGB色彩

| 英文名称 | RGB整数值   | RGB小数值      | 中文名称 |
| -------- | ----------- | -------------- | -------- |
| white    | 255,255,255 | 1,1,1          | 白色     |
| yellow   | 255,255,0   | 1,1,0          | 黄色     |
| magenta  | 255,0,255   | 1,0,1          | 洋红     |
| cyan     | 0,255,255   | 0,1,1          | 青色     |
| blue     | 0,0,255     | 0,0,1          | 蓝色     |
| black    | 0,0,0       | 0,0,0          | 黑色     |
| seashell | 255,245,238 | 1,0.96,0.93    | 海贝色   |
| gold     | 255,215,0   | 1,0.84,0       | 金色     |
| pink     | 255,192,203 | 1,0.75,0.80    | 粉红色   |
| brown    | 165,42,42   | 0.65,0.16,0.16 | 棕色     |
| purple   | 160,32,240  | 0.63,0.13,0.94 | 紫色     |
| tomato   | 255,99,71   | 1,0.39,0.28    | 番茄色   |



##### turtle的RGB色彩模式

默认采用小数值，可切换为整数值。

```python
turtle.colormode(mode)
#1.0：小数值模式
#255：整数值模式
```





### turtle程序语法元素

完整示例代码：

```python
import turtle
turtle.setup(650, 350, 200, 200)
turtle.penup()
turtle.fd(-250)
turtle.pendown()
turtle.pensize(25)
turtle.pencolor("purple")
turtle.seth(-40)
for i in range(4):
    turtle.circle(40, 80)
    turtle.circle(-40, 80)
turtle.circle(40, 80/2)
turtle.fd(40)
turtle.circle(16, 180)
turtle.fd(40 * 2/3)
turtle.done()
```



#### 库引用 import

使用 `import` 保留字完成，采用 `<a>.<b>()` 编码风格

```python
#import <库名>

#调用时每句语句都需要写出库名
#<库名>.<函数名>(<函数参数>)
```

示例：

```python
import turtle
turtle.setup(650, 350, 200, 200)
turtle.penup()
```



使用 `from` 和 `import` 保留字共同完成

```python
#from <库名> import <函数名>
#from <库名> import *

#调用时可以直接写函数名
#<函数名>(<函数参数>)
```

> 第一种方法不会出现函数重名问题，第二种方法则会出现。

示例：

```python
from turtle import *
setup(650, 350, 200, 200)
penup()
```



使用 `import` 和 `as` 保留字共同完成，给调用的外联库关联一个更短、更方便自己使用的名字

```python
#import <库名> as <库别名>

#调用时使用库别名
#<库别名>.<函数名>(<函数参数>)
```

示例：

```python
import turtle as t
t.setup(650, 350, 200, 200)
t.penup()
```



#### turtle画笔控制函数

抬起画笔

```python
turtle.penup()
#turtle.pu()
```



落下画笔

```python
turtle.pendown()
#turtle.pd()
```

> 画笔操作后一直有效，一般成对出现。



画笔宽度

```python
#turtle.pensize(width)
#turtle.width(width)
```



画笔颜色

```python
#turtle.pencolor(color)
#color 为颜色字符串或rgb值

#颜色字符串：turtle.pencolor("purple")
#RGB的小数值：turtle.pencolor(0.63,0.13,0.94)
#RGB的元组值：turtle.pencoloe((0.63,0.13,0.94))
```

> 画笔设置后一直有效，直至下次重新设置。



#### turtle运动控制函数

向前行进，走直线

```python
#turtle.forward(d)
#turtle.fd(d)

#行进距离d可以为负数
```



根据半径 radius 绘制 extent 角度的弧形

```python
#turtle.circle(radius, extent = None)

#radius：默认圆心在海龟左侧radius距离的位置
#extent：绘制角度，默认是360度的整圆
```

示例：

<img src="assets/turtle-8.jpg" />



#### turtle方向控制函数

改变行进方向，海龟走角度（绝对角度）

```python
#turtle.setheading(angle)
#turtle.seth(angle)

#angle：行进方向的绝对角度
```

示例：

<img src="assets/turtle-9.jpg" />



控制海龟面对方向（海龟角度）

```python
#turtle.left(angle)
#turtle.right(angle)

#angle：在海龟当前行进方向上旋转的角度
```







