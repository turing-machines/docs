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

- Setup /etc/wpa_supplicant/wpa_supplicant
- Setup /etc/network/interfaces.d/wlan0
- Setup /etc/dhcpcd.conf
- Setup /etc/resolv.conf.tail
- Check /etc/resolv.conf

## Deploy

{{% notice note %}}
Also the Kubedge team went through the process, it has not been documented yet. Still some example files are available bellow.
{{% /notice %}}

Install dhcpcd5. The dhcpcd service controls the start of the interfaces as well as the creation of the /etc/resolv.conf

### Install DHCPCD

```bash
sudo apt-get install dhcpcd5
```

The /etc/dhcpcd.conf (not the /etc/dhcpd/dhcpd.conf) controls the startup of the interfaces. We want the eth0 to be kind of static, the wlan0 to be dynamic

```bash
diff dhcpcd.conf /home/pirate/proj/kubedge/kube-rpi/config/cluster1/hypriotos/kubemaster-pi/etc/dhcpcd.conf
```

### Prepare lo and eth0

You can keep 3 files in the /etc/network/interfaces.d: l0, eth0 and wlan0.
Note comment out the iptables line at first in the eth0 file. eth0 is static so that the internal IP of the master PI is always 192.168.2.1

```bash
diff lo /home/pirate/proj/kubedge/kube-rpi/config/cluster1/hypriotos/kubemaster-pi/etc/network/interfaces.d/lo
diff eth0 /home/pirate/proj/kubedge/kube-rpi/config/cluster1/hypriotos/kubemaster-pi/etc/network/interfaces.d/eth0
```

### Enable WLAN0.

In wlan0 the list of the sssid you want to potentially connect to. Needs to match the id_str in the wpa_supplicant.conf
```bash
vi wlan0
vi /etc/wpa_supplicant/wpa_supplicant.conf
```

Check the IP address. Depending on PI3B or PI3B+, the WLAN network may be different.
Use the files in **$HOME/proj/kubedge/kube-rpi/config/cluster1/hypriotos/** as examples.

```bash
ip a
iwconfig
sudo ip link set wlan0 up
sudo iwlist scan | grep ES
sudo iwlist scan | grep ED
wpa_passphrase <sommessid>
sudo vi /etc/network/interfaces.d/wlan0
sudo vi /etc/wpa_supplicant/wpa_supplicant.conf
sudo systemctl restart dhcpcd 
```
At that point the wlan0 should come up and IP 192.168.2.1 should be assigned to the master-pi.

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
