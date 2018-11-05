---
layout: post
title:  "Kubedge eLTE Simulation"
menuTitle:  "eLTE"
weight: 15
date:   2018-09-01
categories: [wiki, wip]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [kubernetes, kubedge, elte, rpi]
published: true
---

Install Kubedge eLTE Application on the PI Cluster

<!--more-->

## Key Aspects

- Install eLTE
- Test access to eLTE

## Deploy Using helm

```bash
helm repo add hack4easy "https://raw.githubusercontent.com/kubedge/helmrepos/arm32v7/hack4easy"
helm repo update
```

## Apply the labels to the nodes

Ensure the right labels have been applied to the nodes where eLTE is installed

For instance:

```bash
kubectl label nodes kubemaster-pi kubedgeNodeType=lte-ran 
```

### Direct installation from the repo

If you feel lucky:

```bash
helm install hack4easy/kubesim-elte-arm32v7 --name sim-elte 
```

### Two steps installation from local

If you want to better understand the setup:

```bash
cd $MY_LOCAL_HELM_CHARTS
helm fetch hack4easy/kubesim-elte-arm32v7
tar xvf kubesim-elte-arm32v7-0.1.0.tgz
cd kubesim-elte-arm32v7/
helm install . --name sim-elte 
```
## Source Code

The images creation scripts are availble under:

- [Repo](https://github.com/kubedge/kubesim_elte)
- [ApplicationCode](https://github.com/kubedge/kubesim_elte/tree/arm32v7/kubesim_elte)
- [Dockerfile](https://github.com/kubedge/kubesim_elte/tree/arm32v7/images/kubesim_elte)
- [Chart](https://github.com/kubedge/kubesim_elte/tree/arm32v7/charts/kubesim-elte-arm32v7)

## Cleanup

```bash
$ helm delete --purge sim-elte

release "elte" deleted
```

## Conclusion

{{% notice note %}}
WIP
{{% /notice %}}

## Reference Links

- [Video1](https://youtu.be/ZyTLMnzehyU?t=1798)
- [Video2](https://www.youtube.com/watch?v=a7MX6ED2zVM)
