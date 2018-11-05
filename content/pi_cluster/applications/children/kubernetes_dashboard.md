---
layout: post
title:  "Installing Kubernetes Dashboard"
menuTitle:  "Dashboard"
weight: 10
date:   2018-09-01
categories: [wiki, wip]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [kubernetes, dashboard, rpi]
published: true
---

Install Kubernetes Dashboard on the PI Cluster

<!--more-->

![](/images/kubernetes/cluster2_overview.png)

## Key Aspects

- Install Dashboard
- Access the dashboard for a web browser

## Deploy Using kubectl

```bash
cd $KUBE_RPI_GITREPO_LOCATION/kube-deployment/dashboard
kubectl apply -f kubernetes-dashboard-arm.yaml
```
## Deploy Using helm

{{% notice note %}}
Helm Chart is still work in progress
{{% /notice %}}

```bash
helm repo add kubedge2 "https://raw.githubusercontent.com/kubedge/helmrepos/arm32v7/kubedge2"
helm repo update
```

### Direct installation from the repo

If you fill lucky:

```bash
helm install kubedge2/kubernetes-dashboard-arm32v7 --name kubernetes-dashboard 
```

### Two steps installation from local

If you want to better understand the setup:

```bash
cd $MY_LOCAL_HELM_CHARTS
helm fetch kubedge2/kubernetes-dashboard-arm32v7
tar xvf kubernetes-dashboard-arm32v7-0.7.5.tgz
cd kubernetes-dashboard-arm32v7/
helm install . --name kubernetes-dashboard 
```

## Source Code

The chart is available under:

- [kubernetes-dashboard](https://github.com/kubedge/kube-rpi/tree/master/charts/kubernetes-dashboard-arm32v7)

## Cleanup

```bash
kubectl delete -f kubernetes-dashboard-arm.yaml

secret "kubernetes-dashboard-certs" deleted
serviceaccount "kubernetes-dashboard" deleted
role.rbac.authorization.k8s.io "kubernetes-dashboard-minimal" deleted
rolebinding.rbac.authorization.k8s.io "kubernetes-dashboard-minimal" deleted
deployment.apps "kubernetes-dashboard" deleted
service "kubernetes-dashboard" deleted
```

## Conclusion

{{% notice note %}}
Still need to debug the Kubernetes Helm Chart.
{{% /notice %}}

## Reference Links

{{% notice note %}}
WIP
{{% /notice %}}
