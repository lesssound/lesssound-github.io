---
title: Ssh
draft: true
categories:
  - linux
date: 2021-07-10 00:00:00
---


## ssh/config
```sh
Host virtual
    HostName xxx
    User xxx
    IdentitiesOnly yes
    IdentityFile ~/.ssh/id_rsa
    ServerAliveInterval 120
# ssh-copy-id -i ~/.ssh/id_rsa.pub virtual
# ssh -D 1082 -f -C -q -N xx
```
