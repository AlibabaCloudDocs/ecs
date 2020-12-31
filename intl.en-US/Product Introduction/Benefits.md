# Benefits

Compared with Internet Data Centers \(IDCs\) and common cloud servers, Elastic Compute Service \(ECS\) has the benefits of high availability, security, and scalability.

## High availability

Alibaba Cloud adopts more stringent IDC standards, server access standards, and O&M standards to ensure data reliability and high availability of the cloud computing infrastructure and ECS instances.

Each Alibaba Cloud region has multiple zones. You can create active/standby or active/active ECS instances in multiple zones to achieve higher availability. You can build fault tolerant systems across multiple regions and zones to implement a financial-grade solution that spans three data centers across two regions. Alibaba Cloud provides mature solutions for fault tolerant services such as disaster recovery.

The Alibaba Cloud framework allows you to seamlessly switch between services. For more information about industry solutions, see [Solutions by industry](https://www.alibabacloud.com/solutions). Alibaba Cloud industry solutions support a variety of services, such as finance, e-commerce, and video services.

Alibaba Cloud provides you with the following support services:

-   Products and services for high availability, such as Elastic Compute Service \(ECS\), Server Load Balancer \(SLB\), ApsaraDB Relational Database Service \(RDS\), and Data Transmission Service \(DTS\).
-   Industry partners and ecosystem partners that help you build a more advanced and stable architecture and ensure service continuity.
-   Diverse training services that help you achieve high availability from businesses to underlying services.

## Security

Alibaba Cloud has passed a host of international information security certifications, such as ISO 27001 and MTCS. These certifications require to keep user data, profile, and privacy strictly confidential.

We recommend that you use ECS in a virtual private cloud \(VPC\). VPCs provide a stable, secure, controllable network environment that can be delivered in a short period of time. The capability and architecture of VPC hybrid cloud bring the technical advantages of cloud computing to enterprises in traditional industries that have not implemented cloud computing. For more information, see [Alibaba Cloud Virtual Private Cloud](/intl.en-US/Product Introduction/What is a VPC?.md).

-   Breadth of network products

    You need only to perform a simple configuration to connect your business environment to global IDCs, making your business more flexible, stable, and scalable.

-   Interconnection with your IDC

    You can use Express Connect to connect Alibaba Cloud VPC to your IDC to build a hybrid cloud architecture. You can use a variety of hybrid cloud architectures to provide network services and robust networking.

-   Stability

    After you build a VPC, you can update your network architecture and obtain new network features on a daily basis to constantly evolve your network infrastructure and ensure that your business is always running steadily.

-   Security

    VPC features traffic isolation and attack isolation to protect your services from cyber attacks. After you build your business in a VPC, the first line of defense is established.


## Elasticity

Elasticity is a key benefit of cloud computing. Alibaba Cloud is capable of providing IT resources required by a medium-sized Internet enterprise within a few minutes. In this way, most enterprises that build business on the cloud can process huge business volumes.

Alibaba Cloud provides elastic computing, storage, networking, and business architecture planning and allows you to combine your businesses.

-   Elastic computing
    -   Vertical scaling

        Vertical scaling is the process where the configurations of an ECS instance are modified. After you purchase an ECS instance or storage capacity from Alibaba Cloud, you can configure the instance based on your transaction volume, whereas it may be difficult to change the configurations of a server in a traditional IDC. For more information about vertical scaling, see [Overview of instance upgrade and downgrade](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.md).

    -   Horizontal scaling

        Horizontal scaling allows the re-division of resources between applications. A traditional IDC may not be able to immediately provide sufficient resources for online gaming or live video streaming applications during peak hours. The elasticity of cloud computing makes it possible to provide the resources required during peak hours. When the load returns to normal levels, you can release unnecessary resources to reduce operation costs. The combination of ECS vertical and horizontal elasticity enables you to scale resources up and down by specific quantities as scheduled or against business load. For more information about horizontal scaling, see [What is Auto Scaling?](/intl.en-US/Product Introduction/What is Auto Scaling?.md).

-   Elastic storage

    In a traditional IDC, you must add servers to increase the storage space. However, the number of servers that you can add is limited. Alibaba Cloud provides unlimited storage capacity and allows you to order as much storage space based on the business requirements. For more information about elastic storage, see [Resize a disk](/intl.en-US/Block Storage/Resize cloud disks/Overview.md).

-   Elastic network

    Alibaba Cloud VPCs are flexible to scale. You can configure Alibaba Cloud VPCs in the same ways as you would do with IDCs. In addition, VPCs have the following benefits: interconnection between data centers, separate secure domains in data centers, and flexible network configurations and planning within a VPC. For more information about elastic networks, see [Virtual Private Cloud](/intl.en-US/Product Introduction/What is a VPC?.md).


## Comparison between ECS and traditional IDCs

The following table lists the benefits of ECS compared with traditional IDCs.

|Item|ECS|Traditional IDC|
|:---|:--|:--------------|
|Equipment room deployment|Provides DC-powered servers that are developed by Alibaba Cloud and have low power usage effectiveness \(PUE\).|Provides traditional AC-powered servers with high PUE.|
|Provides backbone equipment rooms with high outbound bandwidth and dedicated bandwidth.|Provides equipment rooms with various quality levels and shared bandwidth primarily, difficult for users to choose from.|
|Provides multi-line Border Gateway Protocol \(BGP\) computer rooms, which enables smooth and balanced access among regions.|Provides equipment rooms with a single or dual line primarily.|
|Ease of operation|Provides mainstream OSs, including activated Windows OS.|Requires users to purchase and install OSs manually.|
|Easily switches between OSs online.|OSs have to be manually reinstalled.|
|Provides a Web-based console for online management.|Users must manually perform management and maintenance operations.|
|Provides mobile phone verification for password setting, increasing data security.|Brings difficulty in resetting passwords, and exposes high risk of password cracking.|
|Disaster recovery and backup|Stores three copies of each piece of data. When one copy is corrupted, the data can be quickly restored.|Users must build a disaster recovery environment by themselves, and use traditional storage devices.|
|Users can customize automatic snapshot policies to create automatic snapshots for data recovery.|Does not support automatic recovery because the snapshot function is not provided.|
|Hardware failures can be recovered quickly and automatically.|Users must restore corrupted data manually.|
|Security and reliability|Effectively prevents MAC spoofing and ARP attacks.|Fails to prevent MAC spoofing and ARP attacks.|
|Effectively defends against DDoS attacks by using black holes and traffic scrubbing.|Needs additional costs for devices for traffic scrubbing and black hole shielding systems.|
|Provides additional services, such as port scanning, trojan scanning, and vulnerability scanning.|Typically encounters problems such as port scanning, trojan scanning, and vulnerability scanning.|
|Flexible scalability|Activates cloud servers on demand and upgrades configurations online.|Needs a long time for server delivery.|
|Adjusts outbound bandwidth as required.|Requires one-off purchase of outbound bandwidth that cannot be adjusted.|
|Combines with SLB online, which makes it easy to scale up applications.|Uses hardware-based server load balancing, which is expensive and difficult to set up.|
|Cost effectiveness|Low cost.|High cost.|
|Small up-front investment.|Large up-front investment, causing serious waste of resources.|
|Provides pay-as-you-go and flexible payment options to allow you to flexibly respond to business changes.|Requires users to purchase up front to meet configuration requirements during peak hours.|

