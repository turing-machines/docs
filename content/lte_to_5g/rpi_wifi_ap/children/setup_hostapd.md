---
layout: post
title:  "Setting up HOSTAPD on 5G NR node"
menuTitle:  "HOSTAPD"
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

This tutorial how to setup WIFI AccessPoint on PI simulating 5G NR node

<!--more-->

## Key Aspects

- Setup /etc/network/interfaces.d/wlan0.
- Setup /etc/dhcpcd.conf
- Check /etc/resolv.conf

## Deploy

{{% notice note %}}
Also the Kubedge team went through the process, it has not been documented yet. Still some example files are available bellow.
{{% /notice %}}

- [wlan0](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kube-node02/etc/network/interfaces.d/wlan0)
- [dhcpcd](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kube-node02/etc/dhcpcd.conf)
- [hostapd](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kube-node02/etc/hostapd/hostapd.conf)

## Conclusion

{{% notice note %}}
WIP
{{% /notice %}}

## Reference Links

{{% notice note %}}
WIP
{{% /notice %}}
