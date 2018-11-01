---
layout: post
title:  "Rebuild Calico for ARM32V7"
menuTitle:  "Calico"
date:   2018-07-17
categories: [wiki, wip]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [kubernetes, calico, cni]
weight: 15 
published: true
---

Neither calico nor canal seems to be available for usage yet on ARM32V7 for PI.
The attempt here is to cross-compile the calico containers and use them on the PI cluster.
Since calico's role is mainly to setup ip table to get Kubernetes POD-POD communication established,
the likelyhood of being able to reuse some of calico go for a VNF are really slim.

<!--more-->

## Key Aspects

- Rebuild the Calico 

## Build Kubernetes executables for ARM32V7

{{% notice note %}}
WIP
{{% /notice %}}

## Conclusion

{{% notice note %}}
WIP
{{% /notice %}}

## Reference Links

- [Kubernetes cross build]()

