+++
title = "DevOps"
description = "This is devops tutorial page"
weight = 5 
pre = "<b>1. </b>"
chapter = true
+++

# DevOps

Since each PI acts a cloud node, you need to be able
to install, manage, test and share the software.
Kubedge leverages GitHub and GerritHub to share and review code,
Travis-CI for continuous integration. One key aspect is to be able
to build executables and docker image that can run on the broadcom processor
of the PI. The docker images are available to download on dockerhub.

In order to build the present website, we had to understand how to use
github pages and well as for instance the Hugo framework to convert the
markdown documents into HTML.

Finally some of the operations are easier to run on your laptop, for
instance the development of the software. Kubedge team did create an Ubuntu base
virtual machine using an SDK. 

<!--more-->

{{%children style="h3" description="false" depth="1" sort="weight" %}}
