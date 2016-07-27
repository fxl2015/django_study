һ�����ȣ��½�һ����Ŀ(project), ����Ϊ mysite
django-admin startproject mysite
��ע��
1. ��� django-admin ���У����� django-admin.py
2. �������Linux����Դ�밲װ�ģ������� pip ��װ�ģ�Ҳ����  django-admin.py ����

��, �½�һ��Ӧ��(app), ���ƽ� learn
python manage.py startapp learn # learn ��һ��app������
�������¶����app�ӵ�settings.py�е�INSTALL_APPS��

�޸� mysite/mysite/settings.py
INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'learn',
)
��ע,��һ���Ǹ�ʲô��? 
�½��� app ������ӵ� INSTALL_APPS �еĻ�, 
django �Ͳ����Զ��ҵ�app�е�ģ���ļ�(app-name/templates/�µ��ļ�)�;�̬�ļ�(app-name/static/�е��ļ�) , 
�������ѧϰ�����Ƿֱ�������ʲô.

����������ͼ����������ҳ��ʱ�����ݣ�
������learn���Ŀ¼��,��views.py��,�޸����е�Դ����,�ĳ������
#coding:utf-8
from django.http import HttpResponse
def index(request):
    return HttpResponse(u"��ӭ���� ��ǿѧ��!")
	
�ģ�������ͼ������ص�URL(��ַ)  �����涨 ����ʲô��ַ��Ӧʲô���ݣ�
���Ǵ� mysite/mysite/urls.py ����ļ�, �޸����еĴ���:


���� Django �汾�� urls.py ������һЩ���ģ�

Django 1.7.x �����µ�ͬѧ���ܿ������������ģ�
from django.conf.urls import patterns, include, url
 
from django.contrib import admin
admin.autodiscover()
 
urlpatterns = patterns('',
    url(r'^$', 'learn.views.index'),  # new
    # url(r'^blog/', include('blog.urls')),
 
    url(r'^admin/', include(admin.site.urls)),
)
Django 1.8.x�����ϣ�Django �ٷ���������˵Ҫ�������룬��ʹ�ã�
from django.conf.urls import url
from django.contrib import admin
from learn import views as learn_views  # new
 
urlpatterns = [
    url(r'^$', learn_views.index),  # new
    url(r'^admin/', admin.site.urls),
]

�壬���ն������� python manage.py runserver ���ǻῴ�������������Ϣ:
$ python manage.py runserver
Performing system checks...
System check identified no issues (0 silenced).
You have unapplied migrations; your app may not work properly until they are applied.
Run 'python manage.py migrate' to apply them.
December 22, 2015 - 11:57:33
Django version 1.9, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
���Ǵ������,���� http://127.0.0.1:8000/