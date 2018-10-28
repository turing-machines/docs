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
- Setup /etc/default/isc-dhcp-server
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

## Verification

{{% notice warning %}}
WIP: The connection to the PAN is still kind of unstable
{{% /notice %}}


On the laptop, under the bluetook icon, use the **Join Personal Area Network**.
If the worker PI and the master PI are configured properly (dhcpd, network/eth0,pan0)
the worker PI and master PI will acts as routers. The worker PI will provide the laptop with an IP address in the **192.168.1xx.0/255** range.

![](/images/networks/pan0_pict2.png)

SSH to the node.
```bash
ssh 192.168.1xx.1 -l pirate
```

On your PC itself, open a command prompt or cygwin
```bash
ipconfig /all
```
![](/images/networks/pan0_pict1.png)

If the previous test is successful, the Name Server list should contain the IP and your home router, and you should be able
to surf the internet.

{{% notice note %}}
Notice the IP address of the home router *192.168.1.1* in the DNS server list
{{% /notice %}}

## Reference Links

{{% notice note %}}
WIP
{{% /notice %}}
