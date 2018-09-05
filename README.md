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

笔者的Linux开发环境下，同时存在`Python 3.6.5`和`Python 2.7.15`两个版本，因此Z-shell命令行中运行`Hello World`程序时，需要显式输入`python3`，以提示系统打开`Python 3.6.5`运行环境。

```bash
➜  / python3
Python 3.6.5 (default, Apr  1 2018, 05:46:30) 
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> print("Hello World!")
Hello World!
```

当然，也可以单独将`print("Hello World!")`保存到一个独立的`print.py`代码文件，然后在命令行当中直接开始运行。

```bash
➜  1-hello-world python3 print.py
Hello World!
```

## 数据类型

## 列表

## 条件判断

## 函数

## 类

## 异常

## 文件操作

## 代码测试

## 包管理

## 环境隔离

## Djongo框架

## 实践：在线图片相似度比较

