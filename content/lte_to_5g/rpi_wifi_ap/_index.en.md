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
    loop kernel
        5GNR_WorkerPI->5GNR_WorkerPI: wlan0 - eth0 
    end
    5GNR_WorkerPI->>5GC_MasterPI: eth0/backhaul IP traffic
    loop kernel
        5GC_MasterPI->5GC_MasterPI: eth0 - wlan0 
    end
    5GC_MasterPI->>MPLSNetwork: wlan0/core IP traffic
    MPLSNetwork->>5GC_MasterPI: IP traffic
    5GC_MasterPI->>5GNR_WorkerPI: IP traffic
    5GNR_WorkerPI->>UE_PC: IP traffic
{{< /mermaid >}}

{{%children style="h3" description="false" depth="1" sort="weight" %}}

![](/images/networks/wlan0_pict1.png)
