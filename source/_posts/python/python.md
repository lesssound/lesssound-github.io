title: python
categories:
  - python
tags:
  - python
date: 2021-06-17 11:30:22
---
{% codeblock "code" lang:python %}

# mysql-clients
```sh
yay -S --noconfirm mysql-clients gcc
pip install mysqlclient
```

# json
json.dumps(item, ensure_ascii=False, indent=4)

# 对字典排序
sorted(_dict.items(), key=lambda d: d[1], reverse=False)

# unicode replace
repr()

# http server
py2 python -m SimpleHTTPServer 8000
py3 python -m http.server 8000

# 格式化输出
print("{:02d}".format(1))
print(f"{1:02d}")

# datetime
pip install python-dateutil

from datetime import datetime
from dateutil import parser

t = "Thu, 9 Sep 2021 00:17:59"
result = parser.parse(t)
print(result)
print(type(result))

now = datetime.now()
print((now - result).days)

# csv
import csv

my_dict = {"test": 1, "testing": 2}
with open('mycsvfile.csv', 'w') as f:  # You will need 'wb' mode in Python 2.x
    w = csv.DictWriter(f, my_dict.keys())
    w.writeheader()
    w.writerow(my_dict)
    # w.writerows(my_dict)

# xmljson
import xmljson
from lxml.etree import  fromstring,tostring

json.loads(json.dumps(xmljson.badgerfish.data(fromstring(con.encode()))))

# 乘法表 
print ('\n'.join([' '.join(['%s*%s=%-2s' % (y,x,x*y) for y in range(1,x+1)]) for x in range(1,10)]))

{% endcodeblock %}