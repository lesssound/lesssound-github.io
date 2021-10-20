title: Django
author: ycm76229@gmail.com
categories:
  - python
tags:
  - django
date: 2021-07-23 15:11:00
---

{% codeblock "在script中使用Django model" lang:sh %}
import os
import django
from proxyip.models import ProxyIP

os.environ['DJANGO_SETTINGS_MODULE'] = 'dj_project.settings'
django.setup()

p = ProxyIP(ip='192.168.50.1')
p.save()
print(ProxyIP.objects.all())

python manage.py shell < main.py
{% endcodeblock %}

{% codeblock "django 导出导入数据" lang:sh %}
python manage.py dumpdata (myapp) > myapp.json

python manage.py loaddata myapp.json
{% endcodeblock %}
