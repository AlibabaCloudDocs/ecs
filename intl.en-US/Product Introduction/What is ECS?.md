# What is ECS?

Elastic Compute Service \(ECS\) is a high-performance, stable, reliable, and scalable IaaS-level service provided by Alibaba Cloud. ECS eliminates the need to invest in IT hardware up front and allows you to quickly scale computing resources on demand. This makes ECS more convenient and efficient than physical servers. ECS provides a variety of instance types that suit different business needs and help boost business growth.



## Why ECS?

ECS provides the following benefits:

-   You do not need to purchase hardware or construct data centers.
-   ECS instances can be delivered within minutes. This enables rapid deployment and reduces time to market.
-   You can connect ECS instances to data centers including Border Gateway Protocol \(BGP\) computer rooms around the world.
-   You can scale resources up or down based on your actual business needs at a transparent, easy-to-understand cost.
-   x86 architecture-based ECS instances, ECS Bare Metal instances, and heterogenous computing ECS instances such as GPU-accelerated and FPGA-accelerated instances are provided.
-   You can use ECS to access other Alibaba Cloud services over the internal network, reducing Internet traffic costs.
-   A host of security solutions such as virtual firewalls, role-based permission control, internal network isolation, virus protection, and traffic throttling are provided.
-   ECS comes with a performance monitoring framework and active O&M system.
-   A standardized API is provided to improve ease-of-use and applicability.

For more benefits, see [Benefits of ECS](/intl.en-US/Product Introduction/Benefits.md) and [Scenarios](/intl.en-US/Product Introduction/Scenarios.md).

## Architecture

ECS comprises the following major components:

-   [Instance](/intl.en-US/Instance/Overview.md): An ECS instance is a virtual server that includes basic computing components such as CPU, memory, operating system, bandwidth, and disks. The computing performance, memory specifications, and applicable scenarios of an instance are determined by its instance type. Each instance type has particular specifications, including the number of vCPUs, memory capacity, and network performance.
-   [Image](/intl.en-US/Images/Image overview.md): Images provide operating systems, initial application data, and pre-installed software for instances. Multiple Linux distributions and Windows Server operating systems are supported.
-   [Elastic Block Storage](/intl.en-US/Block Storage/Block Storage overview/Block Storage overview.md): Elastic Block Storage \(EBS\) devices offer high performance and low latency. ECS comes with distributed storage architecture-based cloud disksand physical storage-based local disks.
-   [Snapshot](/intl.en-US/Snapshots/Snapshot overview.md): A snapshot is a stateful data file of a cloud disk at a certain point in time. Snapshots are often used to back up and restore data or to create custom images.
-   [Security group](/intl.en-US/Security/Security groups/Overview.md): A security group is a logical grouping of instances located within the same region that have the same security requirements and require access to each other. A security group works as a virtual firewall for the ECS instances inside it.
-   [Network](/intl.en-US/Network/Network types.md):
    -   [Virtual private cloud \(VPC\)](/intl.en-US/Product Introduction/What is a VPC?.md): A VPC is a logically isolated private cloud network. You can configure a private IP address range, a route table, and a gateway for a VPC.
    -   Classic network: All classic network-type instances are built on a shared infrastructure network that is centrally planned and managed by Alibaba Cloud.

For more information, see the [Product page of Elastic Compute Service](https://www.alibabacloud.com/product/ecs).

The following figure shows the architecture of ECS components. For more information about the functional components in the figure, see the ECS documentation.

![whatIsECS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2750056951/p48636.png)

## Pricing

ECS supports multiple billing methods such as subscription and pay-as-you-go and purchasing options such as reserved instances and preemptible instances. For more information, see [Billing overview](/intl.en-US/Pricing/Billing overview.md) and the Pricing tab of the [Product page of Elastic Compute Service](https://www.alibabacloud.com/product/ecs).

## Management tools

After you register an Alibaba Cloud account, you can create, use, or release ECS instances in any region by using one of the following methods provided by Alibaba Cloud:

-   ECS console: a web service page used to manage ECS instances. For more information, see [Quick reference](/intl.en-US/Best Practices/Quick reference.md).
-   ECS API: an RPC API that supports GET and POST requests. For more information, see [API Reference](/intl.en-US/API Reference/Introduction.md). The following developer tools can be used to call ECS API operations:
    -   [Alibaba Cloud CLI](): a flexible and scalable management tool based on Alibaba Cloud APIs. You can use CLI to encapsulate Alibaba Cloud native APIs to develop custom features.
    -   [OpenAPI Explorer](https://api.aliyun.com/): allows you to retrieve API operations, call API operations, and dynamically generate SDK sample code.
    -   [Alibaba Cloud SDK](https://next.api.aliyun.com/api-tools/sdk/Ecs?version=2014-05-26): SDKs for a variety of programming languages such as Java, Python, and PHP are provided.
-   [Resource Orchestration Service \(ROS\)](/intl.en-US/Product Introduction/What is ROS?.md): automatically creates and configures Alibaba Cloud resources based on user-defined templates.
-   [Terraform](/intl.en-US/Elasticity/Terraform/What is Terraform?.md): an open source tool that uses configuration files to call computing resources of Alibaba Cloud and other platforms that support Terraform. Terraform also implements version control.

## Deployment suggestions

Before you purchase an ECS instance, consider the following factors:

-   Region and zone

    A region represents an Alibaba Cloud data center. The region and zone determine the physical location of an ECS instance. After an instance is created, its metadata is established and its region cannot be changed. You can obtain metadata only of the ECS instances located within VPCs. Select a region and zone based on the target geographical location, availability of Alibaba Cloud services, application availability requirements, and whether internal network communication is required. For example, if you want to access both ECS and ApsaraDB RDS, the ApsaraDB RDS instance and ECS instance must be within the same region. For more information, see [Regions and zones]().

-   High availability

    To ensure business consistency and continuity, we recommend that you use snapshots to back up data, and use multi-zone deployment, deployment sets, and Server Load Balancer \(SLB\) for disaster recovery.

-   Set up network connections

    We recommend that you use VPC to plan your own private IP addresses. VPC supports all new features and new instance types. VPC also supports business system isolation and multi-region system deployment. For more information, see [What is a VPC?](/intl.en-US/Product Introduction/What is a VPC?.md)

-   Security solutions

    You can use ECS security groups to control inbound and outbound access policies and the port listening status of ECS instances. For applications deployed on ECS instances, Alibaba Cloud provides Anti-DDoS Basic for free. You can also use Alibaba Cloud Security. For example:

    -   You can use Anti-DDoS Pro to ensure the stability and reliability of source sites. For more information, see [What is Anti-DDoS Pro](/intl.en-US/Anti-DDoS Pro Service (Old)/Product Introduction/What is Anti-DDoS Pro.md).
    -   Security Center can be used to safeguard the security of ECS instances. For more information, see [What is Security Center?](/intl.en-US/Product Introduction/What is Security Center.md)

## Related services

Together with ECS, you can select the following Alibaba Cloud services:

-   Auto Scaling: automatically adjusts the number of ECS instances based on business and policy changes. For more information, see [What is Auto Scaling?](/intl.en-US/Product Introduction/What is Auto Scaling?.md)
-   Dedicated Host \(DDH\): allows you to deploy ECS instances on a dedicated host to have dedicated use of its physical resources. DDH also allows you to migrate your businesses to the cloud at minimal costs while meeting compliance requirements. For more information, see [What is DDH?](/intl.en-US/Product Introduction/What is DDH?.md)
-   Container Service for Kubernetes: manages application lifecycles on groups of ECS instances. For more information, see [What is Container Service for Kubernetes?](/intl.en-US/Product Introduction/What is Container Service for Kubernetes?.md)
-   Server Load Balancer \(SLB\): distributes traffic among multiple ECS instances. For more information, see [What is Server Load Balancer?](/intl.en-US/Classic Load Balancer/Product Introduction/What is CLB?.md)
-   CloudMonitor: develops monitoring solutions for instances, system disks, and public bandwidth. For more information, see [Overview](/intl.en-US/Product Introduction/What is Cloud Monitor?.md).
-   ApsaraDB RDS: provides database services accessible over internal networks to ECS instances, reduces network latency and access fees, and delivers top-notch performance. ApsaraDB RDS supports multiple database engines, including MySQL, SQL Server, PostgreSQL, PPAS, and MariaDB. For more information, see [What is ApsaraDB RDS?](/intl.en-US/Product Introduction/What is ApsaraDB for RDS?.md)
-   [Alibaba Cloud Marketplace](https://www.alibabacloud.com/marketplace): a platform where third-party partners provide software infrastructure, business software, and various software and services related to website construction, hosted O&M, security, data, APIs, and solutions. You can also provide software and services as a service provider in Alibaba Cloud Marketplace.

For more solutions, see [Alibaba Cloud solutions](https://www.alibabacloud.com/solutions).

