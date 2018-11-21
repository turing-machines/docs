---
layout: post
title:  "OS Installation on Worker PI"
menuTitle: "OS on Worker PI"
weight: 25
date:   2018-07-07
categories: [wiki]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [ansible, hypriot, rpi]
published: true
---

This page describes simple steps to install the OS (HypriotOS) on the PIs.

<!--more-->

## Overview

Kubedge uses HypriotOS because the quickest to set up. SSH and Docker supported by default

## OS on worker/slave PI

{{% notice warning %}}
If your NAT setup was successfull on the master PI, it is time to push the SD card on the worker PIs,
plug them to the ethernet switch and enable the power.
{{% /notice %}}

### Access the node

- Insert the SD card in the worker PI and power it on.
- SSH to the master PI.
- From the master PI, ssh to the new PI. And IP address in 192.168.2.1xx will have been assigned to the new node.

### Freeze your configuration

Cloud init is perfect for the first boot. Once the node
is up, it can be challenging not to preserve the fine tuning done
to the OS.

```bash
sudo apt-get remove --purge cloud-init
sudo apt-get autoremove
```

### Update OS

Let's update to the latest version

```bash
sudo apt-get update
sudo apt-get upgrade
```

Gain access to latest docker-ce

```bash
sudo -i

curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
usermod -aG docker pirate
```

At the time this article is written 18.09 is not supported yet.

```bash
sudo apt-cache policy docker-ce
sudo apt-get remove --purge docker-ce
sudo apt-get autoremove

sudo apt-get install docker-ce=18.06.1~ce~3-0~debian
```

### Update worker PI name

As root, replace **black-pearl** by **kube-nodeXX**, in the two following files:

```bash
sudo -i

vi /etc/hosts
```

It seems on HypriotOS 64, you need to do

```bash
sudo hostnamectl set-hostname kubemaster-pi
```

{{% notice warning %}}
The /etc/resolv.conf on the new node should contain the IP address of your home router if dhcpd is setup properly
on your master node.
{{% /notice %}}


### Update the static IP on the master PI

It is important to edit the dhcpd.conf file in order to enfore the same internal IP address on the 192.168.2.x network
every time the cluster is rebooted. Be sure to check then isc-dhcp-server is still working and that you need not
corrupt the configuration file.

```bash
arp -a

sudo vi /etc/dhcpd/dhcpd.conf

sudo service isc-dhcp-server restart
```

## Reference Links

- [HypriotOS](https://github.com/hypriot/image-builder-rpi/releases)
