# What is Dedicated Block Storage Cluster?

Dedicated Block Storage Cluster is a block storage service that offers physical isolation and allows you exclusive access to the entire block storage cluster.

## Feature description

A dedicated block storage cluster is a block storage cluster in which you have exclusive access to its resources. As the only user of the block storage cluster, you do not need to share its physical resources with other users. You can view the performance monitoring information and exception information of the cluster.

Compared with public cloud block storage clusters, dedicated block storage clusters offer physical isolation and exclusive resources. After you purchase a dedicated block storage cluster, you can create a dedicated cloud disk on the cluster. All physical resources related to the disk exclusively belong to you. The cloud disk created by using the dedicated block storage cluster can be attached to an ECS instance within the zone where the dedicated block storage cluster is located, including ECS instances that are deployed on dedicated hosts.

![Dedicated block storage cluster](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1769646161/p246410.png)

**Note:** The dedicated block storage cluster feature is available in the China \(Heyuan\), China \(Ulanqab\), and Indonesia \(Jakarta\) regions. The number of supported regions is increasing.

## Scenarios

Dedicated block storage clusters are physically isolated from other public cloud block storage clusters. After you purchase a dedicated block storage cluster, the cluster is yours exclusively. The dedicated block storage cluster feature is suited for industries that have strict data security requirements, such as finance, healthcare, and government.

## Limits

The following table describes the limits of the dedicated block storage cluster feature.

|Item|Limit|
|----|-----|
|Cluster capacity|-   Minimum capacity: 72 TiB
-   Maximum capacity: 2,304 TiB

**Note:** The cluster capacity can be increased by an increment of only 12 TiB, and cannot be customized. |
|Disk category|Only enhanced SSDs \(ESSDs\) of the PL1 performance level can be created. For more information about PL1 ESSDs, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md). |

## Lifecycle management

The following figure shows the lifecycle of a dedicated block storage cluster from its creation to O&M and then release.

![Lifecycle management](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2148846161/p246126.png)

