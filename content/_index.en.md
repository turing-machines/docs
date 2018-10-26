---
title: "Kubedge"
---

# Kubedge

Note: This page and web site is still work in progress.

## Personal, Portable Edge Network and Lab. 

![](/images/raspberrypi/IMG_0339.JPG)
![](/images/raspberrypi/DSC08310.JPG)


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

### DevOps Training

Since each PI acts a cloud node, you need to be able
to install, manage, test and share the software.
Kubedge leverages GitHub and GerritHub to share and review code,
Travis-CI for continuous integration. One key aspect is to be able
to build executables and docker image that can run on the broadcom processor
of the PI. The docker images are available to download on dockerhub.

In order to build the present website, we had to understand how to use
github pages and well as for instance the Hugo framework to convert the
markdown documents into HTML.

Finally some of the operations are easier to run on your laptop, for
instance the development of the software. Kubedge team did create an Ubuntu base
virtual machine using an SDK. 

### Kubernetes Training Lab

The assembly of the cluster itself brings its set of lessons. What to
be carreful of when you purchase your power supply, the length of your
ethernet cables or power supply cables. 
Differences between the PI 3B+ vs PI 3B (*1Gb* ethernet instead of 100Mb) have
to be accounted when you pick up your switch. Account for having 1 additonal port available
on your switch to be able to plug your PC to cluster using Ethernet.

Next step is to install the OS. Immediatly you will realize that it is unpracticle
to plug each node one after the other to an HDMI screen, USB mouse and keyboard in
order to perform the first initalization. Some of the OS such HyperiotOS have the 
great idea to preconfigure the node with SSH enabled, docker. This makes every plug
and play: Flush your SD card, connect the PI to your home router and voila you just
have to SSH.

Then you will have to learn how to create a NAT and DHCP server on your master node.

The bigger your cluster the quicker you will realize that some of the operations
are repetitiv, hence the need for automation. The easiet one to learn is ansible. 
Put if you install everything on the OS directly, then start the issue of maintaining the OS.
Because HyperiotOS comes by default with docker, which brings us back to lesson 1: Have everything
has a container.

The defacto tools to manage a multi node docker cluster is currently kubernetes. By using
kubeadm the installation is quite simple as long as you pay attention that the images pulled
by kubernetes are actually the one for PI and not the one for your usual cloud.

For people with Kubernetes experience (for instance on GCP), this is where the real lessons start:
- A lot of the software is not available by default on PI. How do you recompile calico, tiller...for the PI.
- It is much easier to install components using the Kubernetes HELM but a lot of the helm charts are pulling the AMD64 version of the ARM image.
- Finally, how do you create your own helm chart repository using github so that you can run a clean helm add repo and helm install commands.

And mainly, you will started to appreciate go and the new Java 9 modules to actually create true microservices
Because both langugage have the ability to create standalone executables, which in turn allow to create containers starting from "scratch".
Compare it with a python container and you will understand very quickly why it is beneficial. The PI only has 1G of RAM...which helps to understand
the interest of having slim true microservices.


### LTE and 5G Simulator

- The upstream wifi network from the master PI acts as the core network. You connect to the internet.
- The master PI is running the LTE EPC and the 5G CORE components. Some of those of components such
as SGW Gateway are running on the Master PI.
- Some secondary PIs are used to simulate the LTE eNODEb and 5G NR nodes. 
5G NR nodes (leveraging the Wifi spectrum).
- The Ethernet cables act as the backhaul network between the EPC and eNodeB/5G NR.
- a PI enabling its WIFI access point acts 5G NR nodes and spectrum.
- a PI enabling its Bluetooth as an Personal Area Network acts an LTE or eLTE eNodeB (and spectrum)

### NFV/SDN Network Slicing Simulator

Finally currently when the traffic is following through WIFI to ETH0 on the 5G NR node and from ETH0 to WIFI on the EPC node, the routing of the 
traffic is done using Linux Kernel mainly.
The goal here is to build an NFV able to throttle for instance the traffic wifi network (simulating 5G) in order to create a simulation of 
network slicing. At that point the traffic on the 5G NR node will not go through the kernel but will go from WIFI through the NFV back to ETH0. 


WIP.

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

