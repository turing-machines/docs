---
layout: post
title:  "Installing Prometheus"
menuTitle:  "Prometheus"
weight: 20
date:   2018-09-01
categories: [wiki, wip]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [kubernetes, prometheus, rpi]
published: true
---

Install Prometheus on the Turing Pi

<!--more-->

![](/images/prometheus/load-node-stack1.png)

## Key Aspects

- Install Prometheus
- Access the dashboard for a web browser

## Deploy Using helm

```bash
helm repo add kubedge2 "https://raw.githubusercontent.com/kubedge/helmrepos/arm32v7/kubedge2"
helm repo update
```

### Direct installation from the repo

If you feel lucky:

```bash
helm install kubedge2/prometheus-arm32v7 --name prometheus
```

### Two steps installation from local

If you want to better understand the setup:

```bash
cd $MY_LOCAL_HELM_CHARTS
helm fetch kubedge2/prometheus-arm32v7
tar xvf prometheus-arm32v7-7.3.4.tgz
cd prometheus-arm32v7/
helm install . --name prometheus
```

## Source Code

The images creation scripts are availble under:

- [prometheus](https://github.com/kubedge/kube-rpi/tree/master/images/prometheus)
- [alertmanager](https://github.com/kubedge/kube-rpi/tree/master/images/alertmanager)
- [node-exporter](https://github.com/kubedge/kube-rpi/tree/master/images/node-exporter)
- [pushgateway](https://github.com/kubedge/kube-rpi/tree/master/images/pushgateway)
- [config-reload](https://github.com/kubedge/kube-rpi/tree/master/images/config-reload)
- [kube-state-metrics](https://github.com/kubedge/kube-rpi/tree/master/images/kube-state-metrics)

The chart is available under:

- [prometheus](https://github.com/kubedge/kube-rpi/tree/master/charts/prometheus-arm32v7)

## Cleanup

Run the delete command

```bash
helm delete --purge prometheus

release "prometheus" deleted
```

## Conclusion

{{% notice note %}}
We still have to be able to create the images automatically using .travis.yml
{{% /notice %}}

## Reference Links

{{% notice note %}}
WIP
{{% /notice %}}
