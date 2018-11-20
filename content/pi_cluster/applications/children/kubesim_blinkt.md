---
layout: post
title:  "Installing Kubedge Blinkt"
menuTitle:  "Blinkt"
weight: 15
date:   2018-09-01
categories: [wiki, wip]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [kubernetes, kubedge, blinkt, rpi]
published: true
---

Install Kubedge Blinkt Application on the PI Cluster

<!--more-->

{{< youtube P83FCYi3kL4 >}}

## Key Aspects

- Install Blinkt
- Test access to Blinkt

## Deploy Using helm

```bash
helm repo add kubedge1 "https://raw.githubusercontent.com/kubedge/helmrepos/arm32v7/kubedge1"
helm repo update
```

## Apply the labels to the nodes

Ensure the right labels have been applied to the nodes where Blinkt is installed

For instance:

```bash
kubectl label nodes kubemaster-pi blinktInstalled=true
kubectl label nodes home-pi blinktInstalled=true
kubectl label nodes nas-pi blinktInstalled=true
```

### Direct installation from the repo

If you feel lucky:

```bash
helm install kubedge1/kubesim-blinkt-arm32v7 --name blinkt
```

### Two steps installation from local

If you want to better understand the setup:

```bash
cd $MY_LOCAL_HELM_CHARTS
helm fetch kubedge1/kubesim-blinkt-arm32v7
tar xvf kubesim-blinkt-arm32v7-0.1.0.tgz
cd kubesim-blinkt-arm32v7/
helm install . --name blinkt
```
## Replica Control

Ensure the right labels have been applied to the nodes where Blinkt is installed

```bash
helm upgrade blinkt kubedge1/kubesim-blinkt-arm32v7 --set image.pullPolicy=IfNotPresent --set blinkt.algorithm=blinkt5 --set replicaCount=2
helm upgrade blinkt kubedge1/kubesim-blinkt-arm32v7 --set image.pullPolicy=IfNotPresent --set blinkt.algorithm=blinkt5 --set replicaCount=3
helm upgrade blinkt kubedge1/kubesim-blinkt-arm32v7 --set image.pullPolicy=IfNotPresent --set blinkt.algorithm=blinkt5 --set replicaCount=0
```
## Rolling Upgrade

Use blinkt coloring to highlight rolling upgrade

```bash
helm upgrade blinkt kubedge1/kubesim-blinkt-arm32v7 --set image.pullPolicy=IfNotPresent --set replicaCount=3 --set blinkt.release=green
helm upgrade blinkt kubedge1/kubesim-blinkt-arm32v7 --set image.pullPolicy=IfNotPresent --set replicaCount=3 --set blinkt.release=blue
helm upgrade blinkt kubedge1/kubesim-blinkt-arm32v7 --set image.pullPolicy=IfNotPresent --set replicaCount=3 --set blinkt.release=red
```

## Rollback

```bash
$ helm history blinkt
REVISION        UPDATED                         STATUS          CHART                           DESCRIPTION
....
16              Fri Nov  2 21:33:30 2018        SUPERSEDED      kubesim-blinkt-arm32v7-0.1.0    Upgrade complete
17              Sat Nov  3 02:00:18 2018        SUPERSEDED      kubesim-blinkt-arm32v7-0.1.0    Upgrade complete
18              Sat Nov  3 02:22:11 2018        SUPERSEDED      kubesim-blinkt-arm32v7-0.1.0    Upgrade complete
19              Sat Nov  3 02:23:11 2018        SUPERSEDED      kubesim-blinkt-arm32v7-0.1.0    Upgrade complete
20              Sun Nov  4 15:16:33 2018        SUPERSEDED      kubesim-blinkt-arm32v7-0.1.0    Upgrade complete
21              Mon Nov  5 00:11:42 2018        SUPERSEDED      kubesim-blinkt-arm32v7-0.1.0    Upgrade complete
22              Mon Nov  5 00:11:56 2018        SUPERSEDED      kubesim-blinkt-arm32v7-0.1.0    Upgrade complete
23              Mon Nov  5 00:13:41 2018        DEPLOYED        kubesim-blinkt-arm32v7-0.1.0    Upgrade complete
```
```bash
$ helm rollback blinkt 18

Rollback was a success! Happy Helming!
```

## Source Code

The images creation scripts are availble under:

- [Repo](https://github.com/kubedge/kubesim_blinkt)
- [ApplicationCode](https://github.com/kubedge/kubesim_blinkt/tree/arm32v7/kubesim_blinkt)
- [Dockerfile](https://github.com/kubedge/kubesim_blinkt/tree/arm32v7/images/kubesim_blinkt)
- [Chart](https://github.com/kubedge/kubesim_blinkt/tree/arm32v7/charts/kubesim-blinkt-arm32v7)

## Cleanup

```bash
$ helm delete --purge blinkt

release "blinkt" deleted
```

## Conclusion

{{% notice note %}}
WIP
{{% /notice %}}

## Reference Links

- [Video1](https://youtu.be/ZyTLMnzehyU?t=1798)
- [Video2](https://www.youtube.com/watch?v=a7MX6ED2zVM)
