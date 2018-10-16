---
title: Python速成手册
tags: Server
categories: Web
---

Python诞生于20世纪90年代初，由荷兰人Guido van Rossum开发完成，是一款非常简洁易读的解释型脚本语言；擅长于科学计算与图形处理，传统的计算机视觉库[OpenCV](https://opencv.org/)、三维可视化库[VTK](https://www.vtk.org/)、医学图像处理库[ITK](https://itk.org/)都提供了Python调用接口，Python也原生提供了[NumPy](http://www.numpy.org/)、[SciPy](https://www.scipy.org/)、[matplotlib](https://matplotlib.org/)等强大的科学计算扩展库。Web开发方面，Python也提供有[Django](https://www.djangoproject.com/)、[Tornado](http://www.tornadoweb.org/en/stable/)两款常用的Web开发框架。总而言之，得益于强大的开源社区支持，Python已经成为一门功能丰富的胶水语言。

![](python/logo.png)

本文的示例代码基于目前最新的[Python 3.6.5](https://www.python.org/downloads/)版本，在简单介绍相关语法，以及[pip](https://pypi.org/project/pip/)、[virtualenv](https://virtualenv.pypa.io/en/stable/)等扩展库的使用之后，将会最终完成一个基于Django的在线图片相似度比较程序。本文涉及的代码和Markdown都已经上传至笔者的[Github](https://github.com/uinika/python-quick-guide)，需要的朋友可以直接进行克隆，如果有任何建议或发现缪误请提交issue。

<!-- more -->

## Hello World

Python运行环境安装非常方便，Windows操作系统下直接前往[Python官网](https://python.org)下载安装包（*注意添加环境变量*），使用Debian软件包格式的Linux操作系统可以通过如下命令安装：

```bash
➜  sudo apt install python3
```

笔者的Linux开发环境下，同时存在`Python 3.6.5`和`Python 2.7.15`两个版本，因此Z-shell命令行中运行`Hello World`程序时，需要显式输入`python3`，以指定操作系统打开`Python 3.6.5`运行环境。

```bash
➜  / python3
Python 3.6.5 (default, Apr  1 2018, 05:46:30) 
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> print("Hello World!")
Hello World!
```

> 代码执行完毕后，可以通过按下`CTRL + D`或者输入`exit()`退出Python运行环境。

当然，也可以单独将`print("Hello World!")`保存到一个独立的`test.py`代码文件，然后在命令行当中直接开始运行。

```bash
➜  1-hello-world python3 test1.py
Hello World!
```

默认情况下，Python源代码是以`UTF-8`格式进行编码的，但可以通过向源文件头部添加如下声明来指定编码格式。

```py
# -*- coding: utf-8 -*-
```

可以在`.py`脚本文件的头部手动添加Python解释器的路径，从而在Linux系统可以方便的通过`./test1.py`执行该脚本，避免`python3 test1.py`写法的繁琐。

```
#!/usr/bin/python3
```

Python使用缩进来表示代码块，相同代码块的语句必须包含相同的缩进空格数。

```py
# -*- coding: utf-8 -*-
number = 2018
if number > 2020:
    print(number)
print(number)
```

代码将只会执行最后的`print`语句，运行结果如下：

```bash
➜  1-hello-world git:(master) ✗ python3 test2.py
2018
```

## 变量

Python是弱类型语言，因此声明变量时不需要指定数据类型，现在修改上一步的例子，声明一个`infomation`变量然后输出：

```py
infomation = "Hello World!"
print(infomation)
```

执行结果如下：

```bash
➜  2-Variable git:(master) ✗ python3 test1.py
Hello World!
```

相对C、Go、Java等强类型语言，Python的语法结构更为松散，但是变量的命名依然需要遵循以下规则：

1. 变量名只能包含字母、数字、下划线，但不能以数字开头，例如`infomation_1`是合法的变量声明，但是`1_infomation`则属于非法。
2. 变量名不能包含空格，不过可以使用下划线来分隔单词，例如``print_something``是合法的，但是`print something`属于非法。
3. 不能使用Python关键字、函数名称作为变量名，例如`lambda`、`yield`、`raise`、`def`、`nonlocal`、`elif`、`assert`、`except`、`pass`、`with`。
4. 建议使用小写字母作为变量名，并且谨慎使用小写字母`l`和大写字母`O`，因为两者很容易被代码阅读者混淆为数字`1`和`0`。
5. 变量命名尽量见文知意，避免过度的缩写，例如`person_name`明显比`person_n`更加易读。

熟悉了变量命名规则之后，进一步扩展上面的程序，对变量`infomation`重新进行赋值然后打印输出：

```py
infomation = "Hello World!"
print(infomation)

infomation = "Hello Hank!"
print(infomation)
```

执行后将会输出两次打印结果：

```bash
➜  2-Variable git:(master) ✗ python3 test2.py
Hello World!
Hello Hank!
```

**traceback**（*回溯,追踪*）是Python语法解析器提供给开发人员的代码错误提示信息，可以更加直观的定位错误发生的代码位置。

```bash
➜  2-Variable git:(master) ✗ python test3.py
Traceback (most recent call last):  File "test3.py", line 2, in <module>
    print(deom)NameError: name 'deom' is not defined
```

## 注释

python当中可以使用`#`声明一个**单行注释**。

```py
# Comment
print("使用井号的单行注释；")
```

或者使用`3`个单引号`'''`声明一个**多行注释**。

```py
'''
First Comment
Second Comment
'''
print("使用3个单引号声明的多行注释；")
```

也可以使用`3`个双引号`"""`声明一个**多行注释**。

```py
"""
First Comment
Second Comment
"""
print("使用3个双引号声明的多行注释；")
```

## 数据类型

Python是弱类型语言，使用前不需要专门声明，赋值之后变量即被创建。Python一共拥有5种标准的数据类型：**数值**（*Number*）、**字符串**（*String*）、**列表**[*List*]、**元组**（*Tuple*）、**字典**{*Dictionary*}。

Python这5种标准数据类型除了通过字面量方式声明之外，还可以通过构造函数`int()`、`float()`、`complex()`、`str()`、`list()`、`tuple()`、`dict()`进行声明。

Python当中除了这5种标准数据类型之外，还有二进制序列类型（`bytes`, `bytearray`, `memoryview`）、集合类型（`set`, `frozenset`）等衍生的数据类型，本文这里并不将其作为基本数据类型进行介绍，开发人员可以结合官方文档的[《internal-objects》](https://docs.python.org/3.6/library/stdtypes.html#internal-objects)章节按需进行查阅。

### 数值 Number

由于Python非常适合于科学计算用途，因此对于数值类型方面内容的讲解篇幅相对较大。Python的数值类型分为**整型**（*精度不限*）、**浮点类型**（*底层使用C语言的双精度浮点类型实现*）、**复数类型**（*包含实部和虚部*）三种，其中**布尔类型**是作为整型的子类型出现。

当前硬件设备对Python浮点数精度的相关支持信息，可以通过如下代码进行查看。

```py
import sys
print(sys.float_info)
```

上述代码在笔者的64位Linux系统上执行的结果如下：

```py
sys.float_info(max=1.7976931348623157e+308, max_exp=1024, max_10_exp=308, min=2.2250738585072014e-308, min_exp=-1021, min_10_exp=-307, dig=15, mant_dig=53, epsilon=2.220446049250313e-16, radix=2, rounds=1)
```

全部数值类型都支持的运算符：

| 操作 | 结果 | 示例 |
|:------|:-------|:-----|
| `x + y`  | `x`与`y`的和 | `3 + 2`，结果为`5`。 |
| `x - y`  | `x`与`y`的差 | `5 - 1`，结果为`4`。 |
| `x * y`  | `x`与`y`的乘积 | `3 * 9`，结果为`27`。 |
| `x ** y` | `x`的`y`幂次方 | `2 ** 3`，结果为`8`。 |
| `x / y`  | `x`和`y`的商 | `8 / 2`，结果为`4.0`。 |
| `x // y` | `x`和`y`的商取整 | `4 // 3`，结果为`1`。 |
| `x % y`  | `x`与`y`的余数 | `12 % 7`，结果为`5`。 |
| `-x`     | 取`x`的负数 | `-3`。 |
| `+x`     | 取`x`的正数，原值不会变化 | `+3`。 |

全部数值类型都支持的方法：

| 操作 | 结果 | 示例 |
|:------|:-------|:-----|
| `abs(x)`          | 取`x`的绝对值 | `abs(-32.3)`，结果为`32.3`。 |
| `int(x)`          | 取`x`的整型 | `int(3.84)`，结果为`3`。 |
| `float(x)`        | 取`x`的浮点类型 | `float(5)`，结果为`5.0`。 |
| `complex(re, im)` | 一个以`re`作为实部`im`（默认为`0`）作为虚部的实数 | `complex(2.02, 3.3)`，结果为`(2.02+3.3j)`。 |
| `c.conjugate()`   | 复数`c`的共轭复数 | `(complex(2.02, 3.3)).conjugate()`，结果为`(2.02-3.3j)`。 |
| `divmod(x, y)`    | 由`(x // y, x % y)`组成的值对 | `divmod(12, 7)`，结果为`(1, 5)`。 |
| `pow(x, y)`       | `x`的`y`幂次方，等效于`x ** y` | `pow(2, 3)`，结果为`8`。 |

整型的位操作：

| 操作 | 结果 | 示例 |
|:------|:-------|:-----|
| `x & y`  | 按位与 | `3 & 2`，结果为`2`。 |
| `x ｜ y`  | 按位或 | `3 ｜ 2`，结果为`3`。 |
| `x ^ y`  | 按位异或 | `3 ^ 2`，结果为`1`。 |
| `x << n` | 左移位 | `3 << 2`，结果为`12`。 |
| `x >> n` | 右移位 | `3 >> 2`，结果为`0`。 |
| `~x`     | 按位取反 | `~3`，结果为`-4`。 |

Python的Boolean值由`False`和`True`两个静态对象组成，其它对象参与布尔运算时，通常被认为是`True`（*除非重写其类定义当中的`__bool__()`方法并返回`False`，或者重写`__len__()`并返回`0`*），下列对象在布尔运算中被认为是`False`。

1. 被定义为`False`的等效常量：`None`、`False`。
2. 任意值为`0`的数值类型：`0`、`0.0`、`0j`、`Decimal(0)`、`Fraction(0, 1)`。
3. 空的序列或者集合：`''`、`()`、`[]`、`{}`、`set()`、`range(0)`。

> 包含布尔结果的Python内建函数总是返回`0`和`False`或者`1`和`True`。

特别需要注意的是：**布尔运算`or`和`and`总是返回其中一个操作数本身**，请参见下面的布尔运算符说明表：

| 操作 | 结果 | 示例 |
|:------|:-------|:-----|
| `x or y`  | 如果`x`为假，那么返回`y`，否则返回`x`        | `2 or 3`，结果为`3`。 |
| `x and y` | 如果`x`为假，那么返回`x`, 否则返回`y`        | `2 and 3`，结果为`2`。 |
| `not x`   | 如果`x`为假, 那么返回`True`, 否则返回`False` | `not 0`，结果为`True`。 |

Python拥有6个比较运算符，其各自的运算优先级相同，可以随意链式使用。例如：` x < y <= z `与`x < y and y <= z`等效。

| 操作符 | 结果 | 示例 |
|:------|:-------|:-----|
| `x < y`      | 严格小于 | `3 < 1`，结果为`False`。 |
| `x <= y`     | 小于或等于 | `4 <= 4`，结果为`True`。 |
| `x > y`      | 严格大于 | `12 > 33`，结果为`False`。 |
| `x >= y`     | 大于或等于 | `21 >= 19`，结果为`True`。 |
| `x == y`     | 等于 | `["A", "B"] == ["A", "B"]`，结果为`True`。 |
| `x != y`     | 不等于 | `21 != 21`，结果为`False`。 |
| `x is y`     | 对象引用地址的相等性判断 | `["A", "B"] is ["A", "B"]`结果为`False`。 |
| `x is not y` | 对象引用地址的相等性判断的结果取反 | `["A", "B"] is not ["A", "B"]`结果为`True`。 |

### 字符串 String

Python中的字符串是一个不可变的Unicode字符序列，可以保存在`str`对象或者字符串字面量当中。其中，字符串字面量可以通过如下3种方式书写：

单引号：`'allows embedded "double" quotes'`。
双引号：`"allows embedded 'single' quotes"`。
三引号：`'''Three single quotes'''`、`"""Three double quotes"""`。

> 三引号字符串可以书写到多行，并且所有的空格都将会完整的保存下来。

Python字符串同样可以通过`class str(object=b'', encoding='utf-8', errors='strict')`构造器进行创建。

```py
str("hello python!") == "hello python!" # True
```

Python字符串可以进行索引，字符串第1个字符的索引为`0`，子字符串可以使用分割符`:`来指定。

```py
hank = "uinika"
print(hank[0]) # 输出字符串'u'
print(hank[0:4])  # 输出字符串 'uini'
```

### 列表 List

列表List是一个可变的序列（*即可以对列表的每个数据项进行修改*），用于存储同类数据的集合，可以通过如下方式进行创建：

1. 使用方括号`[]`表达一个空的列表，例如`[]`；
2. 使用方括号`[]`并且使用逗号`,`分隔每项数据，例如：`[1, 2, 3]`；
3. 使用列表理解，例如`[x for x in iterable]`；
4. 使用`list()`或者`list(iterable)`构造器；

```py
'''定义列表'''
cars = ['FORD', 'HONDA', 'BMW']

print(cars) # 输出['FORD', 'HONDA', 'BMW']

'''修改列表'''
car[2] = 'BENZ';
print(cars) # 输出['FORD', 'HONDA', 'BENZ']

'''打印列表指定项'''
print(cars[1]) # 输出HONDA

'''在列表尾部添加新的项目'''
cars.append("BENTLEY")
print(cars) # 输出['FORD', 'HONDA', 'BENZ', 'BENTLEY']

'''返回一个列表的拷贝'''
print(cars[:]) # 输出['FORD', 'HONDA', 'BENZ', 'BENTLEY']

'''指定位置批量插入值'''
cars[1:2] = ['CHERY', 'BYD']
print(cars) # 输出['FORD', 'CHERY', 'BYD', 'BENZ', 'BENTLEY']

'''打印列表长度'''
print(len(cars)) # 输出5

'''清除列表'''
cars = []
print(cars) # 输出[]
```

可以使用`class range(stop)`或者`class range(start, stop[, step])`生成一系列数值，通常指定`for`循环的次数。

```py
for value in range(1, 5):
  print(value)
'''
1
2
3
4
'''
```

使用`list()`构造函数可以将`range()`生成的结果直接转换为列表。

```py
"""生成range"""
range_numbers = range(1, 6)
print(type(range_numbers)) # <class 'range'>

"""转换为list"""
list_numbers = list(range_numbers)
print(type(list_numbers)) # <class 'list'>
print(list_numbers) # [1, 2, 3, 4, 5]
```

### 元组 Tuple

元组（*[ˈtʌpəl]*）是不可修改的序列类型，即不能对其中的元素进行修改。

1. 使用圆括号`()`表达一个空的元组，例如`()`；
2. 向只拥有一个数据项的元组最后添加逗号，例如：`(1,)`
3. 使用逗号分隔不同的数据项，例如：`(1, 2, 3)`；
4. 使用列表理解，例如`[x for x in iterable]`；
5. 使用内建的`tuple()`或者`tuple(iterable)`构造函数；

```py
'''定义元组'''
companies = ("Google", "Facebook", "Microsoft")

'''访问元祖元素'''
print("Top 1 is", companies[0]) # Top 1 is Google

'''访问倒数第1个元祖元素'''
print("Countdown 1 is", companies[-1]) # Countdown 1 is Microsoft

'''截取元组前两个元素'''
print("Top 2 is", companies[0: 2]) # Top 2 is ('Google', 'Facebook')

'''拷贝元组'''
print("All companies is", companies[0:]) # print("All companies are", companies[0:])

'''获取元组元素的个数'''
print("Number of companies is", len(companies)) # Number of companies is 3

'''修改元祖是非法的'''
companies[1] = "Yahoo" # TypeError: 'tuple' object does not support item assignment

'''删除元祖中的元素也是非法的'''
del companies[1] # TypeError: 'tuple' object doesn't support item deletion

'''但是可以删除元组及其所属的变量，so，互联网泡沫来了...'''
del companies;
print("Oops, Internet bubble burst!", companies) # NameError: name 'companies' is not defined
```

元组都可以使用`+`和`*`进行运算，也可以组合或者复制，然后获得一个新的元组。

```py
(1, 2, 3, "A", "B") + (4, 5, 6, "C", "D") # 输出(1, 2, 3, 'A', 'B', 4, 5, 6, 'C', 'D')

("UFO,")*5 # 输出'UFO,UFO,UFO,UFO,UFO,'

"Media" in ("System", "Softawre", "Media") # 输出True

for index in (0,1,2,3,4,5): print(index);
"""
输出
0
1
2
3
4
5
"""
```

> 上面介绍的列表List，也可以进行类似操作。

### 字典 Dictionary

Python官方文档当中，将**列表**（*List*）和**元组**（*Tuple*）归纳为**序列类型**（*Sequence Types*），而将**字典**（* dict*）类型归为**映射类型**（*Mapping Types*）。Python中的字典类型是使用花括号`{}`包裹并通过逗号`,`分隔的`key-value`键值对，例如：`{"name": "hank", "age": 33}`。当然，同样也可以通过`class dict(**kwarg)`、`class dict(mapping, **kwarg)`、`class dict(iterable, **kwarg)`构造函数进行创建。

```py
'''定义字典'''
hank = { "name": "uinika", 33: 1985 }

'''访问字典'''
print(hank["name"], hank[33]) # uinika 1985

'''修改字典'''
hank[33]=2018
print(hank) # {'name': 'uinika', 33: 2018}

'''删除字典'''
del hank[33]
print(hank) # {'name': 'uinika'}

'''使用len()打印字典长度'''
print(len(hank)) # 1

'''使用str()输出字典字符串'''
string_hank = str(hank)
print(string_hank) # {'name': 'uinika'}

'''使用str()输出字典字符串'''
print(type(string_hank)) # <class 'str'>
```

字典的`key`值必须是不可变的，因此可以使用**数字**、**字符串**、**元组**作为键值。但是由于**列表**的元素是可变的，因此被不能作为字典的键值。

```py
'''打印一个使用元组作为key的字典元素'''
dictionary = {(1, 2, 3):('A', 'B', 'C'), "贰": "二", "叁": "三"}
dictionary[(1, 2, 3)] # ('A', 'B', 'C')
```

## 条件判断

Python的条件判断语句与其它类C语言相似，但是每个condition后面需要使用冒号`:`表示后面是满足条件后执行的语句块。需要注意的是，**Python语句块的划分是通过缩来完成的，相同缩进数量的语句构成一个语句块**。

```py
if condition1:
  block1
elif condition2:
  block2
else:
  block3
```

下面的代码是一个条件判断语句的例子，当`if`和`elif`判断的结果都为`False`时，最终打印`else`子句的结果。

```py
if False:
  print("Current condition is IF")
elif False:
  print("Current condition is ELIF")
else:
  print("Current condition is ELSE")

'''
Current condition is ELSE
'''
```

> Python当中没有`switch/case`语句。

## 循环

### while循环

Python中使用`while`循环时，需要特别注意与其它类C语言语法的不同，即语句后的**标识符`:`**与**代码块缩进**。

```py
index = 1

while index <= 100:
  print(index)  # 输出1~100的序数
  index+=1
```

> 注意了，Python是没有`do/while`循环的。

可以通过设置条件表达为`True`实现无限循环，请看下面的例子：

```py
while True:
  print("Thit is an infinite loop")
```

如果`while`循环体当中只拥有一条语句，可以将其与`while`关键字书写在同一行，因此上面无限循环的示例也可以写成下面这样：

```py
while True: print("Thit is an infinite loop")
```

Python的`while`循环拥有一个与其它类C语言截然不同的用法，即使用`while/else`语句在条件判断为`False`时执行`else`语句块当中的内容。

```py
index = 1

while index <= 100:
  print(index)
  index+=1
else:
  print("超过100啦！")
```

### for循环

Python的`for`语句可以用来对**列表**、**元组**、**字典**、**字符串**进行遍历操作。

```py
cars = ['FORD', 'HONDA', 'BMW']

for car in cars:
  print("输出结果：", car)

'''
输出结果： FORD
输出结果： HONDA
输出结果： BMW
'''

companies = ("Google", "Facebook", "Microsoft")

for company in companies:
  print("输出结果：", company)

'''
输出结果： Google
输出结果： Facebook
输出结果： Microsoft
'''

dictionaries = { "total": 10000, "limit": 50 }

for key, value in dictionaries.items(): # 字典的items()方法返回该字典的每个键值对
  print("输出key值：", key)
  print("输出value值：", value)

'''
输出key值： total
输出value值： 10000
输出key值： limit
输出value值： 50
'''

text = "Chengdu"

for character in text:
  print("输出结果：", character)

'''
输出结果： C
输出结果： h
输出结果： e
输出结果： n
输出结果： g
输出结果： d
输出结果： u
'''
```

`for`语句同样可以结合`else`一起使用，`for`循环完毕之后，就会执行`else`子句中的代码。

```py
string = "成都"

for liter in string:
  print(liter)
else:
  print("赵雷")

'''
成
都
赵雷
'''
```

### break与continue

在Python的循环语句当中，可以通过`break`强行跳出当前循环体。

```py
for number in [0, 1, 2, 3, 4, 5]:
  if number == 5:
    break
  print(number)

print("Game over!")

'''
0
1
2
3
4
Game over!
'''
```

也可以通过`continue`直接略过本次循环。

```py
for number in [0, 1, 2, 3, 4, 5]:
  if number == 3:
    print("Skip number 3!")
    continue
  print(number)

'''
0
1
2
Skip number 3!
4
5
'''
```

### pass

`pass`被执行的时候，并不进行任何操作，只起到一个语法占位符的作用。

```py
def demo(arg): pass # 定义一个不进行任何操作的函数

class Demo: pass    # 定义一个没有任何方法的类
```

可以通过定义一个只有`pass`语句的类，来实现类似C语言结构体的功能。

```py
class Engineer:
    pass

hank = Engineer()

hank.name = "uinika"
hank.age = "18"

print(hank.name + " is just only " + hank.age) # uinika is just only 18
```

## 函数

Python使用关键字`def`来定义函数，使用方式和声明规则与其它类C语言相似。

```py
'''定义函数'''
def demo(parameter):
  print('this is a' + parameter + '!')
  return 0

'''调用函数
demo("function")
```

同其它类C语言一样，Python中的变量也可以分为局部变量（*定义在函数内部*）和全局变量（*定义在函数外部*）。

```py
'''定义函数'''
test = '全局变量'
def demo():
    test = '局部变量'
    print(test) # 局部变量

'''调用函数'''
demo()
```

### 命名参数

调用Python函数时，可以向其传递命名参数，指定该参数值由哪个函数参数进行接收，避免按照顺序接收所可能带来的潜在错误。

```py
def function(parameter): 
  print("parameter", parameter)

'''传递命名参数'''
function(parameter = 0) # parameter 0
```

### 默认参数

定义Python函数的时候，对于缺省的参数可以赋予其一个默认值。

```py
'''
定义函数的时候声明了parameter2的默认参数
'''
def function(parameter1, parameter2 = 2): 
  print("执行结果：")
  print("parameter1", parameter1)
  print("parameter2", parameter2)
)

function(parameter1 = 1)

'''
执行结果：
parameter1： 1
parameter2： 2
'''
```

### 可变参数列表

定义函数时，可以使用星号`*`作为前缀来声明一个可变参数列表，用来接收调用函数时传递的任意个数参数，这些参数会被包装至一个**元组**。

```py
# 在可变参数之前，可以放置任意数量的普通参数
def demo(parameter, *tuple):
  print('Parameter is：', parameter)
  print('Tuple is：', tuple)

demo('Hello Python!', 1, 2, 3, '四', '五')

'''
Parameter is： Hello Python!
Tuple is： (1, 2, 3, '四', '五')
```

也可以使用`**`作为前缀来声明参数，此时这些参数会包装为一个**字典**。

```py
def demo(parameter, **dictionary):
  print("Parameter is", parameter)
  print("Dictionary is", dictionary)

demo("Hello World!", a=1, b=2, c=3)

'''
Parameter is Hello World!
Dictionary is {'a': 1, 'b': 2, 'c': 3}
'''
```

如果`*`号**单独**出现在函数参数当中，那么后续的参数则必须使用**命名参数**显式传入。

```PY
def demo(parameter1, *, parameter2, parameter3):
  print("Parameter1 is", parameter1)
  print("Parameter2 is", parameter2);
  print("Parameter3 is", parameter3);

demo(1, parameter2 = 2, parameter3 = 3)

'''
Parameter1 is 1
Parameter2 is 2
Parameter3 is 3
'''

demo(A, B, parameter3 = C)

'''
Traceback (most recent call last):
  File "test1.py", line 14, in <module>
    demo(A, B, parameter3 = C)
NameError: name 'A' is not defined
'''
```

### lambda函数

Python的lambda函数是只由一个Python表达式所组成的匿名的内联函数，其语法书写形式如下：

```py
lambda [parameters]: expression
```

lamdba函数的语法只能包含一条语句，例如：

```py
demo = lambda parameterA, parameterB: print(parameterA / parameterB)

demo(1985, 8)

'''
248.125
'''
```

### return语句

`return`语句用于退出函数并返回函数的执行结果值，具体用法如下代码所示：

```py
def demo(parameter1, parameter2):
  return parameter1 + parameter2

print(demo(83, 2))
```

当Python中的`return`语句没有返回值时，则默认返回值为`None`。

```py
def demo():
  return

print(demo())

'''
None
'''
```

> 不带参数值的`return`语句返回`None`。

## 作用域

Python当中仅`module`模块、`class`类、`def`或`lambda`函数会引入新作用域，`if/elif/else`、`try/except`、`for/while`等代码块并不会引入新作用域，即这些语句当中定义的变量在其外部也能访问。

```py
def function():
  STRING = "This is a String!"

print(text)

'''
Traceback (most recent call last):
  File "test1.py", line 4, in <module>
    print(text)
NameError: name 'text' is not defined
'''

def function():
  text = "This is a String!"
  print(text)

function()

'''
This is a String!
'''
```

### `global`关键字

使用`global`关键字声明的标识符将会引用至**全局变量**，在局部作用域中对其进行的修改操作都将会保留下来，就如同操作真正的全局变量一样。

```py
text = "全局变量"

def function():
  global text
  print(text) # 输出："全局变量"
  text = "局部变量"
  print(text) # 输出："局部变量"

function()

print(text) # 输出："局部变量"
```

### `nonlocal`关键字

使用`nonlocal`关键字声明的标识符将会引用至当前作用域外层的变量，在当前作用域对其进行的修改操作都将会保留，如同在真正的操作该作用域外层的变量一样。

```py
def outer():
    text = "外部变量"

    def inner():
      nonlocal text
      text = "内部变量"
      print(text) # 输出："内部变量"
    
    inner()

    print(text) # 输出："内部变量"

outer()
```

## 类

Python使用`class`关键字创建一个**类**，然后直接调用类名即其初始化方法就可以创建这个类的**实例**。类进行实例化时，会自动调用该类的初始化方法`__init__(self)`（*作用类似于Java当中的构造函数*）。

```py
# Dog类
class Dog:
  # 类属性
  age = ""
  # 初始化方法
  def __init__(self, age):
    self.age = age;
  # 类方法
  def run(self):
    print("I'm running!")

pet = Dog("1岁") # 实例化Dog类，并显式向初始化函数__init__传递参数

print(pet.age)

pet.run()

'''
1岁
I'm running!
'''
```

> 注意：类方法（*包括初始化方法*）中的`self`参数是不能省略的，该参数指向类的实例，而非类本身。当然，根据个人编码习惯，也可以将`self`置换为其它语言中更为常用的`this`进行命名。

### 继承

Python做为面向对象的语言，自然是支持继承的。需要继承一个类，只需要在定义子类时传入父类的名称即可，同时为了保证子类和父类都能够正确的实例化，子类的初始化方法需要显示调用父类的初始化方法。

```py
# 定义Dog父类
class Dog:
  age = ""

  def __init__(self, age):
    self.age = age;

  def run(self):
    print(self.age)


# 定义Puppy子类，并传入Dog父类
class Puppy(Dog):
  weight = ""

  def __init__(self, weight):
    Dog.__init__(self, "1岁") # 调用父类Dog的初始化方法
    self.weight = weight;

  def cute(self):
    print(self.weight)

pet = Puppy("10斤")

pet.run() # 调用父类Dog的方法
pet.cute() # 调用子类Puppy的方法

'''
1岁
10斤
'''
```

如同Java一样，Python也是可以实现多重继承的。多重继承时，为了保证继承树能够正确的进行实例化，需要在子类的初始化方法`__init__`内显式的调用父类们的初始化方法，并将子类的`self`属性传递过去。

```py
class A:
  attribute = "";
  def __init__(self):
    print("A")

class B:
  def __init__(self):
    print("B")

class C(A, B):
  def __init__(self):
    A.__init__(self) # 在子类初始化方法内调用父类A的初始化方法
    B.__init__(self) # 在子类初始化方法内调用父类B的初始化方法
    print("C")

demo = C()

'''
A 
B 
C 
'''
```

### 私有属性和方法

在类中声明属性和方法时添加两条下划线`__`，就可以将这个属性和方法声明为**私有**的。私有属性和方法只能在类中通过`self.__private`进行访问，而不能在类实例化后进行访问。

```py
class demo:
  __attribute = "私有属性"

  def __getAttribute(self):
    print(self.__attribute + "私有方法")
  
test = demo()
test.__attribute # AttributeError: 'demo' object has no attribute '__attribute'
test.__getAttribute() # AttributeError: 'demo' object has no attribute '__getAttribute'  
```

### 方法重写override

如果父类中定义的方法不能满足要求，那么可以考虑在子类中对父类的方法进行重写。

```py
class Parent:
  def method(self):
    print("输出：Parent")

class Child(Parent):
  def __init__(self):
    Parent.__init__(self)
  def method(self):
    print("输出：Child")

childInstance = Child()

childInstance.method() # 输出：Child
```

当然，也可以通过`super()`函数显式调用被子类重写了的父类方法。对于上面的例子，可以使用如下语句调用父类的`method()`方法。

```py
super(Child, childInstance).method() # 输出：Parent
```

### 迭代器

大家可能注意到许多容器对象能够使用`for`语句进行循环处理，就像下面代码这样：

```py
for element in [1, 2, 3]:
    print(element)

for element in (1, 2, 3):
    print(element)

for key in {'one':1, 'two':2}:
    print(key)

for char in "123":
    print(char)

for line in open("file.txt"):
    print(line, end='')
```

这样的处理方法简单明了，实质上`for`语句调用容器对象上的`iter()`方法，该方法返回一个迭代器对象，这个迭代器对象当中定义了一个`__next__()`方法用于操作容器对象的元素，当没有更多可供迭代的元素时，该方法将会抛出一个`StopIteration`异常通知`for`语句终止循环操作。这里你可以通过`next()`内置函数去调用`__next__()`方法，参见下面的例子：

```py
string = 'abc'

stringIterator = iter(string)
print(stringIterator) # 输出<str_iterator object at 0x00000000023F8898>

print(next(stringIterator)) # 输出a
print(next(stringIterator)) # 输出b
print(next(stringIterator)) # 输出c
print(next(stringIterator))

'''
输出
Traceback (most recent call last):
  File "test.py", line 9, in <module>
    print(next(stringIterator))
StopIteration
'''
```

定义一个`iter()`方法，该方法用`next()`方法返回一个对象。如果该类定义了`next()`，那么`iter()`就可以返回`self`。

```py
# 迭代器，用于反向循环一个序列
class Reverse:
  def __init__(self, data):
    self.data = data # 初始化函数传入的待处理数据
    self.index = len(data) # 待处理数据的长度

  def __iter__(self):
    return self # 返回对象实例本身

  def __next__(self):
    if self.index == 0:
      raise StopIteration
    self.index = self.index - 1 
    return self.data[self.index] # 从字符串尾部开始逐一返回字母

reverseUinika = Reverse('Hank')
iter(reverseUinika) # 生成迭代器对象

for char in reverseUinika: # 循环打印
  print(char)

'''
k
n
a
H
'''
```

### 生成器

生成器Generator是一个用于建立迭代器iterators的简单又强大的工具，其书写方式类似于函数，但是在返回数据的时候使用了`yield`语句。当生成器的`next()`每次被调用的时候，生成器会恢复到其离开的位置（*生成器能够记忆所有的数据和最后执行的语句位置*）。

```py
def reverse(data):
  for index in range(len(data) - 1, -1, -1):
    yield data[index] # 使用yield语句

for char in reverse("Hank"):
  print(char)

'''
k
n
a
H
'''
```

上述代码实现了之前迭代器示例相同的功能，生成器函数代码如此短小精悍的原因在于`iter()`和`next()`方法的创建以及`StopIteration`异常抛出都是自动进行的。另外生成器函数的局部变量和执行状态在每次调用都会被保存，这样比前面基于class的迭代器总是手动处理`self.index`和`self.data`更加便捷。

一些简单的生成器可以使用特殊语法书（*与列表解析相似，不过使用圆括号代替了*）书写为一种更加简捷的表达式，即**生成器表达式**。这种表达式常用于在闭包函数内使用生成器的情况，语法上比完整的生成器定义更紧凑，并且比同等的列表理解更加容易记忆。

```py
# 求平方和
sumOfSquares = sum(index * index for index in range(10)) 
print(sumOfSquares) # 285

# 求点积
a = [10, 20, 30]
b = [7, 5, 3]
dotProduct = sum(x*y for x,y in zip(a, b))
print(dotProduct) # 260
```

## 异常处理

## 模块管理

## 环境隔离

## 输入输出

## 代码测试

## Python之禅

## 实践：使用Djongo搭建Web服务

## 实践：在线图片相似度比较