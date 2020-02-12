---
layout: post
title:  "FAQ"
menuTitle: "FAQ"
weight: 50
date:   2019-10-25
categories: [wiki]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [turing_pi, faq]
published: true
---

### 1. Which Raspberry Pi models are compatible?

Turing Pi supports the following models with and without eMMC

- [Raspberry Pi Compute Module 1](https://www.raspberrypi.org/products/compute-module-1/)
- [Raspberry Pi Compute Module 3](https://www.raspberrypi.org/products/compute-module-3/)
- [Raspberry Pi Compute Module 3+](https://www.raspberrypi.org/products/compute-module-3-plus/)

### 2. Does the board support the new Rasberry pi 4?

There is no Compute Model for the Raspberry pi 4th generation yet

### 3. How to the compute modules communicate with each other?

The nodes interconnected with the onboard 1 Gbps switch. However, each node is limited with 100 Mbps USB speed. Also, there is an I2C bus to exchange some technical information between nodes, including Real-Time Clock (RTC).

### 4. From where the cluster board boots OS?

You can boot the OS either from eMMC or SD card. 

### 5. Does each node get its own IP address?

Yes

### 6. Can I flash compute modules through the board?

Yes, you can flash a compute module using a top/master node.

### 7. How do the Ethernet, USB, HDMI, and audio ports work? Is there a way to switch them between nodes?
Each pair of USB connected to a particular node. HDMI and audio connected with a top/master node. Ethernet connected with a second node. 

### 8. There are ATX and DC 12V power ports on the cluster board. Does this mean it can function from either an ATX power supply or 12V?
Yes

### 7. What ca I do with the board?

- Edge gateway and application hosting
- Homelab
- Develop and learn cloud-native technologies (Kubernetes, Docker, Serverless, Microservices) on bare metal
- Cloud-native apps testing environment
- Learn concepts of distributed Machine Learning apps
- Hosting and managing IoT apps
- Prototype and learn cluster applications, parallel computing, and distributed computing concepts on bare metal
- Host Minecraft 

