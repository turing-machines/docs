---
layout: post
title:  "Installing NATS"
menuTitle:  "NATS"
weight: 21 
date:   2018-11-11
categories: [wiki, wip]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [kubernetes, nats, rpi]
published: true
---

Install NATS on the PI Cluster

<!--more-->

## Key Aspects

- Install NATS as a CRD in Kubedge using Helm
- Verify using simple pub/sub that the system is working

```bash
$ kubectl get crd
NAME                       CREATED AT
natsclusters.nats.io       2018-11-11T23:26:59Z
natsserviceroles.nats.io   2018-11-11T23:26:59Z

$ kubectl get all -n nats-io
NAME                                             READY   STATUS    RESTARTS   AGE
pod/nats-cluster-1                               1/1     Running   0          89m
pod/nats-cluster-2                               1/1     Running   0          89m
pod/nats-cluster-3                               1/1     Running   0          89m
pod/nats-nats-operator-arm32v7-9f66d65d6-dnp9p   1/1     Running   1          90m

NAME                        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)             AGE
service/nats-cluster        ClusterIP   10.107.86.149   <none>        4222/TCP            89m
service/nats-cluster-mgmt   ClusterIP   None            <none>        6222/TCP,8222/TCP   89m

NAME                                         DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nats-nats-operator-arm32v7   1         1         1            1           90m

NAME                                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/nats-nats-operator-arm32v7-9f66d65d6   1         1         1       90m
```

## Deploy Using helm

```bash
helm repo add kubedge2 "https://raw.githubusercontent.com/kubedge/helmrepos/arm32v7/kubedge2"
helm repo update
```

### Direct installation from the repo

If you feel lucky:

```bash
helm install --namespace nats-io --name nats kubedge2/nats-operator-arm32v7
```

### Two steps installation from local

If you want to better understand the setup:

```bash
cd $MY_LOCAL_HELM_CHARTS
helm fetch kubedge2/nats-operator-arm32v7
tar xvf nats-operator-arm32v7-7.3.4.tgz
cd nats-operator-arm32v7/
kubectl create -f templates/customresourcedefinition.yaml
helm install --namespace nats-io --name nats .
```
### Install a Subscriber

Use the subscriber help chart

```bash
helm install --name nats-sub kubedge1/nats-sub-arm32v7
```

### Install a Publisher

Use the publisher helm chart

```bash
helm install --name nats-pub kubedge1/nats-pub-arm32v7
```

### Check the messages flow

The messages published by the publisher are received in the subscriber

```bash
kubectl logs pod/nats-sub-kubesim-nats-sub-55d8d899b5-sfvlc kubesim-nats-sub-arm32v7

Listening on [dockerfile-hardcoded-subject]
[#1] Received on [dockerfile-hardcoded-subject]: 'dockerfile-hardcoded-message'
[#2] Received on [dockerfile-hardcoded-subject]: 'dockerfile-hardcoded-message'
[#3] Received on [dockerfile-hardcoded-subject]: 'dockerfile-hardcoded-message'
[#4] Received on [dockerfile-hardcoded-subject]: 'dockerfile-hardcoded-message'
[#5] Received on [dockerfile-hardcoded-subject]: 'dockerfile-hardcoded-message'
[#6] Received on [dockerfile-hardcoded-subject]: 'dockerfile-hardcoded-message'
[#7] Received on [dockerfile-hardcoded-subject]: 'dockerfile-hardcoded-message'
[#8] Received on [dockerfile-hardcoded-subject]: 'dockerfile-hardcoded-message'
[#9] Received on [dockerfile-hardcoded-subject]: 'dockerfile-hardcoded-message'
[#10] Received on [dockerfile-hardcoded-subject]: 'dockerfile-hardcoded-message'
[#11] Received on [dockerfile-hardcoded-subject]: 'dockerfile-hardcoded-message'
```

## Source Code

The images creation scripts are availble under:

- [nats-operator](https://github.com/kubedge/kube-rpi/tree/master/images/nats-operator)

The chart is available under:

- [nats-operator](https://github.com/kubedge/kube-rpi/tree/master/charts/nats-operator-arm32v7)

## Cleanup

Run the delete command

```bash
helm delete --purge nats

release "nats" deleted
```

## Conclusion

{{% notice note %}}
We still have to be able to create the images automatically using .travis.yml
{{% /notice %}}

## Reference Links

{{% notice note %}}
WIP
{{% /notice %}}
