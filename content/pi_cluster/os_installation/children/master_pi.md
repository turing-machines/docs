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

- Download the operating system from [HypriotOS](https://github.com/hypriot/image-builder-rpi/releases).
- Flash all 3 or 5 SD cards using **Win32DiskImager** or similar.

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

~~~
sudo apt-get remove --purge cloud-init
sudo apt-get autoremove
~~~

### Update master PI name 

As root, replace **black-pearl** by **kubemaster-pi**, in the two following files:

```bash
sudo -i

vi /etc/hosts
vi /etc/hostname
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

