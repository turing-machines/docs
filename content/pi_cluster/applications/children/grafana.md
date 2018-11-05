---
layout: post
title:  "Installing Grafana"
menuTitle:  "Grafana"
weight: 25 
date:   2018-09-01
categories: [wiki, wip]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [kubernetes, grafana, rpi]
published: true
---

**Install Grafana on the PI Cluster**. Grafana helps to plot the data in the system. It is an OSS like tools which helps to manage the kubedge cluster.

<!--more-->

## Key Aspects

- Install Dashboard
- Access the dashboard for a web browser

## Deploy Using helm

{{% notice note %}}
Helm Chart is still work in progress
{{% /notice %}}

```bash
helm repo add kubedge2 "https://raw.githubusercontent.com/kubedge/helmrepos/arm32v7/kubedge2"
helm repo update
```

### Direct installation from the repo

If you feel lucky:

```bash
helm install kubedge2/grafana-arm32v7 --name grafana 
```

### Two steps installation from local

If you want to better understand the setup:

```bash
cd $MY_LOCAL_HELM_CHARTS
helm fetch kubedge2/grafana-arm32v7
tar xvf grafana-arm32v7-1.17.4.tgz
cd grafana-arm32v7/
helm install . --name grafana 
```

## Source Code

The chart is available under:

- [grafana](https://github.com/kubedge/kube-rpi/tree/master/charts/grafana-arm32v7)

## Cleanup

Run the delete command

```bash
helm delete --purge grafana

release "grafana" deleted
```

## Reference Links

{{% notice note %}}
WIP
{{% /notice %}}
