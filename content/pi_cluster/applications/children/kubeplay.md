---
layout: post
title:  "Installing Kubedge Kubeplay"
menuTitle:  "Kubeplay"
weight: 5
date:   2018-09-01
categories: [wiki, wip]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [kubernetes, kubedge, rpi]
published: true
---

Install simplistic Kubeplay Application on the PI Cluster. It is a primitiv golang based server
which get the user to go through the entire DevOps process (to build the docker image) and
deploy it using Helm on Kubedge.

<!--more-->

![](/images/kubeplay/kubeplay.png)

## Key Aspects

- Install Kubeplay
- Understand Helm and values.yaml
- Test access to Kubeplay

## Deploy Using helm

```bash
helm repo add kubedge1 "https://raw.githubusercontent.com/kubedge/helmrepos/arm32v7/kubedge1"
helm repo update
```

## Apply the labels to the nodes

No special label needed for kubeplay

### Direct installation from the repo

If you fill lucky:

```bash
helm install kubedge1/kubeplay-arm32v7 --name kubeplay 
```

### Two steps installation from local

If you want to better understand the setup:

```bash
cd $MY_LOCAL_HELM_CHARTS
helm fetch kubedge1/kubeplay-arm32v7
tar xvf kubeplay-arm32v7-0.1.0.tgz
cd kubeplay-arm32v7/
helm install . --name kubeplay 
```

## Testing

```bash
$ kubectl get services | grep kubeplay

kubeplay-kubeplay-arm32v7   NodePort    10.105.196.0     <none>        8005:32520/TCP    4m58s
```

Open a web browser and point at the master IP: [example](http://192.168.1.95:32520/testing_kubeplay)

## Source Code

The images creation scripts are availble under:

- [Repo](https://github.com/kubedge/kubeplay)
- [ApplicationCode](https://github.com/kubedge/kubeplay/tree/arm32v7/kubeplay)
- [Dockerfile](https://github.com/kubedge/kubeplay/tree/arm32v7/images/kubeplay)
- [Chart](https://github.com/kubedge/kubeplay/tree/arm32v7/charts/kubesim-kubeplay-arm32v7)

## Cleanup

```bash
$ helm delete --purge kubeplay

release "kubeplay" deleted
```

## Deploy

{{% notice note %}}
WIP
{{% /notice %}}

## Conclusion

{{% notice note %}}
WIP
{{% /notice %}}

## Reference Links

{{% notice note %}}
WIP
{{% /notice %}}
