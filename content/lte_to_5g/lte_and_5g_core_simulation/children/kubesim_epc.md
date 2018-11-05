---
layout: post
title:  "Kubedge EPC Simulation"
menuTitle:  "EPC"
weight: 10
date:   2018-09-01
categories: [wiki, wip]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [kubernetes, kubedge, epc, rpi]
published: true
---

Install Kubedge EPC Application on the PI Cluster

<!--more-->

## Key Aspects

- Install EPC
- Test access to EPC

## Deploy Using helm

```bash
helm repo add hack4easy "https://raw.githubusercontent.com/kubedge/helmrepos/arm32v7/hack4easy"
helm repo update
```

## Apply the labels to the nodes

Ensure the right labels have been applied to the nodes where EPC is installed

For instance:

```bash
kubectl label nodes kubemaster-pi kubedgeNodeType=lte-core 
```

### Direct installation from the repo

If you feel lucky:

```bash
helm install hack4easy/kubesim-epc-arm32v7 --name sim-epc 
```

### Two steps installation from local

If you want to better understand the setup:

```bash
cd $MY_LOCAL_HELM_CHARTS
helm fetch hack4easy/kubesim-epc-arm32v7
tar xvf kubesim-epc-arm32v7-0.1.0.tgz
cd kubesim-epc-arm32v7/
helm install . --name sim-epc 
```
## Source Code

The images creation scripts are availble under:

- [Repo](https://github.com/kubedge/kubesim_epc)
- [ApplicationCode](https://github.com/kubedge/kubesim_epc/tree/arm32v7/kubesim_epc)
- [Dockerfile](https://github.com/kubedge/kubesim_epc/tree/arm32v7/images/kubesim_epc)
- [Chart](https://github.com/kubedge/kubesim_epc/tree/arm32v7/charts/kubesim-epc-arm32v7)

## Cleanup

```bash
$ helm delete --purge sim-epc

release "epc" deleted
```

## Conclusion

{{% notice note %}}
WIP
{{% /notice %}}

## Reference Links

- [Video1](https://youtu.be/ZyTLMnzehyU?t=1798)
- [Video2](https://www.youtube.com/watch?v=a7MX6ED2zVM)
