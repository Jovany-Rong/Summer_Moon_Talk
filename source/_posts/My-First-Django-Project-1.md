---
title: 我的Django学习笔记（一）：第一个Django项目
categories: Python
tags:
  - Python
  - Django
  - BS开发
  - 学习笔记
copyright: true
abbrlink: e568
date: 2019-05-31 23:16:38
---

Django是Python的Web应用模块中非常流行的一款。**我的Django学习笔记**系列博文将记录我学习使用Django的历程。

本系列博文将不定期更新，欢迎各位前来捧场。

本篇博文主要记录了Django环境准备、启动项目。

<!-- More -->

# 环境准备

## 前置环境

首先贴出系统环境和Python环境。

操作系统为MacOS 10.14.5。

Python环境为3.7.0。

## Django安装

使用pip安装django，代码如下。

```
$ pip install django
```

安装完成后使用如下命令查看Django版本。

```
$ python

>>>import django

>>>django.VERSION
```

查到安装的Django版本为2.2.1，说明Django安装成功。

# 创建Django项目

## 新建项目

使用django-admin来创建新项目 *HelloWorld* ， 代码如下。

```
$ django-admin startproject HelloWorld
```

查看项目目录结构，代码如下。

```
$ tree
.
├── HelloWorld
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── manage.py

1 directory, 5 files
```

该目录所有目录和文件的说明如下。

 - HelloWorld: 项目的容器。
 - manage.py: 一个实用的命令行工具，可让你以各种方式与该 Django 项目进行交互。
 - HelloWorld/__init__.py: 一个空文件，告诉 Python 该目录是一个 Python 包。
 - HelloWorld/settings.py: 该 Django 项目的设置/配置。
 - HelloWorld/urls.py: 该 Django 项目的 URL 声明; 一份由 Django 驱动的网站"目录"。
 - HelloWorld/wsgi.py: 一个 WSGI 兼容的 Web 服务器的入口，以便运行你的项目。

使用以下命令启动Django服务器。

```
$ python manage.py runserver 0.0.0.0:8000
```

在浏览器访问 **127.0.0.1:8000** ，出现 **Django** 页面。

## 配置视图及URL

在项目目录中 **HelloWorld** 目录内新建 **view.py** 文件，并写入以下代码。

```
from django.http import HttpResponse
 
def hello(request):
    return HttpResponse("Hello world ! ")
```

打开 **urls.py** 文件，删除原来代码，将以下代码复制粘贴到 **urls.py** 文件中。

```
from django.conf.urls import url
 
from . import view
 
urlpatterns = [
    url(r'^$', view.hello),
]
```

目录结构如下。

```
$ tree
.
├── HelloWorld
│   ├── __init__.py
│   ├── __pycache__
│   │   ├── __init__.cpython-37.pyc
│   │   ├── settings.cpython-37.pyc
│   │   ├── urls.cpython-37.pyc
│   │   ├── view.cpython-37.pyc
│   │   └── wsgi.cpython-37.pyc
│   ├── settings.py
│   ├── urls.py
│   ├── view.py
│   └── wsgi.py
├── db.sqlite3
└── manage.py

2 directories, 12 files
```

启动Django服务器，浏览器打开 **127.0.0.1:8000** ，页面显示 **Hello world !** 。

修改 **urls.py** 中的代码如下。

```
from django.urls import path
 
from . import view
 
urlpatterns = [
    path('hello/', view.hello),
]
```

则在浏览器打开 **127.0.0.1:8000/hello** ，页面显示 **Hello world !** 。

**注意**，Django无需重启，即可重新载入新的代码。