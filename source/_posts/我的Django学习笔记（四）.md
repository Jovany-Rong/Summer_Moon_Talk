---
title: 我的Django学习笔记（四）：登录界面中cookie的使用
copyright: true
categories: Python
tags:
  - Python
  - Django
  - BS开发
  - 学习笔记
abbrlink: '2e782639'
date: 2019-06-07 19:57:59
---

Django是Python的Web应用模块中非常流行的一款。**我的Django学习笔记**系列博文将记录我学习使用Django的历程。

本系列博文将不定期更新，欢迎各位前来捧场。

本篇博文主要记录了在登录界面中使用coockie的步骤。

<!-- More -->

# 添加登录动作的浏览器Cookie的设置和读取

编辑 **guest/sign/views.py** 文件。

*views.py*

```
# 登录动作
def login_action(request):
    if request.method == 'POST':
        username = request.POST.get('username', '')
        password = request.POST.get('password', '')
        if username == 'admin' and password == '123':
            response = HttpResponseRedirect('/event_manage/') # 设定response变量
            response.set_cookie("user", username, 3600) # 添加coockie
            return response # 返回response变量
        else:
            return render(request, 'index.html', {'error': 'username or password error!'})

# 会议管理
def event_manage(request):
    username = request.COOKIES.get("user", "") # 读取cookie
    return render(request, 'event_manage.html', {"user":username}) # 返回用户名
```

在本例 **set_cookie()** 方法中，第一个参数表示写入浏览器的cookie名，第二个参数表示cookie值，第三个参数为cookie在浏览器中的保持时间（秒）。

编辑 **guest/sign/templates/event_manage.html** 文件，添加以下代码。

*event_manage.html*

```
        <div style="float:right;">
            <a>Hey, {{ user }}. Welcome!</a><hr/>
        </div>
```

刷新页面重新登录。

![](http://ww1.sinaimg.cn/large/006tNc79gy1g3sxp3vpksj30rk0iamxd.jpg)