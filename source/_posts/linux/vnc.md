title: vnc
categories:
  - linux
tags:
  - remote desktop
date: 2021-07-17 11:23:12
---


{% codeblock "服务端安装" lang:sh %}

# ubuntu 
  sudo apt-get install x11vnc

  x11vnc -storepasswd

  x11vnc -auth guess -once -loop -noxdamage -repeat -rfbauth ~/.vnc/passwd -rfbport 5900 -shared

  x11vnc -forever

  https://www.realvnc.com/en/connect/download/viewer/


# arch 
    yay -S x11vnc net-tools
    update -> /etc/gdm/custom.conf:
        WaylandEnable=false

    x11vnc -wait 50 -noxdamage -passwd PASSWORD -display :0 -forever -o /var/log/x11vnc.log -bg 
{% endcodeblock %}

{% codeblock "客户端" lang:sh %}
https://www.realvnc.com/
{% endcodeblock %}
