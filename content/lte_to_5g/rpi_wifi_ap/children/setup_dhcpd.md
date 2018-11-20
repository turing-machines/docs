---
layout: post
title:  "Setting up DHCPD on 5G NR Node"
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
internet through the AP & NAT running on 5G NR simulating PI. This tutorial
also describe how to setup the DHCPD to automatically allocated IPs to UE or PCs.

<!--more-->

## Key Aspects

- Setup /etc/dhcp/dhcpd.conf.
- Setup /etc/default/isc-dhcp-server
- Setup /etc/systcl.conf
- Setup /etc/dhcpcd.conf

## Deploy

{{% notice note %}}
Also the Kubedge team went through the process, it has not been documented yet. Still some example files are available bellow.
{{% /notice %}}

- [dhcpd](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kube-node02/etc/dhcp/dhcpd.conf)
- [isc-dhcp-server](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kube-node02/etc/default/isc-dhcp-server)
- [systemctl](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kube-node02/etc/sysctl.conf)
- [dhcpcd](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kube-node02/etc/dhcpcd.conf)

## Verification

On the laptop, under the wifi icon, join a network **xxx@kubedge** network
If the worker PI and the master PI are configured properly (dhcpd, network/eth0,pan0)
the worker PI and master PI will acts as routers. The worker PI will provide the laptop with an IP address in the **192.168.0xx.0/255** range.

![](/images/networks/wlan0_pict1.png)

SSH to the node.
```bash
ssh 192.168.0xx.1 -l pirate
```

On your PC itself, open a command prompt or cygwin
```bash
ipconfig /all
```
![](/images/networks/wlan0_pict2.png)

{{% notice note %}}
Notice the IP address of the home router *192.168.1.1* in the DNS server list
{{% /notice %}}

If the previous test is successful, the Name Server list should contain the IP and your home router, and you should be able
to surf the internet.

![](/images/networks/wlan0_pict3.png)


## Reference Links

{{% notice note %}}
WIP
{{% /notice %}}
