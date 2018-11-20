---
layout: post
title:  "OS Installation on Master PI"
menuTitle: "OS on Master PI"
weight: 10
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

{{% notice note %}}
Even if processor is 64bits, OS is still 32bits. (Memory is small anyway).
Removed cloud-init once the site was up.
{{% /notice %}}

- For simple arm32v7 OS, download the operating system from [HypriotOS ARM32V7](https://github.com/hypriot/image-builder-rpi/releases/download/v1.9.0/hypriotos-rpi-v1.9.0.img.zip)
- For more complex arm64 OS, download the operating system from [HypriotOS ARM64V8](https://github.com/DieterReuter/image-builder-rpi64/releases/download/v20180429-184538/hypriotos-rpi64-v20180429-184538.img.zip)
- Flash all 3 or 5 SD cards using **Win32DiskImager** or similar. It takes around 30 seconds per card.

## OS on master on master PI

{{% notice warning %}}
Do not power up the slaves nodes for right now. Either plug your home router directly to the master PI, or to the switch.
The goal here is to get an IP address allocated by your home router to the master PI.
{{% /notice %}}

### Access the node

- Insert the SD card in the master PI.
- Access your home router and look for "black-pearl" IP address.
- SSH to the node using **cygwin**, **putty** or **moba-xterm** for instance. The credentials are pirate/hypriot.

### Freeze your configuration

Cloud init is perfect for the first boot. Once the node
is up, it can be challenging not to preserve the fine tuning done
to the OS.

```bash
sudo apt-get remove --purge cloud-init
sudo apt-get autoremove
```

Let's update to the latest version

```bash
sudo apt-get update
sudo apt-get upgrade
```

### Update master PI name

As root, replace **black-pearl** by **kubemaster-pi**, in the two following files:

```bash
sudo -i

vi /etc/hosts
```

It seems on HypriotOS 64, you need to do

```bash
vi /etc/hostname
sudo service hostname restart
```

It seems on HypriotOS 32, you need to do

```bash
sudo hostnamectl set-hostname kubemaster-pi
```


### Configure the pirate account

If you prefer to edit using vi instead of nano

```bash
vi /etc/environment

EDITOR=vi
```
Then you need to set up the ssh keys
Either create a new ssh key (id_rsa, id_rsa.pub) and copy in id_rsa.pub into [GitHub](https://github.com/settings/keys)

```bash
ssh-keygen
```
or install your private and public key into the **/home/pirate/.ssh** directory (The same key you registered in GitHub)

```bash
scp id_rsa pirate@<PI>:/home/pirate/.ssh/id_rsa
scp id_rsa.pub pirate@<PI>:/home/pirate/.ssh/id_rsa.pub
```

### Install GIT

Since you have ethernet access, it is a good time to install GIT in order to download usefull scripts from github.com

```bash
sudo apt-get update
sudo apt-get install git
sudo apt-get install git-review
```


```bash
$ mkdir -p $HOME/proj/kubedge
$ cd $HOME/proj/kubedge
```


create a cloneit1.sh file and run it

```bash
#!/bin/bash
GOODPATH=`pwd`
USERID=yourgithubaccount
for i in helmrepos kubeplay kubesim_5gc kubesim_base kubesim_elte kubesim_epc kubesim_lte kubesim_nr kubesim_blinkt
do
echo "======================================================"
echo $i
echo "======================================================"
# If you want to contribute
# git clone -b arm32v7 ssh://$USERID@review.gerrithub.io:29418/kubedge/$i && scp -p -P 29418 $USERID@review.gerrithub.io:hooks/commit-msg $i/.git/hooks/
git clone -b arm32v7 git@github.com:kubedge/$i.git
cd $GOODPATH
done
```

create a cloneit2.sh file and run it

``` bash
#!/bin/bash
GOODPATH=`pwd`
USERID=yourgithubaccount
for i in kube-rpi ansible-kube-rpi kubedge
do
echo "======================================================"
echo $i
echo "======================================================"
# If you want to contribute
# git clone ssh://$USERID@review.gerrithub.io:29418/kubedge/$i && scp -p -P 29418 $USERID@review.gerrithub.io:hooks/commit-msg $i/.git/hooks/
git clone git@github.com:kubedge/$i.git
cd $GOODPATH
done
```

{{% notice info %}}
You know have access especially through **kube-rpi** and **ansible-kube-rpi** to example files and ansible playbook usefull to install your first node:
**cd $HOME/proj/kubedge/kube-rpi/config/cluster1/hypriotos/kubemaster-pi**
{{% /notice %}}


## Reference Links

- [HypriotOS](https://github.com/hypriot/image-builder-rpi/releases)
- [Video2](https://www.youtube.com/watch?v=eZ5uX-JJbyY)

