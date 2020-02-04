---
layout: post
title:  "Deploy Helm and Tiller on Turing PI cluster"
menuTitle:  "Helm and Tiller"
weight: 10
date:   2020-02-04
categories: [wiki]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [kubernetes, helm]
published: true
---

Use Helm & Tiller on the Turing PI Cluster.

<!--more-->

### Install Helm

~~~
wget https://get.helm.sh/helm-v2.14.3-linux-arm.tar.gz
tar xvzf helm-v2.14.3-linux-arm.tar.gz
sudo mv linux-arm/helm /usr/local/bin/helm
rm -rf linux-arm
~~~

Create rbac-config.yaml
~~~
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tiller
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: tiller
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
  - kind: ServiceAccount
    name: tiller
    namespace: kube-system
~~~

~~~
kubectl apply -f rbac-config.yaml
~~~

Init Helm
~~~
helm init --tiller-image=jessestuart/tiller --service-account tiller --override spec.selector.matchLabels.'name'='tiller',spec.selector.matchLabels.'app'='helm' --output yaml | sed 's@apiVersion: extensions/v1beta1@apiVersion: apps/v1@' | kubectl apply -f -
~~~

### Reference Links

- [Usage of remote API](https://github.com/jonaseck2/rpi-helm)
