---
layout: post
title:  "Raspberry PI cluster Assembly"
menuTitle: "HW Assembly"
weight: 5
date:   2018-07-07
categories: [wiki]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [ansible, rpi]
published: true
---

This page contains examples of harware to use in order to build a cluster

<!--more-->

## Assembled 3 nodes cluster

![](/images/raspberrypi/DSC08310.JPG)

## 3 Nodes Cluster Hardware Assembly

| Component               | URL Example                                                            | Quantity | Cost Estimate |
|-------------------------|------------------------------------------------------------------------|----------|---------------|
| Rack                    | [PI Rack](https://www.amazon.com/gp/product/B077D4J3M5)                |     1    |           $30 |
| PI                      | [PI](https://www.amazon.com/gp/product/B07BDR5PDW)                     |     3    |          $105 |
| SD Card                 | [SD Cards](https://www.amazon.com/gp/product/B06XWN9Q99)               |     3    |           $30 |
| Heat Sink               | [Heat Sink](https://www.amazon.com/gp/product/B01G9NA2I6)              |     6    |           $10 |
| 5-Port Power Supply     | [Power Supply](https://www.amazon.com/gp/product/B00VH8ZW02)           |     3    |           $20 |
| Power Cable for PI      | [Power Cable for PI](https://www.amazon.com/gp/product/B015XR60MQ)     |     3    |           $10 |
| Power Cable for Switch  | [Power Cable for Switch](https://www.amazon.com/gp/product/B003MQO96U) |     1    |            $5 |
| 5-Port Switch           | [Switch](https://www.amazon.com/gp/product/B001QUA6R0)                 |     1    |           $15 |
| 1ft CAT6 Cables         | [Cat 6 Cables](https://www.amazon.com/gp/product/B00E5I7T9I)           |     3    |           $10 |
| **Total**               |                                                                        |          |      **$235** |
| Blinkt                  | [Blinkt](https://www.adafruit.com/product/3195)                        |     3    |           $15 |
| Transport Case          | [Case](https://www.google.com/shopping/product/192066162776567162)     |     1    |           $25 |
| **Total with addons**   |                                                                        |          |      **$275** |

{{% notice note %}}
Pay attention to the PI ethernet speed when picking the switch. PI3B are only 100Mbps where PI3B+ are 1Gpbs
{{% /notice %}}

## 5 Nodes Cluster Hardware Assembly

| Component               | URL Example                                                            | Quantity | Cost Estimate |
|-------------------------|------------------------------------------------------------------------|----------|---------------|
| Rack                    | [PI Rack](https://www.amazon.com/gp/product/B077D4J3M5)                |     1    |           $30 |
| PI                      | [PI](https://www.amazon.com/gp/product/B07BDR5PDW)                     |     5    |          $175 |
| SD Card                 | [SD Cards](https://www.amazon.com/gp/product/B06XWN9Q99)               |     5    |           $50 |
| Heat Sink               | [Heat Sink](https://www.amazon.com/gp/product/B01G9NA2I6)              |    10    |           $10 |
| 10-Port Power Supply    | [Power Supply](https://www.amazon.com/gp/product/B00YRYS4T4)           |     1    |           $40 |
| Power Cable for PI      | [Power Cable for PI](https://www.amazon.com/gp/product/B015XR60MQ)     |     5    |           $10 |
| Power Cable for Switch  | [Power Cable for Switch](https://www.amazon.com/gp/product/B003MQO96U) |     1    |            $5 |
| 8-Port Switch           | [Switch](https://www.amazon.com/gp/product/B001QUA6RA)                 |     1    |           $25 |
| 1.5f CAT6 Cables        | [Cat 6 Cables](https://www.amazon.com/gp/product/B0721RFHT8)           |     5    |           $10 |
| **Total**               |                                                                        |          |      **$355** |
| Blinkt                  | [Blinkt](https://www.adafruit.com/product/3195)                        |     3    |           $15 |
| Transport Case          | [Case](https://www.google.com/shopping/product/192066162776567162)     |     1    |           $25 |
| **Total with addons**   |                                                                        |          |      **$395** |

{{% notice note %}}
Having available ports on the switch is very helpfull to connect to the cluster when the WIFI access is not working properly.
{{% /notice %}}

{{% notice note %}}
1ft long cables for the top PI are kind of too short. 3ft long cables are kind of too long.
{{% /notice %}}

## Reference Links

- [Video1](https://www.youtube.com/watch?v=KJKhRLKXr-Q)
