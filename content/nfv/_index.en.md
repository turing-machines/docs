+++
title = "NFV/SDN/Network Slicing"
description = "This is nfv tutorial page"
weight = 20 
pre = "<b>4. </b>"
chapter = true
+++

# Network Slicing

Finally currently when the traffic is following through WIFI to ETH0 on the 5G NR node and from ETH0 to WIFI on the EPC node, the routing of the 
traffic is done using Linux Kernel mainly.
The goal here is to build an NFV able to throttle for instance the traffic wifi network (simulating 5G) in order to create a simulation of 
network slicing. At that point the traffic on the 5G NR node will not go through the kernel but will go from WIFI through the NFV back to ETH0. 

<!--more-->

{{<mermaid>}}
sequenceDiagram
    participant PC
    participant Phone
    participant 5GNR_WorkerPI
    participant 5GC_MasterPI
    participant MPLSNetwork
    PC->>5GNR_WorkerPI: Establish RAN Connection
    5GNR_WorkerPI->>PC: Return IP
    Phone->>5GNR_WorkerPI: Establish RAN Connection
    5GNR_WorkerPI->>Phone: Return IP
    PC->>5GNR_WorkerPI: wlan0/ran IP traffic
    Phone->>5GNR_WorkerPI: wlan0/ran IP traffic
    loop NFV
        5GNR_WorkerPI->5GNR_WorkerPI: Prioritize ran->backhaul traffic
    end
    5GNR_WorkerPI->>5GC_MasterPI: eth0/backhaul IP traffic
    loop NFV
        5GC_MasterPI->5GC_MasterPI: Prioritize backhaul->core Traffic
    end
    5GC_MasterPI->>MPLSNetwork: wlan0/core IP traffic
    MPLSNetwork->>5GC_MasterPI: IP traffic
    loop NFV
        5GC_MasterPI->5GC_MasterPI: Prioritize core->backhaul Traffic
    end
    5GC_MasterPI->>5GNR_WorkerPI: IP traffic
    loop NFV
        5GNR_WorkerPI->5GNR_WorkerPI: Prioritize backhaul->ran traffic
    end
    5GNR_WorkerPI->>Phone: IP traffic
    5GNR_WorkerPI->>PC: IP traffic
{{< /mermaid >}}

{{%children style="h3" description="false" depth="1" sort="weight" %}}

![](/images/hack4easy/logo_akraino_edge_stack.png)
![](/images/hack4easy/logo_fdio_header.png)
![](/images/hack4easy/logo_onap_2017.png)
![](/images/hack4easy/opnfv_logo_wp.png)
