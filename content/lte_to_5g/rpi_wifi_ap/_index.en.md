+++
title = "WIFI AP"
menuTitle = "WIFI AP"
description = "This is lte_to_5g/rpi_wifi_bluetooth tutorial page"
weight = 5 
pre = "<b>3.1. </b>"
chapter = true
+++

# WIFI AP

{{<mermaid>}}
sequenceDiagram
    participant UE_PC
    participant 5GNR_WorkerPI
    participant 5GC_MasterPI
    participant MPLSNetwork
    UE_PC->>5GNR_WorkerPI: Establish RAN Connection
    5GNR_WorkerPI->>UE_PC: Return IP
    UE_PC->>5GNR_WorkerPI: wlan0/ran IP traffic
    loop Linux NAT
        5GNR_WorkerPI->5GNR_WorkerPI: translate wlan0 IP into eth0 IP
    end
    5GNR_WorkerPI->>5GC_MasterPI: eth0/backhaul IP traffic
    loop Linux NAT
        5GC_MasterPI->5GC_MasterPI: translate eth0 IP into wlan0 IP
    end
    5GC_MasterPI->>MPLSNetwork: wlan0/core IP traffic
    MPLSNetwork->>5GC_MasterPI: IP traffic
    5GC_MasterPI->>5GNR_WorkerPI: IP traffic
    5GNR_WorkerPI->>UE_PC: IP traffic
{{< /mermaid >}}

{{% notice info %}}
We are currently using NAT here to keep the simulation simple. It would
be more accurate to use Linux Briding or OVS to simulate the fact that
the SGW running on the EPC is "allocating" the IP address.
{{% /notice %}}

{{%children style="h3" description="false" depth="1" sort="weight" %}}

![](/images/networks/wlan0_pict1.png)
