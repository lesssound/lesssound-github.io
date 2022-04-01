---
title: git && ssh
draft: true
categories:
  - linux
tags:
  - git
  - ssh
updated: 2022-04-01 09:40:00
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

## ssh config

#### $HOME/.ssh/config
```sh
Host archServer
    HostName 192.168.xx.xx
    User xxx
    Port xxx
    # use ipv4
    # AddressFamily inet
    IdentitiesOnly yes
    IdentityFile ~/.ssh/id_rsa
    ServerAliveInterval 120
    
# 转发跳板机端口
# ssh -tt -i ./id_rsa -L 0.0.0.0:local_port:host2:host2_port user@host1

# 上传共钥到目标服务器
# ssh-copy-id -i ~/.ssh/id_rsa.pub archServer

# 转发服务器到本机的1082端口
# ssh -D 1082 -f -C -q -N archServer
```
