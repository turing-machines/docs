+++
title = "Kubedge"
description = "Main page"
weight = 1 
chapter = true
+++

# Kubedge

![](/images/raspberrypi/IMG_0339.JPG)

## Personal, Portable Edge Network and Lab. 

Kubedge is personal and portable edge cloud. The
key concept is to leverage the three
network interfaces available on each PI:

- 1 GB Ethernet
- Wifi
- Bluetooth.

The PI are interconnected together using the local
switch. The top/master PI is acting as a NAT/Router
for the rest of the PI. This main advantage that 
when you move your lab from home to work, all the IPs
of the cluster stay identical. 

{{% notice note %}}
This page and web site is still work in progress.
{{% /notice %}}

## Trainings & Tutorials


## Associated GIT Repos

master branch is mainly used for dev.
arm32v7 branch contains stable code for Rasberry PI.
amd64 branch contains stable code for AMD64 cluster

SIMULATOR REPOS:

- [kubesim_base](https://github.com/kubedge/kubesim_base)
- [kubesim_5gc](https://github.com/kubedge/kubesim_5gc)
- [kubesim_elte](https://github.com/kubedge/kubesim_elte)
- [kubesim_epc](https://github.com/kubedge/kubesim_epc)
- [kubesim_lte](https://github.com/kubedge/kubesim_lte)
- [kubesim_nr](https://github.com/kubedge/kubesim_nr)

TUTORIAL REPOS:

- [kubedge](https://github.com/kubedge/kubedge)
- [kubeplay](https://github.com/kubedge/kubeplay)

## Infrastructure Repos

INFRASTRUCTURE REPOS:

- [kube-rpi](https://github.com/kubedge/kube-rpi)
- [ansible-kube-rpi](https://github.com/kubedge/ansible-kube-rpi)

## Docker imagesi for PI

SIMULATOR DOCKER IMAGES FOR PI:

- [kubesim_base](https://hub.docker.com/r/hack4easy/kubesim_base-arm32v7)
- [kubesim_5gc](https://hub.docker.com/r/hack4easy/kubesim_5gc-arm32v7)
- [kubesim_elte](https://hub.docker.com/r/hack4easy/kubesim_elte-arm32v7)
- [kubesim_epc](https://hub.docker.com/r/hack4easy/kubesim_epc-arm32v7)
- [kubesim_lte](https://hub.docker.com/r/hack4easy/kubesim_lte-arm32v7)
- [kubesim_nr](https://hub.docker.com/r/hack4easy/kubesim_nr-arm32v7)

TUTORIAL REPOS FOR PI:

- [kubedge](https://hub.docker.com/r/kubedge1/kubedge-arm32v7)
- [kubeplay](https://hub.docker.com/r/kubedge1/kubeplay-arm32v7)

## Docker images for AMD64

SIMULATOR DOCKER IMAGES FOR AMD64:

- [kubesim_base](https://hub.docker.com/r/hack4easy/kubesim_base-amd64)
- [kubesim_5gc](https://hub.docker.com/r/hack4easy/kubesim_5gc-amd64)
- [kubesim_elte](https://hub.docker.com/r/hack4easy/kubesim_elte-amd64)
- [kubesim_epc](https://hub.docker.com/r/hack4easy/kubesim_epc-amd64)
- [kubesim_lte](https://hub.docker.com/r/hack4easy/kubesim_lte-amd64)
- [kubesim_nr](https://hub.docker.com/r/hack4easy/kubesim_nr-amd64)

TUTORIAL REPOS FOR AMD64:

- [kubedge](https://hub.docker.com/r/kubedge1/kubedge-amd64)
- [kubeplay](https://hub.docker.com/r/kubedge1/kubeplay-amd64)


## HELM REPOS

- [helmrepos](https://github.com/kubedge/helmrepos)

## Gerrit Review

SIMULATOR REPOS:

- [kubesim_base](https://review.gerrithub.io/#/admin/projects/kubedge/kubesim_base)
- [kubesim_5gc](https://review.gerrithub.io/#/admin/projects/kubedge/kubesim_5gc)
- [kubesim_elte](https://review.gerrithub.io/#/admin/projects/kubedge/kubesim_elte)
- [kubesim_epc](https://review.gerrithub.io/#/admin/projects/kubedge/kubesim_epc)
- [kubesim_lte](https://review.gerrithub.io/#/admin/projects/kubedge/kubesim_lte)
- [kubesim_nr](https://review.gerrithub.io/#/admin/projects/kubedge/kubesim_nr)

TUTORIAL REPOS:

- [kubedge](https://review.gerrithub.io/#/admin/projects/kubedge/kubedge)
- [kubeplay](https://review.gerrithub.io/#/admin/projects/kubedge/kubeplay)

## Automatic Build Review

SIMULATOR REPOS:

- [kubesim_base](https://travis-ci.com/kubedge/kubesim_base)
- [kubesim_5gc](https://travis-ci.com/kubedge/kubesim_5gc)
- [kubesim_elte](https://travis-ci.com/kubedge/kubesim_elte)
- [kubesim_epc](https://travis-ci.com/kubedge/kubesim_epc)
- [kubesim_lte](https://travis-ci.com/kubedge/kubesim_lte)
- [kubesim_nr](https://travis-ci.com/kubedge/kubesim_nr)

TUTORIAL REPOS:

- [kubedge](https://travis-ci.com/kubedge/kubedge)
- [kubeplay](https://travis-ci.com/kubedge/kubeplay)

