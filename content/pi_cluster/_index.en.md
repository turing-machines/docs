+++
title = "RPI Cluster"
description = "This is pi_cluster tutorial page"
weight = 10 
pre = "<b>2. </b>"
chapter = true
+++

# Rapsberry PI Cluster

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

<!--more-->

![](/images/kubernetes/cluster1_overview.png)

{{%children style="h3" description="false" depth="1" sort="weight" %}}

![](/images/kubernetes/cluster1_nodes.png)
![](/images/kubernetes/cluster2_nodes.png)

