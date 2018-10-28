---
layout: post
title:  "Setting up PAN"
menuTitle:  "PAN"
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

This tutorial how to setup PAN on the slave pi to simulator LTE and eLTE RAN.

<!--more-->

## Key Aspects

- Setup /etc/network/interfaces.d/pan0.
- Setup /etc/dhcpcd.conf 
- Check /etc/resolv.conf

## Deploy

{{% notice note %}}
Also the Kubedge team went through the process, it has not been documented yet. Still some example files are available bellow.
{{% /notice %}}

- [pan0](https://github.com/kubedge/kube-rpi/blob/master/config/cluster2/hypriotos/nas-pi/etc/network/interfaces.d/pan0)
- [dhcpcd](https://github.com/kubedge/kube-rpi/blob/master/config/cluster2/hypriotos/nas-pi/etc/dhcpcd.conf)

## Conclusion

{{% notice note %}}
WIP
{{% /notice %}}

## Reference Links

{{% notice note %}}
WIP
{{% /notice %}}
