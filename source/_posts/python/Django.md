---
title: Django
author: ycm76229@gmail.com
tags: []
categories:
  - python
date: 2021-07-23 15:11:00
---

#### 在script中使用Django model
```python
import os
import django
from proxyip.models import ProxyIP

os.environ['DJANGO_SETTINGS_MODULE'] = 'dj_project.settings'
django.setup()

p = ProxyIP(ip='192.168.50.1')
p.save()
print(ProxyIP.objects.all())

python manage.py shell < main.py
```

#### django 导出导入数据
```python
python manage.py dumpdata (myapp) > myapp.json

python manage.py loaddata myapp.json
```
