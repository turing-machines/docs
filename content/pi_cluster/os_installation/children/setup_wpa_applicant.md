---
layout: post
title:  "Setting up WPA supplicant"
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

- [wpa_supplicant](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kubemaster-pi/etc/wpa_supplicant/wpa_supplicant.conf)
- [wlan0](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kubemaster-pi/etc/network/interfaces.d/wlan0)
- [dhcpcd](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kubemaster-pi/etc/dhcpcd.conf)

## Conclusion

{{% notice note %}}
WIP
{{% /notice %}}

## Reference Links

{{% notice note %}}
WIP
{{% /notice %}}
