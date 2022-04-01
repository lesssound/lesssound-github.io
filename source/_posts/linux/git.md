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

## git config
{% codeblock "generate public key" lang:sh %}
  git config --global user.name ""
  git config --global user.email ""
  ssh-keygen -t rsa -b 4096 -C ""
{% endcodeblock %}

{% codeblock "git config" lang:sh %}
  git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
  git config --global https.https://github.com.proxy socks5://127.0.0.1:1080

  # or vi ~/.gitconfig
  [http "https://github.com"]
    proxy = socks5://127.0.0.1:1080
    postBuffer = 524288000
  [https "https://github.com"]
    proxy = socks5://127.0.0.1:1080
    postBuffer = 524288000
{% endcodeblock %}

{% codeblock "git submodule" lang:sh %}
git submodule add https://github.com/liuyib/hexo-theme-stun/ themes/stun
git submodule update --remote
{% endcodeblock %}

## ssh config

{% codeblock "$HOME/.ssh/config" lang:sh %}
Host github
   HostName github.com
   User git
   # 走 HTTP 代理
   # ProxyCommand socat - PROXY:127.0.0.1:%h:%p,proxyport=8080
   # 走 socks5 代理
   ProxyCommand nc -v -x 127.0.0.1:1080 %h %p


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
ssh -tt -i ./id_rsa -L 0.0.0.0:local_port:host2:host2_port user@host1

# 上传共钥到目标服务器
ssh-copy-id -i ~/.ssh/id_rsa.pub archServer

# 转发服务器到本机的1082端口
ssh -D 1082 -f -C -q -N archServer
{% endcodeblock %}
