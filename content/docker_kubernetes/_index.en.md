+++
title = "Kubernetes"
description = "This is Kubernetes tutorial page"
weight = 10
chapter = true
+++

# Kubernetes

~~~
$ kubectl get pods --all-namespaces
NAMESPACE     NAME                             READY   STATUS    RESTARTS   AGE
kube-system   coredns-6955765f44-slbhm         1/1     Running   19         8h
kube-system   coredns-6955765f44-zv8f8         1/1     Running   19         8h
kube-system   etcd-master                      1/1     Running   38         8h
kube-system   kube-apiserver-master            1/1     Running   28         8h
kube-system   kube-controller-manager-master   1/1     Running   29         8h
kube-system   kube-flannel-ds-arm-68ts8        1/1     Running   7          7h27m
kube-system   kube-flannel-ds-arm-dflh6        1/1     Running   14         7h48m
kube-system   kube-flannel-ds-arm-hjh67        1/1     Running   25         7h59m
kube-system   kube-flannel-ds-arm-q6d7q        1/1     Running   16         7h32m
kube-system   kube-flannel-ds-arm-qp4fq        1/1     Running   0          7h40m
kube-system   kube-proxy-62lm8                 1/1     Running   12         7h32m
kube-system   kube-proxy-9fdnh                 1/1     Running   0          7h40m
kube-system   kube-proxy-hxm2m                 1/1     Running   6          7h27m
kube-system   kube-proxy-vb49r                 1/1     Running   20         8h
kube-system   kube-proxy-zpbmc                 1/1     Running   12         7h48m
kube-system   kube-scheduler-master            1/1     Running   30         8h
~~~

{{%children style="h3" description="false" depth="1" sort="weight" %}}
