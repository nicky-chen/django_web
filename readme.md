#Django 教程

**环境安装**

下载包 [Django-1.10.8.tar.gz](https://pypi.org/project/Django/1.10.8/#files) 

````
解压并进入目录，命令行 python setup.py install 安装

检查是否安装成功 命令行 python ->  import django -> django.VERSION

添加环境变量 Path下添加 django 安装目录 C:\Python27\Lib\site-packages\Django-1.10.8-py2.7.egg\django
添加 django 的脚本目录 C:\Python27\Scripts
````


**创建web项目**

````
新建项目的父级目录  mkdir django_web

新建web工程： cd django_web ->  django-admin-script.py startproject website   ------ website 工程名

修改 django_web\website\website 下的settings.py 和 urls.py 文件 

settings.py:
修改 TIME_ZONE = 'Asia/Shanghai'  创建一个blog网站 django-admin-script.py startapp blog

INSTALLED_APPS下添加一个blog

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog',
]


urls.py:
加入web地址 url(r'^blog/index/$', views.index)表示正则regex 匹配到 以blog/index 为开始和结束的链接，
跳转到index方法上，注意 1.10版本以后需要引入  from blog import views


from blog import views

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^blog/index/$', views.index),
]


进入 blog 文件夹 创建视图模版的文件夹 templates  mkdir templates  将index.html网页放入其中

修改 blog 下的 views.py

from django.shortcuts import render
from django.http import HttpResponse
from django.template import loader, Context
# Create your views here.

def index(request):
   //加载器获取视图模版
    t = loader.get_template("index.html")
    //向模版发送数据 这么没有传入为空
    c = Context({}) 
    //渲染
    return HttpResponse(t.render(c))

启动 blog网站内置测试服务器：website目录下输入命令行  .\manage.py runserver

````