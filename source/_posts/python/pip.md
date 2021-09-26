---
title: Pip
draft: true
categories:
  - python
date: 2021-07-10 00:00:00
---

### virtualenv 
```sh
(sudo) pip install virtualenv
virtualenv -p /usr/bin/python3.7 ~/.virtualenv/py3
# pip freeze > requirements.txt
```

### pipenv
```sh
alias pv='pipenv run python'
alias pi='pipenv run pip install '
```

### pip.conf

- ##### 一次
```sh
pip install web.py -i http://pypi.douban.com/simple --trusted-host pypi.douban.com
```
- ##### 全局

```sh
# 清华源
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
# 阿里源
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
# 腾讯源
pip config set global.index-url http://mirrors.cloud.tencent.com/pypi/simple
# 豆瓣源
pip config set global.index-url http://pypi.douban.com/simple/

or

# linux:`~/.pip/pip.conf`
# windows:`%HOMEPATH%\pip\pip.ini）`
[global]
  index-url = http://mirrors.aliyun.com/pypi/simple/
[install]
  trusted-host=mirrors.aliyun.com
```

### error: 
- ##### locale.Error: unsupported locale setting
```sh
export LC_ALL=C
```
