# formcurd 增删改查

<a name="formcurd"></a>
### formcurd

<br />[![](https://cdn.nlark.com/yuque/0/2020/svg/486920/1594719979810-2b872424-51ad-4b1f-881c-a0f4a8f138c3.svg#align=left&display=inline&height=20&margin=%5Bobject%20Object%5D&originHeight=20&originWidth=120&size=0&status=done&style=none&width=120)]()[![](https://cdn.nlark.com/yuque/0/2020/svg/486920/1594720004966-b1063aa0-5e62-4fef-8975-1228a488b230.svg#align=left&display=inline&height=20&margin=%5Bobject%20Object%5D&originHeight=20&originWidth=98&size=0&status=done&style=none&width=98)]()<br />
<br />formcurd 是一个帮助 `Django` 项目实现快速增删改查的组件。集成了组合搜索，关键字搜索，快速排序，批量操作、分页等功能，同时预留了大量钩子函数使定制化开发更加快速。再也不用担心处理各类表格的场景。<br />

<a name="1a82206a"></a>
### 如何快速用到你的 `Django` 项目中

<br />**第1步：** formcurd 注册到你的 `Django` 项目中<br />
<br />`settings.py`<br />

```python
'formcurd.apps.FormcurdConfig',
```

<br />**第2步：** formcurd 加到项目路由中<br />
<br />`urls.py`<br />

```python
from formcurd.service.formcurd import site

urlpatterns = [
    # path('admin/', admin.site.urls),

    url(r'^formcurd/', site.urls),

]
```

<br />**第3步：** 准备好 app 视图<br />
<br />`views/Uatfzenv.py`<br />

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

<br />**第4步：** app 中注册 formcurd 组件<br />
<br />`app/formcurd.py`<br />

```python
# _*_ encoding=utf-8 _*_

__author__ = 'weizhen'

from formcurd.service.v1 import site
from formcurd.service.v1 import FormcurdHandler
from release.views import Uatfzenv

site.register(models.UatFzenv, Uatfzenv.UatFzenvHandler)
```


<a name="a1e95935"></a>
### 案例分享

<br />请参考本人另外一个项目 [ScheduOps](https://github.com/gongwz/ScheduOps.git)<br />

<a name="475791f7"></a>
### Demo 截图
![image.png](https://cdn.nlark.com/yuque/0/2020/png/486920/1594720067079-957d3b85-c222-4919-b73b-5f0b602d151a.png#align=left&display=inline&height=392&margin=%5Bobject%20Object%5D&name=image.png&originHeight=798&originWidth=1514&size=102246&status=done&style=none&width=743)<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/486920/1594720090446-cbf4c281-6bb4-4f69-8a6e-c013b3a3f381.png#align=left&display=inline&height=310&margin=%5Bobject%20Object%5D&name=image.png&originHeight=629&originWidth=1503&size=77892&status=done&style=none&width=741)<br />![image.png](https://cdn.nlark.com/yuque/0/2020/png/486920/1594720114018-a750f5e2-9ccf-4afd-9d8e-31117f1fef88.png#align=left&display=inline&height=384&margin=%5Bobject%20Object%5D&name=image.png&originHeight=768&originWidth=1507&size=87945&status=done&style=none&width=753.5)
<a name="d40e4c26"></a>
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



> Author: 卫振 （weizhen）  -- 最近一直在用阿里的语雀，当图床还挺快  ^_-

