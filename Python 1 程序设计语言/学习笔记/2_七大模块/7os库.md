# 模块7：os库

[os库文档](https://docs.python.org/3/library/os.html)

## os库基本概述

os库是Python**标准库**，包含几百个函数。

os库提供通用的、基本的操作系统交互功能，常用路径操作、进程管理、环境参数等几类。

- 路径操作：os.path子库，处理文件路径及信息
- 进程管理：启动系统中其他程序
- 环境参数：获得系统软硬件信息等环境参数



## 路径操作

os.path子库以path为入口，用于操作和处理文件路径。

```python
import os.path
#import os.path as op
```

| 函数                       | 描述                                            |
| -------------------------- | ----------------------------------------------- |
| os.path.abspath(path)      | 返回path在当前系统中的绝对路径                  |
| os.path.normpath(path)     | 归一化path的表示形式，统一用\\分隔路径          |
| os.path.relpath(path)      | 返回当前程序与文件之间的相对路径                |
| os.path.dirname(path)      | 返回path中的目录名称                            |
| os.path.basename(path)     | 返回path中最后的文件名称                        |
| os.path.join(path, *paths) | 组合path与paths，返回一个路径字符串             |
| os.path.exists(path)       | 判断path对应文件或目录是否存在，返回True或False |
| os.path.isfile(path)       | 判断path对应是否为已存在的文件，返回True或False |
| os.path.isdir(path)        | 判断path对应是否为已存在的目录，返回True或False |
| os.path.getatime(path)     | 返回path对应文件或目录上一次的访问时间。        |
| os.path.getmtime(path)     | 返回path对应文件或目录最近一次的修改时间。      |
| os.path.getctime(path)     | 返回path对应文件或目录的创建时间。              |
| os.path.getsize(path)      | 返回path对应文件的大小，以字节为单位。          |



## 进程管理

```python
#os.system(command)

#执行程序或命令command
#在Windows系统中，返回值为cmd的调用返回信息
```

示例：

```python
import os
os.system("C:\\Windows\\System32\\calc.exe")
```



## 环境参数

### 获取或改变系统环境信息

| 函数           | 说明                   |
| -------------- | ---------------------- |
| os.chdir(path) | 修改当前程序操作的路径 |
| os.getcwd()    | 返回程序的当前路径     |



### 获取操作系统环境信息

| 函数          | 说明                                            |
| ------------- | ----------------------------------------------- |
| os.getlogin() | 获得当前系统登录用户名称                        |
| os.cpu_count  | 获得当前系统的CPU数量                           |
| os.urandom(n) | 获得n个字节长度的随机字符串，通常用于加解密运算 |

