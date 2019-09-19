### formcurd

[![pyversions](https://img.shields.io/badge/python-3.5,3.6,3.7-blue.svg)]()
    [![pyversions](https://img.shields.io/badge/Django-2.0,2.1-green.svg)]()

formcurd 是一个帮助 `Django` 项目实现快速增删改查的组件。集成了组合搜索，关键字搜索，快速排序，批量操作、分页等功能，同时预留了大量钩子函数使定制化开发更加快速。再也不用担心处理各类表格的场景。

### 如何快速用到你的 `Django` 项目中

**第1步：** formcurd 注册到你的 `Django` 项目中

`settings.py`

```python
'formcurd.apps.FormcurdConfig',
```

**第2步：** formcurd 加到项目路由中

`urls.py`

```python
from formcurd.service.formcurd import site

urlpatterns = [
    # path('admin/', admin.site.urls),

    url(r'^formcurd/', site.urls),

]

```

**第3步：** 准备好 app 视图

`views/Uatfzenv.py`

```python
# _*_ encoding=utf-8 _*_

__author__ = 'weizhen'

from django.shortcuts import render, HttpResponse, redirect
from formcurd.service.v1 import FormcurdHandler

from release.models import UatFzenv as JobModel

class UatFzenvHandler(FormcurdHandler):
    list_display = ['app_name','svn_num',jira_url,display_action]
    
    search_list = ['app_name__contains',]

    search_group = [
        Option(field='job_template'),
    ]

```


**第4步：** app 中注册 formcurd 组件

`app/formcurd.py`

```python
# _*_ encoding=utf-8 _*_

__author__ = 'weizhen'

from formcurd.service.v1 import site
from formcurd.service.v1 import FormcurdHandler
from release.views import Uatfzenv

site.register(models.UatFzenv, Uatfzenv.UatFzenvHandler)
```

### Demo

![](http://192.168.24.68/static/imgs/formcurd-host.png)

![](http://192.168.24.68/static/imgs/formcurd-list.png)

### 相关知识点
- inclusion_tag
- yield
- urlencode
- _meta.model_name
- _meta.app_label
- functools
- wraps
- request
- mark_safe
- order_by
- autodiscover_module
- Q查询
- xss攻击
- 深浅拷贝 
- 生成器 
- 装饰器
- ModelForm组件
- 偏函数，partial
- 反射 getattr(row,'name')
- 分页（保留原搜索条件） 
- 钩子函数的思路：预留可扩展位置
- 单例模式：对象共用一堆数据的时候
- 路由分发的名称空间，别名反向解析
- QueryDict对象默认不可改 _mutable=True 
- 反向生成URL：reverse('namespace:xxx')
- 面向对象的继承深入


>Author: 卫振 （weizhen）  