title: Ssh
draft: true
categories:
  - linux
tags:
  - ssh
date: 2021-07-10 00:00:00
---
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