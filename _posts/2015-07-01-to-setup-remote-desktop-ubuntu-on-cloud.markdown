---
layout: post
title:  "Setup remote desktop for ubuntu on aws or softlayer"
date:   2015-07-01 03:02:30
categories: ubuntu linux
---

{% highlight bash %}
sudo apt-get install x11vnc
{% endhighlight %}

{% highlight bash %}
ssh devUser@119.81.232.29 -L 5900:localhost:5900 "x11vnc -display :1 -noxdamage"
{% endhighlight %}

````
sudo apt-get install x11vnc
sudo apt-get install ubuntu-desktop
````
it will create a directory under ~/.vnc

To start or stop vncserver
````
vncserver -kill :1
vncserver :1
````
it will eventually run the ~/.vnc/xstartup 

There is an ongoing bug with ubuntu 14, it will only be fixed on ubuntu 15, gnome-session will not be able to start on macine that does not have hardware graphic exceleration.
You can check the logs, at
~/.vnc/ubuntu:1.log 

````
gnome-session-is-accelerated: No composite extension.
gnome-session-check-accelerated: Helper exited with code 256
gnome-session[31854]: WARNING: software acceleration check failed: Child process exited with code 1
gnome-session[31854]: CRITICAL: We failed, but the fail whale is dead. Sorry....
````

the workaround is not to use gnome-sesssion but to use 

Telling me to give up on GNOME (happy to do so). Got everything working fine with xfce instead:

sudo apt-get install xfce4

Then changed my .vnc/xstartup to:

#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
startxfce4 &