---
layout: post
title:  "Kubedge 5G NR Simulation"
menuTitle:  "5G NR"
weight: 20
date:   2018-09-01
categories: [wiki, wip]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [kubernetes, kubedge, nr, rpi]
published: true
---

Install Kubedge LTE Application on the PI Cluster

<!--more-->

## Key Aspects

- Install LTE
- Test access to LTE

## Deploy Using helm

```bash
helm repo add hack4easy "https://raw.githubusercontent.com/kubedge/helmrepos/arm32v7/hack4easy"
helm repo update
```

## Apply the labels to the nodes

Ensure the right labels have been applied to the nodes where LTE is installed

For instance:

```bash
kubectl label nodes kubemaster-pi kubedgeNodeType=5g-ran
```

### Direct installation from the repo

If you feel lucky:

```bash
helm install hack4easy/kubesim-nr-arm32v7 --name sim-nr 
```

### Two steps installation from local

If you want to better understand the setup:

```bash
cd $MY_LOCAL_HELM_CHARTS
helm fetch hack4easy/kubesim-nr-arm32v7
tar xvf kubesim-nr-arm32v7-0.1.0.tgz
cd kubesim-nr-arm32v7/
helm install . --name sim-nr 
```
## Source Code

The images creation scripts are availble under:

- [Repo](https://github.com/kubedge/kubesim_nr)
- [ApplicationCode](https://github.com/kubedge/kubesim_nr/tree/arm32v7/kubesim_nr)
- [Dockerfile](https://github.com/kubedge/kubesim_nr/tree/arm32v7/images/kubesim_nr)
- [Chart](https://github.com/kubedge/kubesim_nr/tree/arm32v7/charts/kubesim-nr-arm32v7)

## Cleanup

```bash
$ helm delete --purge sim-nr

release "nr" deleted
```

## Conclusion

{{% notice note %}}
WIP
{{% /notice %}}

## Reference Links

- [Video1](https://youtu.be/ZyTLMnzehyU?t=1798)
- [Video2](https://www.youtube.com/watch?v=a7MX6ED2zVM)
