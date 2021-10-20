---
title: Git
draft: true
categories:
  - linux
tags:
  - git
date: 2021-07-10 00:00:00
---

#### generate public key
  ``` shell
  git config --global user.name ""
  git config --global user.email ""
  ssh-keygen -t rsa -b 4096 -C ""
```
#### git config
```sh
  git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
  git config --global https.https://github.com.proxy socks5://127.0.0.1:1080

  # or vi ~/.gitconfig

  [http "https://github.com"]
    proxy = socks5://127.0.0.1:1080
    postBuffer = 524288000
  [https "https://github.com"]
    proxy = socks5://127.0.0.1:1080
    postBuffer = 524288000
  ```

#### git submodule

```sh
git submodule add https://github.com/liuyib/hexo-theme-stun/ themes/stun

git submodule update --remote

```
