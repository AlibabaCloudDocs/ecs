---
keyword: [Alibaba Cloud, ECS, select a server, first purchase]
---

# Best practices for instance type selection

To select instance types, you must know their key features. When you know the features of each instance type, you can select appropriate instance types and take full advantage of the elasticity and flexibility of ECS in scenarios such as insufficient resources, retirement of instance families or instance types, and the use of preemptible instances.

This topic describes how to select enterprise-level instance families, instead of entry-level instance families \(also called shared instance families\). For information about how to select entry-level instance families, see [Shared instance families](/intl.en-US/Instance/Instance type families/Shared instance families.md) or [Overview](/intl.en-US/Instance/Instance type families/Burstable performance instances/Overview.md).

## Learn about instance families

When you create an ECS instance, you want to select the most cost-effective and stable instance type to suit your performance, price, and workload needs. Alibaba Cloud provides a variety of instance families suited for different business scenarios with different specifications of vCPUs, memory, network performance, and throughput. An instance family is further divided into multiple instance types. Instance family names are in the ecs. <Instance family\> format, and instance type names are in the ecs. <Instance family\>.<nx\>large format.

-   ecs: the product code of ECS.
-   <Instance family\>: consists of lowercase letters and numbers.
    -   Lowercase letters are abbreviations that indicate the performance fields of instance families. Examples:
        -   c: compute optimized \(computational\)
        -   g: general purpose \(general\)
        -   r: memory optimized \(ram\)
        -   ne: enhanced network performance \(network enhanced\)
    -   Numbers identify the generations to which instance families of the same type belong. A larger number represents a newer generation, and the instance family is more cost-effective and delivers higher performance.
-   <nx\>large: the number of vCPUs that the instance type has. The larger the number n is, the more vCPUs the instance type has.

For example, ecs.g6.2xlarge represents an instance type that belongs to the general purpose instance family g6 and has eight vCPUs. g6 is a newer-generation instance family than g5.

## Select instance types

You can use one of the following methods to view details about instance families and instance types to select an appropriate instance type:

-   [Instance families](/intl.en-US/Instance/Instance families.md): See this topic to learn details about instance families without logging on with an Alibaba Cloud account.
-   DescribeInstanceTypes: Call this API operation to obtain the latest performance specifications of instance types. You must log on with an Alibaba Cloud account to perform this operation.

    ```
    aliyun ecs DescribeInstanceTypes --InstanceTypeFamily ecs.g6
    ```

-   [Pricing](https://www.alibabacloud.com/product/ecs): View the pricing information and latest special offers on the Pricing tab of the ECS product page, and estimate your costs.
-   [Custom Launch](https://ecs-buy.aliyun.com/wizard#/prepay/cn-hangzhou): Click this tab on the instance buy page of the ECS console to learn more about instance purchase instructions in the **Instance Type** section of the **Basic Configurations** step.

## Select instance families based on scenarios

The following figure shows some ECS instance families and the business scenarios for which they are suited.

![Compute optimized instance families](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8023942061/p85750.png)

## Select instance families based on applications

If you are using software or applications similar to those in the following figure, select corresponding instance families from the right side of the figure.

![Select instances based on workloads](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2904488951/p85751.png)

## Select instance families based on user-created services

If you are using user-created services, select instance families based on your services and the selection principles.

|Application type|Common application|Selection principle|Recommended instance family|
|----------------|------------------|-------------------|---------------------------|
|Load balancing|NGINX|Connections can be frequently established. -   CPU computing power: high.
-   Memory: not high.

|c6 and hfc6|
|RPC|-   SOFA
-   Dubbo

|A large amount of memory is available for network connection-intensive workloads.|g6|
|Cache|-   Redis
-   Memcache
-   Solo

|-   CPU computing power: not high.
-   Memory: high.

|-   r6 and re6
-   Elastic Block Storage: standard SSDs or enhanced SSDs \(ESSDs\) |
|Configuration center|ZooKeeper|A large number of I/O operations generated when applications initiate negotiations can be handled. -   CPU computing power: not high.
-   Memory: not high.

|-   c6
-   Elastic Block Storage: standard SSDs or ESSDs |
|Message queues|-   Kafka
-   RabbitMQ

|Disks are preferred for message integrity. -   CPU computing power: not high.
-   vCPU-to-memory ratio: 1:1.
-   Storage: not high.

|-   c6
-   Elastic Block Storage: standard SSDs or ESSDs |
|Container orchestration|Kubernetes|The ECS bare metal instances and containers are combined to maximize computing power.|ebmc6 and ebmg6|
|Large table storage|HBase|-   Typically, d series instance families are suitable.
-   If your business requires ultra-high IOPS, you can select i series instance families.

|-   d1, d1ne, and d2s
-   i2 |
|Database|-   MySQL
-   NoSQL

|-   If your business requires scalable storage, you can select ESSDs.
-   If your business is I/O-sensitive, i series instance families are preferred.

|-   c6, g6, and r6

Elastic Block Storage: ESSDs

-   i2 |
|SQLServer|-   Windows features single-channel I/O configuration while high I/O capabilities are required. ESSDs are recommended.
-   The logical and physical sectors of ECS instances are set to 4 KB in size.

|-   c6, g6, and r6
-   Elastic Block Storage: ESSDs |
|Text search|Elasticsearch|-   Instance types that have high vCPU-to-memory ratios are recommended.
-   I/O capabilities can meet the requirements for exporting database data in the .es format.

|-   g6

Elastic Block Storage: ESSDs

-   d1, d1ne, and d2s |
|Real-time computing|-   Flink
-   Blink

|You can select general purpose instance families and disks or select d series instance families.|d1, d1ne, and d2s|
|Offline computing|-   Hadoop
-   HDFS
-   CDH

|d series instance families are preferred.|d1, d1ne, and d2s|

## Recommended instance families for common scenarios, game applications, and live streaming

These scenarios are CPU compute-intensive. We recommend that you select an instance type with a relatively balanced CPU-to-memory ratio, typically 1:2, use an ultra disk as the system disk, and use standard SSDs or ESSDs as data disks. For scenarios that require higher network performance such as on-screen video comments, you can select an instance type with higher specifications to improve the packet forwarding rate.

|Scenario category|Scenario|Recommended instance family|Performance requirement|CPU-to-memory ratio|
|-----------------|--------|---------------------------|-----------------------|-------------------|
|Common scenarios|Balanced performance applications and backend applications|g series instance families, such as g6|Medium clock speed, compute-intensive|1:4|
|Applications with high packet forwarding rates|g series instance families, such as g6|High packet forwarding rate, compute-intensive|1:4|
|High-performance computation|c series instance families, such as c6|High clock speed, compute-intensive|1:2|
|Game applications|High-performance client games|c series instance families, such as c6|High clock speed|1:2|
|Mobile or web games|g series instance families, such as g6|Medium clock speed|1:4|
|Live streaming applications|Video forwarding|g series instance families, such as g6|Medium clock speed, compute-intensive|1:4|
|On-screen video comments|g series instance families, such as g6|High packet forwarding rate, compute-intensive|1:4|

## Recommended instance families for big data scenarios such as Hadoop, Spark, and Kafka

In these scenarios, the performance requirements are not the same for each node. You must balance the performance of each node, including the computing performance, storage throughput, and network performance.

-   Management nodes: Select an instance family in the same manner as you would in common scenarios. For more information, see the [Recommended instance families for common scenarios, game applications, and live streaming](#section_afz_9jb_404) section.
-   Compute nodes: Select an instance family in the same manner as you would in common scenarios. For more information, see the [Recommended instance families for common scenarios, game applications, and live streaming](#section_afz_9jb_404) section. You must select instance types based on the cluster size. For example, you can select ecs.g6.4xlarge for a cluster that consists of less than 100 nodes and ecs.g6.8xlarge for a cluster that consists of more than 100 nodes.

    **Note:** Preemptible instances can be used as compute nodes to improve cost-effectiveness. For more information, see [Overview](/intl.en-US/Instance/Instance purchasing options/Preemptible instances/Overview.md).

-   Data nodes: require high storage throughput, high network throughput, and balanced CPU-to-memory ratios. We recommend that you use the d series big data instance families. For example, you can select ecs.d1ne.6xlarge for MapReduce and Hive, and ecs.d1ne.8xlarge for Spark and MLib.

![Select instance families from big data instance families](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2904488951/p85841.png)

## Recommended instance families for databases, caches, and search scenarios

Typically, these scenarios require CPU-to-memory ratios of greater than 1:4. Some software in these scenarios is sensitive to latency and storage I/O capabilities. We recommend that you select instance families whose memory is cost-effective.

|Scenario category|Scenario|Recommended instance family|CPU-to-memory ratio|Data disk|
|-----------------|--------|---------------------------|-------------------|---------|
|Relational databases|High-performance and dependent on high availability in the application layer|i series instance families|1:4|Local SSDs, ultra disks, and standard SSDs|
|Small and medium-sized databases|g series instance families, or other instance families that have CPU-to-memory ratios of 1:4|1:4|Ultra disks and standard SSDs|
|High-performance databases|r series instance families|1:8|Ultra disks and standard SSDs|
|Distributed caches|Medium memory usage|g series instance families, or other instance families that have CPU-to-memory ratios of 1:4|1:4|Ultra disks and standard SSDs|
|High memory usage|r series instance families|1:8|Ultra disks and standard SSDs|
|NoSQL databases|High performance and high availability in the application layer|i series instance families|1:4|Local SSDs, ultra disks, and standard SSDs|
|Small and medium-sized databases|g series instance families, or other instance families that have CPU-to-memory ratios of 1:4|1:4|Ultra disks and standard SSDs|
|High-performance databases|r series instance families|1:8|Ultra disks and standard SSDs|
|ElasticSearch|Small clusters that depend on disks to ensure high data availability|g series instance families, or other instance families that have CPU-to-memory ratios of 1:4|1:4|Ultra disks and standard SSDs|
|Large clusters and being dependent on high availability in the application layer|d series instance families|1:4|Local SSDs, ultra disks, and standard SSDs|

The following example uses databases. Traditionally, business systems directly connect to online transaction processing \(OLTP\) databases and data redundancy is implemented by RAID. However, you can use ECS provided by Alibaba Cloud to flexibly deploy both lightly and heavily loaded databases.

-   Lightly loaded databases: use enterprise-level instance families and disks, which are more cost-effective.
-   Heavily load databases: require high storage IOPS and low read/write latency. We recommend that you use i series instance families equipped with local SSDs. The local SSDs are high I/O NVMe SSDs that can meet the requirements of large heavily-loaded databases.

![Select instance families based on databases](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2904488951/p85843.png)

## Recommended instance families for scenarios such as deep learning and image processing

In these scenarios, applications require high-performance GPU accelerators. The following GPU-to-CPU ratios are recommended for different scenarios:

-   Deep learning training: The recommended GPU-to-CPU ratio is from 1:8 to 1:12.
-   General purpose deep learning: The recommended GPU-to-CPU ratio is from 1:4 to 1:48.
-   Image recognition and inference: The recommended GPU-to-CPU ratio is from 1:4 to 1:12.
-   Speech recognition and synthesis inference : The recommended GPU-to-CPU ratio is from 1:16 to 1:48.

The following figure shows the GPU- and FPGA-accelerated instance families recommended for common AI and image or video processing scenarios.

![Select instance families from GPU- and FPGA-accelerated instance families](../images/p169458.png)

## Check and adjust your selection

After you select an instance type to create an instance and start using the instance, we recommend that you check whether the instance type is suitable based on the performance monitoring information.

If you select the ecs.g6.xlarge instance type and find that the CPU utilization is low, we recommend that you log on to the instance to check whether the memory usage is high. If the memory usage is high, you can change to an instance type that has a more suitable CPU-to-memory ratio within another instance family. For more information, see the following topics:

-   [ECS monitoring service](/intl.en-US/Deployment & Maintenance/Monitor the instance status/Query monitoring information of an instance.md)
-   [View the monitoring data of a cloud disk](/intl.en-US/Block Storage/Cloud disks/View the monitoring data of a cloud disk.md)
-   [Overview](/intl.en-US/Host monitoring/Overview.md)

In scenarios such as insufficient resources, retirement of instance families or instance types, changes to more cost-effective instance families, or configuration upgrades, you can upgrade or downgrade the configurations of instances based on instance family features. The following table lists some recommendations for instance configuration changes. For more information, see [Overview of instance upgrade and downgrade](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.md) and [Instance families that support instance type changes](/intl.en-US/Instance/Change configurations/Change instance types/Instance families that support instance type changes.md).

|Current instance families|Preferred target instance family|Alternative target instance family|
|-------------------------|--------------------------------|----------------------------------|
|sn1 and sn2|-   c6
-   g6
-   r6

|-   c5 and sn1ne
-   g5 and sn2ne
-   r5 and se1ne |
|c4|hfc6 and c6|hfc5 and c5|
|ce4|r6|r5 and se1ne|
|cm4|hfc6|hfc5 and g5|
|n1, n2, and e3|-   c6
-   g6
-   r6

|-   c5 and sn1ne
-   g5 and sn2ne
-   r5 and se1ne |
|-   t1
-   s1, s2, and s3
-   m1 and m2
-   c1 and c2

|-   c6
-   g6
-   r6

|-   c5 and sn1ne
-   g5 and sn2ne
-   r5 and se1ne |

## References

For more information about application scenarios, see [Selection of enterprise-level instance types](https://www.alibabacloud.com/product/ecs).

