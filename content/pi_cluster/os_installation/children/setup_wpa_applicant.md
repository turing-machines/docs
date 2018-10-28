---
layout: post
title:  "Setting up WPA supplicant on Master PI"
menuTitle:  "WPA supplicant"
weight: 15
date:   2018-09-01
categories: [wiki, wip]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [wpa_supplicant, rpi]
published: true
---

This tutorial how to setup WIFI on the master pi to connect to different WLAN 

<!--more-->

## Key Aspects

- Setup /etc/wpa_supplicant/wpa_supplicant.
- Setup /etc/network/interfaaces.d/wlan0.
- Setup /etc/dhcpcd.conf 
- Check /etc/resolv.conf

## Deploy

{{% notice note %}}
Also the Kubedge team went through the process, it has not been documented yet. Still some example files are available bellow.
{{% /notice %}}

### Enable WLAN0.

Check the IP address. Depending on PI3B or PI3B+, the WLAN network may be different.
Use the files in **$HOME/proj/kubedge/kube-rpi/config/cluster1/hypriotos/** as examples.

~~~
ip a
iwconfig
sudo ip link set wlan0 up
sudo iwlist scan | grep ES
sudo iwlist scan | grep ED
wpa_passphrase <sommessid>
sudo vi /etc/network/interfaces.d/wlan0
sudo vi /etc/wpa_supplicant/wpa_supplicant.conf
sudo systemctl restart dhcpcd 
~~~

### Examples of files

- [wpa_supplicant](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kubemaster-pi/etc/wpa_supplicant/wpa_supplicant.conf)
- [wlan0](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kubemaster-pi/etc/network/interfaces.d/wlan0)
- [dhcpcd](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kubemaster-pi/etc/dhcpcd.conf)

## Conclusion

At that point you should be able to unplug the eth0 cable, reboot the PI and check in your router for a **kubemaster-pi** and ssh into the node.
It should allow you access the kubemaster-pi using WIFI.

{{% notice note %}}
WIP
{{% /notice %}}

## Reference Links

{{% notice note %}}
WIP
{{% /notice %}}
