---
title: 我的Django学习笔记（二）：使用模板打开页面
copyright: true
categories: Python
tags:
  - Python
  - Django
  - BS开发
  - 学习笔记
abbrlink: 9771b8da
date: 2019-06-03 22:10:34
---

Django是Python的Web应用模块中非常流行的一款。**我的Django学习笔记**系列博文将记录我学习使用Django的历程。

本系列博文将不定期更新，欢迎各位前来捧场。

本篇博文主要记录了创建guest项目并以模板方式打开Hello Django页面。

<!-- More -->

# 项目介绍

从本期开始，我开始跟着 **《Web接口开发与自动化测试————基于Python语言》** （虫师 著，2017年版）学习。

现在的目标是使用Django开发一个简单的发布会签到系统。

# 创建guest项目

使用Django-Admin创建项目 **guest** 。

```
$ django-admin startproject guest
```

# 创建sign应用

使用manage工具创建应用 **sign** 。

```
$ cd guest
$ python manage.py startapp sign
```

启动Django服务器。

```
$ python manage.py runserver
```

浏览器打开 **127.0.0.1:8000** 。

![](http://ww2.sinaimg.cn/large/006tNc79gy1g3oc4eju2kj311l0u03zz.jpg)

出现以上画面，说明Django启动成功。

# 将sign应用添加到guest项目中

打开 **guest/settings.py** 文件，添加 **sign** 条目。

*settings.py*

```
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'sign', # 添加sign应用
]
```

# 通过访问 127.0.0.1:8000/index 地址显示 “Hello Django”页面

在 **guest/urls.py** 文件中，添加/index/的路径配置。

*urls.py*

```
from django.contrib import admin
from django.urls import path
from sign import views # 导入views文件

urlpatterns = [
    path('admin/', admin.site.urls),
    path('index/', views.index, name="index"), # 添加/index/路径配置
]
```

在 **guest/sign/views.py** 文件中，添加index函数。

*views.py*

```
from django.shortcuts import render
from django.http import HttpResponse # 引入HttpResponse类

# Create your views here.
def index(request): # 创建index函数
    return HttpResponse("Hello Django!")
```

访问 **127.0.0.1:8000/index** 页面，显示 “Hello Django!”。

![](http://ww1.sinaimg.cn/large/006tNc79gy1g3of9f2mtdj30pe0c0dfu.jpg)

# 使用模板展示Hello Django页面

在应用 **sign/** 目录中创建 **templates/index.html** 文件。

*index.html*

```
<html>
    <head>
        <title>Django Page</title>
    </head>
    <body>
        <h1>Hello Django!</h1>
    </body>
</html>
```

修改视图文件 **views.py** 。

*views.py*

```
from django.shortcuts import render
# from django.http import HttpResponse # 无需使用 HttpResponse，注释掉

# Create your views here.
def index(request):
    return render(request, "index.html") # 改为使用render 处理请求
```

刷新页面。

![](http://ww3.sinaimg.cn/large/006tNc79gy1g3ofjpthsuj30k60bywel.jpg)