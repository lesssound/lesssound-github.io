title: python
categories:
  - python
date: 2021-06-17 11:30:22
tags:
---
#### install on deepin
```python
./configure --with-ssl --enable-loadable-sqlite-extensions --enable-optimizations && make && sudo make install
```

#### 乘法表 
```python
print ('\n'.join([' '.join(['%s*%s=%-2s' % (y,x,x*y) for y in range(1,x+1)]) for x in range(1,10)]))
```

#### json
```python
json.dumps(item, ensure_ascii=False, indent=4)
```

#### 对字典排序
```python
sorted(_dict.items(), key=lambda d: d[1], reverse=False)
```
#### unicode replace
```python
repr()
```

#### http server
```sh
py2 python -m SimpleHTTPServer 8000
py3 python -m http.server 8000
```

#### 格式化输出
```python
print("{:02d}".format(1))
print(f"{1:02d}")
```


#### datetime
```python
pip install python-dateutil

from datetime import datetime
from dateutil import parser

t = "Thu, 9 Sep 2021 00:17:59"
result = parser.parse(t)
print(result)
print(type(result))

now = datetime.now()
print((now - result).days)

```