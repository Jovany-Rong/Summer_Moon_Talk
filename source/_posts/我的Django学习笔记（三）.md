---
title: 我的Django学习笔记（三）：登录功能的简单实现
copyright: true
categories: Python
tags:
  - Python
  - Django
  - BS开发
  - 学习笔记
abbrlink: 24e9015a
date: 2019-06-04 19:43:58
---

Django是Python的Web应用模块中非常流行的一款。**我的Django学习笔记**系列博文将记录我学习使用Django的历程。

本系列博文将不定期更新，欢迎各位前来捧场。

本篇博文主要记录了简单实现用户登录功能。

<!-- More -->

# 编写登录页面

首先在 **guest/sign/templates/index.html** 文件中，编写登录表单。

*index.html*

```
<!DOCTYPE HTML>
<html>
<head>
<title>Login Page</title>
<link href="css/style.css" rel="stylesheet" type="text/css" media="all" />
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" /> 
<!-- -->
<script>var __links = document.querySelectorAll('a');function __linkClick(e) { parent.window.postMessage(this.href, '*');} ;for (var i = 0, l = __links.length; i < l; i++) {if ( __links[i].getAttribute('data-t') == '_blank' ) { __links[i].addEventListener('click', __linkClick, false);}}</script>
<script src="js/jquery.min.js"></script>
<script>$(document).ready(function(c) {
	$('.alert-close').on('click', function(c){
		$('.message').fadeOut('slow', function(c){
	  		$('.message').remove();
		});
	});	  
});
</script>
</head>
<body>
<!-- contact-form -->	
<div class="message warning">
<div class="inset">
	<div class="login-head">
		<h1>Login Form</h1>
		 <div class="alert-close"> </div> 			
	</div>
		<form>
			<li>
				<input name="username" type="text" class="text" value="Username" onfocus="this.value = '';" onblur="if (this.value == '') {this.value = 'Username';}"><a href="#" class=" icon user"></a>
			</li>
				<div class="clear"> </div>
			<li>
				<input name="password" type="password" value="Password" onfocus="this.value = '';" onblur="if (this.value == '') {this.value = 'Password';}"> <a href="#" class="icon lock"></a>
			</li>
			<div class="clear"> </div>
			<div class="submit">
				<button id="btn" type="submit">Sign In</button>
				<!--<h4><a href="#">Lost your Password ?</a></h4>-->
						  <div class="clear">  </div>	
			</div>
				
		</form>
		</div>					
	</div>
	</div>
	<div class="clear"> </div>
<!--- footer --->
<div class="footer">
	<p>Copyright &copy; 2019 Chenfei Jovany Rong.</p>
</div>

</body>
</html>
```

该模板为从网上摘抄修改，相关CSS和JS与功能无关，略。

启动Django，访问 **127.0.0.1:8000/index** 页面。

![](http://ww1.sinaimg.cn/large/006tNc79gy1g3pdmcgb39j30la0gamxc.jpg)

# 使用post方法登录

将表单method属性设置为post。

*index.html*

```
		<form method="post">
			<li>
				<input name="username" type="text" class="text" value="Username" onfocus="this.value = '';" onblur="if (this.value == '') {this.value = 'Username';}"><a href="#" class=" icon user"></a>
			</li>
				<div class="clear"> </div>
			<li>
				<input name="password" type="password" value="Password" onfocus="this.value = '';" onblur="if (this.value == '') {this.value = 'Password';}"> <a href="#" class="icon lock"></a>
			</li>
			<div class="clear"> </div>
			<div class="submit">
				<button id="btn" type="submit">Sign In</button>
				<!--<h4><a href="#">Lost your Password ?</a></h4>-->
						  <div class="clear">  </div>	
			</div>
				
		</form>
```

刷新页面，点击登录。

![](http://ww3.sinaimg.cn/large/006tNc79gy1g3pdxcwx1nj324g0pewgr.jpg)

页面报了**跨站请求伪造（CSRF）**错误。

在index.html文件中增加CSRF令牌。

*index.html*

```
		<form method="post">
			<li>
				<input name="username" type="text" class="text" value="Username" onfocus="this.value = '';" onblur="if (this.value == '') {this.value = 'Username';}"><a href="#" class=" icon user"></a>
			</li>
				<div class="clear"> </div>
			<li>
				<input name="password" type="password" value="Password" onfocus="this.value = '';" onblur="if (this.value == '') {this.value = 'Password';}"> <a href="#" class="icon lock"></a>
			</li>
			<div class="clear"> </div>
			<div class="submit">
				<button id="btn" type="submit">Sign In</button>
				<!--<h4><a href="#">Lost your Password ?</a></h4>-->
						  <div class="clear">  </div>	
			</div>
			{% csrf_token %}     // 新增的CSRF令牌	
		</form>
```

重新刷新页面。不产生报错。

# 处理登录请求

设置表单的action属性。

*index.html*

```
		<form method="post" action="/login_action/"> // 添加action属性
			<li>
				<input name="username" type="text" class="text" value="Username" onfocus="this.value = '';" onblur="if (this.value == '') {this.value = 'Username';}"><a href="#" class=" icon user"></a>
			</li>
				<div class="clear"> </div>
			<li>
				<input name="password" type="password" value="Password" onfocus="this.value = '';" onblur="if (this.value == '') {this.value = 'Password';}"> <a href="#" class="icon lock"></a>
			</li>
			<div class="clear"> </div>
			<div class="submit">
				<button id="btn" type="submit">Sign In</button>
				<!--<h4><a href="#">Lost your Password ?</a></h4>-->
						  <div class="clear">  </div>	
			</div>
			{% csrf_token %}	
		</form>
```

设置login_action的路由。

*urls.py*

```
urlpatterns = [
    path('admin/', admin.site.urls),
    path('index/', views.index, name="index"),
    path('login_action/', views.login_action), # 新增
]
```

创建login_action视图函数。

*views.py*

```
from django.shortcuts import render
from django.http import HttpResponse # 引入

# Create your views here.
def index(request):
    return render(request, "index.html")

# 登录动作
def login_action(request): # 创建
    if request.method == 'POST':
        username = request.POST.get('username', '')
        password = request.POST.get('password', '')
        if username == 'admin' and password == '123':
            return HttpResponse('Login success!')
        else:
            return render(request, 'index.html', {'error': 'username or password error!'})
```

在 **index.html** 模板中添加报错位置。

*index.html*

```
		<form method="post" action="/login_action/">
			<li>
				<input name="username" type="text" class="text" value="Username" onfocus="this.value = '';" onblur="if (this.value == '') {this.value = 'Username';}"><a href="#" class=" icon user"></a>
			</li>
				<div class="clear"> </div>
			<li>
				<input name="password" type="password" value="Password" onfocus="this.value = '';" onblur="if (this.value == '') {this.value = 'Password';}"> <a href="#" class="icon lock"></a>
			</li>
			<div class="clear"> </div>
			{{ error }}<br> // 添加报错位置，为render返回字典的key
			<div class="submit">
				<button id="btn" type="submit">Sign In</button>
				<!--<h4><a href="#">Lost your Password ?</a></h4>-->
						  <div class="clear">  </div>	
			</div>
			{% csrf_token %}	
		</form>
```

刷新页面。若用户名/密码为 **admin/123** 。

![](http://ww3.sinaimg.cn/large/006tNc79gy1g3pftluoz1j30ls0ccglm.jpg)

若用户名/密码不为 **admin/123** 。

![](http://ww3.sinaimg.cn/large/006tNc79gy1g3pfvb0etij30na0hq0t0.jpg)

# 创建登录成功页面

刚才是通过直接返回登录成功字符串展示登录成功，这只是一种临时方案。我们需要让其跳转登录成功的页面。

创建 **guest/sign/templates/event_manage.html** 文件。

*event_manage.html*

```
<html>
    <head>
        <title>Event Manage Page</title>
    </head>
    <body>
        <h1>Login success!</h1>
    </body>
</html>
```

添加会议管理视图函数并修改登录动作。

*views.py*

```
from django.shortcuts import render
from django.http import HttpResponse, HttpResponseRedirect # 增加重定向

# Create your views here.
def index(request):
    return render(request, "index.html")

# 登录动作
def login_action(request):
    if request.method == 'POST':
        username = request.POST.get('username', '')
        password = request.POST.get('password', '')
        if username == 'admin' and password == '123':
            return HttpResponseRedirect('/event_manage/') # 修改
        else:
            return render(request, 'index.html', {'error': 'username or password error!'})

# 会议管理
def event_manage(request): # 新增
    return render(request, 'event_manage.html')
```

添加 **event_manage/** 的路由。

*urls.py*

```
urlpatterns = [
    path('admin/', admin.site.urls),
    path('index/', views.index, name="index"),
    path('login_action/', views.login_action),
    path('event_manage/', views.event_manage), # 添加
]
```