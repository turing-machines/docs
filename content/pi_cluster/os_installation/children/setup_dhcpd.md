---
layout: post
title:  "Setting up DHCPD on master PI"
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

This tutorial how to setup DHCPD and NAT so that the slave PI can access the 
internet through the NAT (ETH0->WLAN0) running on Master PI. This tutorial
also describe how to setup the DHCPD to automatically allocated IPs to PI or PCs.

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

- [dhcpd](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kubemaster-pi/etc/dhcp/dhcpd.conf)
- [isc-dhcp-server](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kubemaster-pi/etc/default/isc-dhcp-server)
- [systemctl](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kubemaster-pi/etc/sysctl.conf)
- [dhcpcd](https://github.com/kubedge/kube-rpi/blob/master/config/cluster1/hypriotos/kubemaster-pi/etc/dhcpcd.conf)

## Verification

{{% notice note %}}
This is where is important to have a 5 ports switch for a 3 nodes cluster , and a 8 ports switch for a 5 nodes cluster.
{{% /notice %}}

{{<mermaid>}}
sequenceDiagram
    participant PC
    participant MasterPI
    participant Internet
    PC->>MasterPI: Get IP
    MasterPI->>PC: Return IP in 192.168.2.x
    PC->>MasterPI: eth0 IP traffic
    loop kernel
        MasterPI->MasterPI: eth0 - wlan0 
    end
    MasterPI->>Internet: wifi IP traffic
    Internet->>MasterPI: IP traffic
    MasterPI->>PC: IP traffic
{{< /mermaid >}}

Plug your laptop onto the switch using an ethernet cable. If the master PI is configured properly (dhcpd, network/eth0..),
the master PI will acts as a router. It will provide the laptop with an IP address in the **192.168.2.0/255** range.

![](/images/networks/eth0_pict1.png)

SSH to the node.
```bash
ssh 192.168.2.1 -l pirate
```

On your PC itself, open a command prompt or cygwin
```bash
ipconfig /all
```
![](/images/networks/eth0_pict2.png)

If the previous test is successful, the Name Server list should contain the IP and your home router, and you should be able
to surf the internet.

![](/images/networks/eth0_pict3.png)

## Reference Links

{{% notice note %}}
WIP
{{% /notice %}}
