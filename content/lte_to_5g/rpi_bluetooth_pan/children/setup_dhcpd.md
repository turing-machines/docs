---
layout: post
title:  "Setting up DHCPD on LTE & eLTE Node"
menuTitle:  "DHCPD & NAT"
weight: 20
date:   2018-09-01
categories: [wiki, wip]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [dhcpd, rpi]
published: true
---

This tutorial how to setup DHCPD and NAT so that the UE can access the 
internet through the AP & NAT running on LTE & eLTE simulating PI. This tutorial
also describe how to setup the DHCPD to automatically allocated IPs to UE or PCs.

<!--more-->

## Key Aspects

- Setup /etc/dhcp/dhcpd.conf.
- Setup /etc/default/isc-server
- Setup /etc/systcl.conf 
- Setup /etc/dhcpcd.conf 

## Deploy

{{% notice note %}}
Also the Kubedge team went through the process, it has not been documented yet. Still some example files are available bellow.
{{% /notice %}}

- [dhcpd](https://github.com/kubedge/kube-rpi/blob/master/config/cluster2/hypriotos/nas-pi/etc/dhcp/dhcpd.conf)
- [isc-dhcp-server](https://github.com/kubedge/kube-rpi/blob/master/config/cluster2/hypriotos/nas-pi/etc/default/isc-dhcp-server)
- [systemctl](https://github.com/kubedge/kube-rpi/blob/master/config/cluster2/hypriotos/nas-pi/etc/sysctl.conf)
- [dhcpcd](https://github.com/kubedge/kube-rpi/blob/master/config/cluster2/hypriotos/nas-pi/etc/dhcpcd.conf)

## Conclusion

{{% notice note %}}
WIP
{{% /notice %}}

## Reference Links

{{% notice note %}}
WIP
{{% /notice %}}
