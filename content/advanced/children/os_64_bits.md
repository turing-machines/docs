---
layout: post
title:  "Installing Hypriot OS"
menuTitle:  "Hypriot OS 64"
weight: 10
date:   2018-15-01
categories: [wiki, wip]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [kubernetes, security, 64, rpi]
published: true
---

Also ARM processor on the Raspberry PI 3B+ is a 64 bit processor,
because the board is only equipped with 1G of RAM, a 64 bit operating system
is not really needed except when....

<!--more-->

## Key Aspects

- The goal is to deploy HypriotOS 64
- The key target applications are:
  + DPDK
  + CEPH
  + BlockChain

## The OS

One version of HypriotOS seems to be available here.

- [64BitImage](https://github.com/DieterReuter/image-builder-rpi64/releases)

## Everything Else

- Upgrade all the Travis-CI and branches to support arm64v8
- Rebuild all the docker images for the new architecture.

## The real hard stuff

- Get DPDK to work on ARM64.
- Get CEPH to work on ARM64.

## Reference Links

- [GitHub](https://github.com/dieterreuter/workshop-raspberrypi-64bit-os)


