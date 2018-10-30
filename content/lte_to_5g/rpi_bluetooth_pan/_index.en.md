+++
title = "Bluetooth PAN"
menuTitle = "Bluetooth PAN"
description = "This is Bluetooth PAN tutorial page"
weight = 10 
pre = "<b>3.2. </b>"
chapter = true
+++

# Bluetooth PAN

{{<mermaid>}}
sequenceDiagram
    participant UE_PC
    participant ENODEB_WorkerPI
    participant EPC_MasterPI
    participant MPLSNetwork
    UE_PC->>ENODEB_WorkerPI: Establish RAN Connection
    ENODEB_WorkerPI->>UE_PC: Return IP
    UE_PC->>ENODEB_WorkerPI: pan0/ran IP traffic
    loop kernel
        ENODEB_WorkerPI->ENODEB_WorkerPI: pan0 - eth0 
    end
    ENODEB_WorkerPI->>EPC_MasterPI: eth0/backhaul IP traffic
    loop kernel
        EPC_MasterPI->EPC_MasterPI: eth0 - wlan0 
    end
    EPC_MasterPI->>MPLSNetwork: wlan0/core IP traffic
    MPLSNetwork->>EPC_MasterPI: IP traffic
    EPC_MasterPI->>ENODEB_WorkerPI: IP traffic
    ENODEB_WorkerPI->>UE_PC: IP traffic
{{< /mermaid >}}

{{%children style="h3" description="false" depth="1" sort="weight" %}}

![](/images/networks/pan0_pict2.png)
