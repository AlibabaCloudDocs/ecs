---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# Shared instance families

This topic describes the features of shared instance families and lists the instance types of each instance family.

[Previous-generation shared instance families xn4, n4, mn4, and e4](#section_9zj_1ov_92r)

Shared instances use a CPU-unbound scheduling scheme. Each vCPU is randomly allocated to an idle CPU hyperthread. vCPUs of different instances compete for CPU resources, which causes computing performance to fluctuate when traffic loads are heavy. Shared instances can ensure only availability but not performance that may be required in the SLA. Different from enterprise-level instances that have exclusive resources, shared instances share resources. Therefore, shared instances cannot ensure consistent computing performance but offer lower costs.

**Note:** Burstable instances are also shared instances. For more information, see [Overview](/intl.en-US/Instance/Instance type families/Burstable instance types/Overview.md).

## Previous-generation shared instance families xn4, n4, mn4, and e4

Features

-   Offers multiple CPU-to-memory ratios.
-   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) processors.
-   Uses the DDR4 memory.

|Instance family|Description|vCPU-to-memory ratio|Scenario|
|:--------------|:----------|:-------------------|:-------|
|xn4|Compact type|1:1|-   Frontend web applications
-   Lightweight applications and microservices
-   Development and testing environments |
|n4|Shared compute type|1:2|-   Websites and web applications
-   Development environments, servers, code repositories, microservices, and testing and staging environments
-   Lightweight enterprise applications |
|mn4|Shared balanced type|1:4|-   Websites and web applications
-   Lightweight databases and caches
-   Integrated applications and lightweight enterprise services |
|e4|Shared memory type|1:8|-   Applications that require a large memory
-   Lightweight databases and caches |

xn4

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.xn4.small|1|1.0|0.5|50|1|2|2|

**Note:**

-   When you bind an elastic network interface \(ENI\) to or unbind an ENI from an instance of the ecs.xn4.small instance type, the instance must be in the Stopped state.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

n4

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.n4.small|1|2.0|0.5|50|1|2|2|
|ecs.n4.large|2|4.0|0.5|100|1|2|2|
|ecs.n4.xlarge|4|8.0|0.8|150|1|2|6|
|ecs.n4.2xlarge|8|16.0|1.2|300|1|2|6|
|ecs.n4.4xlarge|16|32.0|2.5|400|1|2|6|
|ecs.n4.8xlarge|32|64.0|5.0|500|1|2|6|

**Note:**

-   When you bind an ENI to or unbind an ENI from an instance of the ecs.n4.small or ecs.n4.large instance type, the instance must be in the Stopped state.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

mn4

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.mn4.small|1|4.0|0.5|50|1|2|2|
|ecs.mn4.large|2|8.0|0.5|100|1|2|2|
|ecs.mn4.xlarge|4|16.0|0.8|150|1|2|6|
|ecs.mn4.2xlarge|8|32.0|1.2|300|1|2|6|
|ecs.mn4.4xlarge|16|64.0|2.5|400|1|2|6|
|ecs.mn4.8xlarge|32|128.0|5|500|2|8|6|

**Note:**

-   When you bind an ENI to or unbind an ENI from an instance of the ecs.mn4.small or ecs.mn4.large instance type, the instance must be in the Stopped state.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

e4

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.e4.small|1|8.0|0.5|50|1|2|2|
|ecs.e4.large|2|16.0|0.5|100|1|2|2|
|ecs.e4.xlarge|4|32.0|0.8|150|1|2|6|
|ecs.e4.2xlarge|8|64.0|1.2|300|1|3|6|
|ecs.e4.4xlarge|16|128.0|2.5|400|1|8|6|

**Note:**

-   When you bind an ENI to or unbind an ENI from an instance of the ecs.e4.small or ecs.e4.large instance type, the instance must be in the Stopped state.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## References

-   [Instance families](/intl.en-US/Instance/Instance families.md)
-   [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md)

