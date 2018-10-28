+++
title = "LTE to 5G Simulations"
description = "This is lte_to_5g tutorial page"
weight = 15 
pre = "<b>3. </b>"
chapter = true
+++

# LTE to 5G Transition

PI is well adapted to simulate 5G and LTE networks:

- The upstream wifi network from the master PI acts as the core network. You connect to the internet.
- The master PI is running the LTE EPC and the 5G CORE components. Some of those of components such
as SGW Gateway are running on the Master PI.
- Some secondary PIs are used to simulate the LTE eNODEb and 5G NR nodes. 
5G NR nodes (leveraging the Wifi spectrum).
- The Ethernet cables act as the backhaul network between the EPC and eNodeB/5G NR.
- a PI enabling its WIFI access point acts 5G NR nodes and spectrum.
- a PI enabling its Bluetooth as an Personal Area Network acts an LTE or eLTE eNodeB (and spectrum)

<!--more-->

![](/images/hack4easy/LTE_to_5G.png)
![](/images/hack4easy/callflow.png)

{{%children style="h3" description="false" depth="1" sort="weight" %}}

