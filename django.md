### 一、Django简介

### 1. Diango一个高效的web框架，以最小代码构建和维护高质量web应用;

### 2. 减少重复代码，专注于Web应用上关键的东西;



**环境搭建**

创建虚拟环境（可以跳过） ：

```text
mkvirtualenv django_env
```

安装django模块：

```text
pip install Django     # 不指定版本号，默认安装最新版
pip install Django==1.11.6    # 指定版本号
```

**二、案例1 - hello world**

**创建Django项目**

```text
1. 创建方式：
     
     #方式1：终端输入
         django-admin startproject testmvt .
         
     #方式2:
        pycharm中新建django项目
```



### 配置URL

~~~text
```
from django.conf.urls import url
from django.contrib import admin
import views

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^$', views.login_view),
]

```
~~~

### 创建views.py文件

```text
#coding=utf-8
from django.http.response import HttpResponse


def login_view(request):
    return HttpResponse('hello world')
```

### 启动服务器

```text
python manage.py runserver 127.0.0.1:8000
```

### 浏览器访问

```text
    http://127.0.0.1:8000/
```

### 知识点总结

```text
testmvt项目包下目录说明：

1.settings.py:包括了项目的初始化设置。可以针对整个项目有关的参数配置。例如（配置数据库，添加应用等）

2.urls.py：（URLconf）这是一个URL配置表文件。主要将URL映射到应用程序上。

3.wsgi.py:WSGI是Web Server Gateway Interface的缩写。WSGI是Python所选择的服务器和应用标准，Django也会使用。
          wsgi.py文件定义了我们所创建的项目都是WSGI应用。
```

作者：冷颜夕
链接：https://zhuanlan.zhihu.com/p/81174316
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



**三、案例2--显示登录首页**

创建django项目

```text
django-admin startproject demo2
```

注意：在命令行里创建的 django 项目没有存放页面的 templates 文件夹。需要后期手动创建，并且在 settings 中 TEMPLATES 中的 'DIRS' 空列表的 路径内容 补上，其他内容不变。

```text
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
```

### 创建student应用

```text
python manage.py startapp student
```

### 在settings.py文件中添加应用

```text
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'student'
]
```

### 配置URL

1. 项目包->[urls.py](http://link.zhihu.com/?target=http%3A//urls.py/)

```text
from django.conf.urls import url, include
    from django.contrib import admin
    
    urlpatterns = [
        url(r'^admin/', admin.site.urls),
        url(r'^student/', include('student.urls')),
    ]
```

1. 创建并编辑应用包->urls.py文件

```text
#coding=utf-8

    from django.conf.urls import url
    import views
    
    urlpatterns = [
        url(r'^$',views.login_view)
    ]
```

### 编辑应用包->view.py文件

```text
# -*- coding: utf-8 -*-
    from __future__ import unicode_literals
    
    from django.shortcuts import render
    
    # Create your views here.
    def login_view(request):
        
        return render(request,'login.html')
```

### 在templates目录下创建login.html

```text
<!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
        <form action="" method="get">
            <p><label for="uname">用户名：</label><input type="text" name="uname" id="uname"/></p>
            <p><label for="pwd">密&emsp;码：</label><input type="password" name="pwd" id="pwd" /></p>
            <p><input type="submit" value="登&emsp;录"/></p>
        </form>
    </body>
    </html>
```

### 启动服务器

```text
python manage.py runserver 127.0.0.1:8000
```

### 浏览器访问

```text
http://127.0.0.1:8000/student/
```

### 总结知识点

```text
应用包目录下文件说明：
1. admin.py：在这个文件中，可以自定义Django管理工具。
例如：设置在管理界面能够管理的项目或者通过重定义于系统管理相关的类对象，向管理功能添加新的内容。

2. apps.py:(Django1.10之后增加)通常包含对应用的配置。例如：为管理功能提供一个适合的应用名称。

3. migrations:这个是一个目录。用于存储应用的数据库表结构的指令。

4. models.py:这是应用的数据模型。

5. tests.py:在这个文件中可以编写测试文档来测试所建立的应用。

6. views.py:这是一个重要的文件。用户保存响应各种请求的函数或者类。
```

**四、MVC_MVT模式**

### MVC模式

```text
MVC各部分的功能:
    M全拼为Model，主要封装对数据库层的访问，对数据库中的数据进行增、删、改、查操作。
    
    V全拼为View，用于封装结果，生成页面展示的html内容。
    
    C全拼为Controller，用于接收请求，处理业务逻辑，与Model和View交互，返回结果。
```

### MVT模式

```text
MVT各部分的功能:
    M全拼为Model，与MVC中的M功能相同，负责和数据库交互，进行数据处理。
    
    V全拼为View，与MVC中的C功能相同，接收请求，进行业务处理，返回响应。
    
    T全拼为Template，与MVC中的V功能相同，负责封装构造要返回的html。
```

**补充：**

Ctrl + D : 复制上一行

作者：冷颜夕
链接：https://zhuanlan.zhihu.com/p/81174316
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



**五、案例3-登录功能（不连数据库）**

### 完善login.html

```text
添加action和method属性值
<form action="/student/login/" method="get">
```

说明：action=""里面的第一个 '/'代表根路径，一定不能忘写。如果没写代表相对路经，会在每次点击提交按钮后，在原有url路径后面继续无限次的追加。而导致无法正常提交数据。

### student应用->urls.py添加路由

```text
#coding=utf-8

        from django.conf.urls import url    # django 2.0以后的版本这里导入的包名改为 path
        import views    # 如果这样写报错可以改为from . import views   其中 . 代表当前路径
        
        urlpatterns = [
            url(r'^$',views.login_view),
            url(r'^login/',views.to_login_view),
            #  django 2.0以后的版本的写法
            # path('admin/', admin.site.urls),
            # path('login/', views.login_view),
            # path('do_login/', views.do_login_view),
        ]
```

### 编辑student应用->views.py文件

```text
# -*- coding: utf-8 -*-
    from __future__ import unicode_literals
    
    from django.http import HttpResponse
    from django.shortcuts import render
    
    users = [
        ('zhangsan','123'),
        ('lisi','123')
    ]
    
    
    # Create your views here.
    #显示登录首页
    def login_view(request):
    
        return render(request,'login.html')
    
    #登录功能
    def to_login_view(request):
        #接收请求参数
        uname = request.GET.get('uname','')
        pwd = request.GET.get('pwd','')
    
        #判断是否登录成功
        for u_uname,u_pwd in users:
            if uname==u_uname and pwd ==u_pwd:
                return HttpResponse('登录成功！')
    
        return HttpResponse('登录失败！')
```

### 启动服务器

### 浏览器访问

### 查看GET请求报文

### POST请求方式

### 修改login.html

```text
<form action="/student/login/" method="post">
```

### 浏览器直接访问报403错误

```text
Forbidden (403)CSRF verification failed. Request aborted.
```

### 解决办法

```text
1. login.html 表单标签内容添加 {% csrf_token %}
2. settings.py文件中的csrf中间件注释
MIDDLEWARE = [
            'django.middleware.security.SecurityMiddleware',
            'django.contrib.sessions.middleware.SessionMiddleware',
            'django.middleware.common.CommonMiddleware',
            # 'django.middleware.csrf.CsrfViewMiddleware',
            'django.contrib.auth.middleware.AuthenticationMiddleware',
            'django.contrib.messages.middleware.MessageMiddleware',
            'django.middleware.clickjacking.XFrameOptionsMiddleware',
        ]
```

### 浏览器访问出现“登录失败！”

```text
1.解决办法：
    修改student/views.py/to_login()
#登录功能
        def to_login_view(request):
            #接收请求参数
            uname = request.POST.get('uname','')
            pwd = request.POST.get('pwd','')
        
            #判断是否登录成功
            for u_uname,u_pwd in users:
        
                if uname==u_uname and pwd ==u_pwd:
        
                    return HttpResponse('登录成功！')
        
            return HttpResponse('登录失败！')
```