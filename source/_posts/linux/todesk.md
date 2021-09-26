---
title: 远程桌面
categories:
  - linux
date: 2021-07-28 15:00:32
---


#### arch install todesk 

```sh
wget https://dl.todesk.com/linux/todesk_2.0.2_x86_64.pkg.tar.zst

sudo pacman -U todesk_2.0.2_x86_64.pkg.tar.zst

sudo systemctl restart todeskd.service
```


详情参考: https://www.todesk.com/download_detail.html
