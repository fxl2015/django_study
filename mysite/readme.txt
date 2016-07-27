一，首先，新建一个项目(project), 名称为 mysite
django-admin startproject mysite
备注：
1. 如果 django-admin 不行，请用 django-admin.py
2. 如果是在Linux是用源码安装的，或者用 pip 安装的，也是用  django-admin.py 命令

二, 新建一个应用(app), 名称叫 learn
python manage.py startapp learn # learn 是一个app的名称
把我们新定义的app加到settings.py中的INSTALL_APPS中

修改 mysite/mysite/settings.py
INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'learn',
)
备注,这一步是干什么呢? 
新建的 app 如果不加到 INSTALL_APPS 中的话, 
django 就不能自动找到app中的模板文件(app-name/templates/下的文件)和静态文件(app-name/static/中的文件) , 
后面你会学习到它们分别用来干什么.

三，定义视图函数（访问页面时的内容）
我们在learn这个目录中,把views.py打开,修改其中的源代码,改成下面的
#coding:utf-8
from django.http import HttpResponse
def index(request):
    return HttpResponse(u"欢迎光临 自强学堂!")
	
四，定义视图函数相关的URL(网址)  （即规定 访问什么网址对应什么内容）
我们打开 mysite/mysite/urls.py 这个文件, 修改其中的代码:


由于 Django 版本对 urls.py 进行了一些更改：

Django 1.7.x 及以下的同学可能看到的是这样的：
from django.conf.urls import patterns, include, url
 
from django.contrib import admin
admin.autodiscover()
 
urlpatterns = patterns('',
    url(r'^$', 'learn.views.index'),  # new
    # url(r'^blog/', include('blog.urls')),
 
    url(r'^admin/', include(admin.site.urls)),
)
Django 1.8.x及以上，Django 官方鼓励（或说要求）先引入，再使用：
from django.conf.urls import url
from django.contrib import admin
from learn import views as learn_views  # new
 
urlpatterns = [
    url(r'^$', learn_views.index),  # new
    url(r'^admin/', admin.site.urls),
]

五，在终端上运行 python manage.py runserver 我们会看到类似下面的信息:
$ python manage.py runserver
Performing system checks...
System check identified no issues (0 silenced).
You have unapplied migrations; your app may not work properly until they are applied.
Run 'python manage.py migrate' to apply them.
December 22, 2015 - 11:57:33
Django version 1.9, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
我们打开浏览器,访问 http://127.0.0.1:8000/