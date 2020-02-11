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

### 1. Which Raspberry Pi are supported?

Supported models with eMMC and without

- [Raspberry Pi Compute Module 1](https://www.raspberrypi.org/products/compute-module-1/)
- [Raspberry Pi Compute Module 3](https://www.raspberrypi.org/products/compute-module-3/)
- [Raspberry Pi Compute Module 3+](https://www.raspberrypi.org/products/compute-module-3-plus/)

### 2. Будет ли поддержка Raspberry Pi 4?

Как только поступят в продажу Raspberry Pi 4 Compute Modules в короткие сроки будет версия платы с их поддержкой

### 3. How to the compute modules communicate with each other?

We use onboard 1 Gbps Ethernet switch within the nodes. Also, each node can exchange some tech info thought the I2C bus with each other, including Real-Time Clock (RTC)

### 4. Поддерживается ли прошивка Compute Modules через кластер?

Yes. Only for the master node.

### 5. USB connections to individual boards or is there a 1 Gbps switch or?

По два вертикальных USB подсоединены каждый к своей ноде. Если смотреть со стороны портов: правый первый USB подсоединенем к мастер ноде, второй с ethernet ко второй ноде, третий к четвертой ноде и четвертый к шестой ноде

### 6. I see ATX DC 12V power ports. Does this mean it can function from either an ATX power supply or 12V?

Yes

### 7. Guys what is the purpose of these things?

Kind of

- To prototype and learn clustering applications and practices
- Host at the edge Kubernetes (k8s, k3s), Docker, TensorFlow, Caffe and other beauties of microservice architecture
- Home education lab
- Compute node for IoT purposes
- Home automation server
