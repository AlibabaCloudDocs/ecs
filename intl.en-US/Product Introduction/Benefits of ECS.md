# Benefits of ECS {#concept_c1y_bp2_vdb .concept}

Compared with Internet Data Centers \(IDCs\) and server vendors, ECS has benefits in terms of availability, security, and elasticity.

## Availability {#section_jrm_cv4_ydb .section}

Alibaba Cloud adopts more stringent IDC standards, server access standards, and O&M standards to guarantee data reliability and high availability of cloud computing infrastructure and cloud servers.

In addition, each Alibaba Cloud region consists of multiple zones. For greater fault tolerance, you can build active/standby or active/active services in multiple zones. For a finance-oriented solution with three IDCs in two regions, you can build fault tolerant systems in multiple regions and zones. Those services include disaster tolerance and backup, which are supported by the mature solutions built by Alibaba Cloud.

Switching between services is smooth within the Alibaba Cloud framework. For more information, see [E-Commerce Solutions](https://www.alibabacloud.com/solutions). Alibaba Cloud industry solutions support a variety of services, such as finance, E-commerce, and video services.

Alibaba Cloud provides you with the following support services:

-   Products and services for availability improvement, including cloud servers, Server Load Balancer, multi-backup databases, and Data Transmission Services \(DTS\).

-   Industry partners and ecosystem partners that help you build a more advanced and stable architecture and guarantee service continuity.

-   Diverse training services that enable you to connect with high availability from the business end to the underlying basic service end.


## Security {#section_lrm_cv4_ydb .section}

For cloud computing users, security and stability are priorities. Alibaba Cloud has passed a host of international information security certifications, including ISO 27001 and MTCS, which demand strict confidentiality of user data and user information, as well as user privacy protection. We recommend that you use ECS in an [Alibaba Cloud Virtual Private Cloud \(VPC\)](../../../../intl.en-US/Product Introduction/What is VPC?.md#).

-   Alibaba Cloud VPC offers more business possibilities.

    You only need to perform a simple configuration to connect your business environment to global IDCs, making your business more flexible, stable, and extensible.

-   Alibaba Cloud VPC can connect to your IDC

    through a leased line to build a hybrid cloud architecture. You can build a more flexible business with robust networking derived from Alibaba Cloud’s various hybrid cloud solutions and network products. A superior business ecosystem is made possible with Alibaba Cloud’s ecosystem.

-   Alibaba Cloud VPC is more stable and secure.

    Stable: After you build your business on VPC, you can update your network architecture and obtain new network functions on a daily basis as the network infrastructure evolves constantly, allowing your business to run steadily. You can divide, configure, and manage your network on VPC according to your needs.

    Secure: VPC features traffic isolation and attack isolation to protect your services from attack traffic on the Internet. By building your business on VPC, the first line of defense is established.


VPC provides a stable, secure, fast-deliverable, self-managed, and controllable network environment. VPC hybrid cloud brings the technical advantages of cloud computing to traditional industries, in addition to industries and enterprises that are not engaged in cloud computing.

## Elasticity {#section_nrm_cv4_ydb .section}

Elasticity is a key benefit of cloud computing. Elasticity is a key benefit of cloud computing. By using Alibaba Cloud, you can have all the IT resources necessary to get an IT company of medium size provisioned within minutes. The available resources and capacities can meet the requirements of most companies, allowing their applications built on the cloud to handle a huge volume of transactions without problems.

-   Elastic computing

    -   Vertical scaling involves modifying the configurations of a server.

        After you purchase ECS or storage capacity of Alibaba Cloud, you can configure your server with great flexibility based on your actual transaction volume, whereas it may be difficult to change configurations in the traditional IDC model. For more information about vertical scaling, see [Change configurations](../../../../intl.en-US/Instances/Change configurations/Overview of configuration changes.md#).

    -   Horizontal scaling

        Horizontal scaling allows the re-division of resources between applications. For example, at peak hours for game or live video streaming apps, in the traditional IDC model, your hands may be tied if additional resources are required when you are already at full capacity. Cloud computing uses elasticity to provide additional resources to you over that period. When the period ends, you can release unnecessary resources to reduce your business costs. By using both horizontal scaling and auto-scaling that Alibaba Cloud provides, you can determine how and when you scale your resources or apply your scaling based on business loads. For more information about horizontal scaling, see [Auto Scaling](https://www.alibabacloud.com/help/doc-detail/25857.htm).

-   Elastic storage

    Alibaba Cloud provides elastic storage. In the traditional IDC model, if more storage space is required, you can only add servers, but the number of servers that you can add is limited. In the cloud computing model, however, the sky is the limit. Order as much storage space as you need to meet business demand. For more information about elastic storage, see [Resize a disk](../../../../intl.en-US/Block Storage/Block storage/Resize cloud disks/Disk resizing overview.md#).

-   Elastic network

    Alibaba Cloud features elastic network as well. When you purchase Alibaba Virtual Private Cloud \(VPC\), you can set network configurations to be the same as those of data centers. In addition, VPC has the following benefits: interconnection between data centers, separate secure domains in data centers, and flexible network configurations and planning within the VPC For more information about elastic networks, see [Virtual Private Cloud](../../../../intl.en-US/Product Introduction/What is VPC?.md#).


Alibaba Cloud incorporates elasticity in computing, storage, network, and business architecture design. By using Alibaba Cloud, you can build your business portfolio in any way you want.

## Comparison between ECS and traditional IDCs {#section_rrm_cv4_ydb .section}

The table lists the benefits of ECS compared with traditional IDCs.

|Item|ECS|Traditional IDCs|
|:---|:--|:---------------|
|Equipment rooms|Provides independently developed DC powered servers with low PUE.|Provides traditional AC powered servers with high PUE.|
|Provides backbone equipment rooms with high outbound bandwidth and dedicated bandwidth.|Provides equipment rooms with various quality levels and shared bandwidth primarily, difficult for users to choose.|
|Provides multiline BGP equipment rooms, enabling smooth and balanced access throughout the world.|Provides equipment rooms with single or dual line primarily.|
|Ease of operation|Provides built-in mainstream OSs, including activated Windows OS.|Purchases and installs OS manually.|
|Switches OS online.|Reinstalls OSs manually.|
|Provides a Web-based console for online management.|Users must manage and maintain network manually.|
|Provides mobile phone verification for password setting, increasing data security.|Has difficulty in resetting passwords, and exposes high risk of password cracking.|
|Disaster recovery and backup|Each data segment has multiple copies. When one copy is corrupted, the data can be quickly restored.|Users must build disaster recovery environment by themselves, and use traditional storage devices.|
|Users can customize automatic snapshot policies to create automatic snapshots for data recovery.|Users must restore all corrupted data manually.|
|Faults can be recovered fast and automatically.|Faults cannot be recovered automatically.|
|Security and reliability|Effectively prevents MAC spoofing and ARP attacks.|Fails to prevent MAC spoofing and ARP attacks.|
|Effectively defends against DDoS attacks by using black holes and cleaning traffic.|Needs additional costs for devices for traffic cleaning and black hole shielding systems.|
|Provides additional services, such as port scanning, Trojan scanning, and vulnerability scanning.|Typically encountered problems such as vulnerability, Trojan, and port scanning.|
|Flexible scalability|Activates cloud servers on demand and upgrades configurations online.|Needs a long time for server delivery.|
|Adjusts outbound bandwidth as required.|One-off purchase of outbound bandwidth, unable to adjust.|
|Combines with Server Load Balancer online, enabling scaling up applications quickly and easily.|Uses hardware-based server load balancing, which is expensive and extremely difficult to set up.|
|Cost effectiveness|Low cost.|High cost.|
|Small up front investment.|Large up front investment, possible waste of resources.|
|Purchases on demand and pay as you go, meeting requirements for constant business changes.|Purchases up front to meet configuration requirements for peak hours.|

