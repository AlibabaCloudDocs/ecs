# Configure an auto provisioning group

This topic describes how to configure an auto provisioning group based on actual scenarios.

## Machine learning scenarios

For example, you plan to complete a machine learning task in the next week. The task is used to analyze risk factors for mortgage loans. You have the following requirements on the instance cluster:

-   Region: China \(Hangzhou\).
-   Instances: use NVIDIA V100 GPUs, and the GPU memory for a single instance does not exceed 32 GB.
-   Target capacity: 20 instances.
-   To reduce costs, only preemptible instances are created. An instance cluster that does not reach the target capacity is acceptable.
-   Instances must be released after the task is complete.

The following table describes the configurations of the auto provisioning group based on the preceding requirements of the scenario.

|Section|Parameter|Description|
|-------|---------|-----------|
|**Capacity Configuration**|**Target Capacity**|Configure the following settings based on the target capacity and instance category requirements:-   Select **Instances** from the Target Capacity drop-down list.
-   Specify **20** in the spin box |
|**Instance Configuration**|**Instance Configuration**|Select the following instance types that use NVIDIA V100 GPUs and have GPU memory not greater than 32 GB per instance:1.  ecs.gn6v-c8g1.2xlarge and ecs.gn6e-c12g1.3xlarge

**Note:** For more information about instance types, see [Instance families](/intl.en-US/Instance/Instance families.md).

2.  Query the available resources of ecs.gn6v-c8g1.2xlarge and ecs.gn6e-c12g1.3xlarge in Hangzhou Zone H and Hangzhou Zone I.

**Note:** You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.


You can add instance configurations based on the zones and instance types:

1.  Perform the following operations to add an instance configuration:
    -   Specify a vSwitch in Hangzhou Zone H.
    -   Add the ecs.gn6v-c8g1.2xlarge and ecs.gn6e-c12g1.3xlarge instance types.
2.  Perform the following operations to add another instance configuration:
    -   Specify a vSwitch in Hangzhou Zone I.
    -   Add the ecs.gn6v-c8g1.2xlarge and ecs.gn6e-c12g1.3xlarge instance types.

The following resource pools are formed after you add the preceding configurations:

-   The ecs.gn6v-c8g1.2xlarge instance type in Hangzhou Zone H
-   The ecs.gn6e-c12g1.3xlarge instance type in Hangzhou Zone H
-   The ecs.gn6v-c8g1.2xlarge instance type in Hangzhou Zone I
-   The ecs.gn6e-c12g1.3xlarge instance type in Hangzhou Zone I |
|**Provisioning Policy**|Select **Cost Optimization Policy**. After the auto provisioning group is started, the most cost-effective resource pool is used to create an instance cluster.|
|**Advanced**|**Group Type**|An instance cluster that does not reach the target capacity is acceptable to minimize costs. Therefore, select **One-time Delivery**.|
|**Start Time** and **End Time**|Specify the start and expiration time based on the next-week time requirement.|
|**Instance Shutdown Settings**|-   Instances in the auto provisioning group must be released after the task is complete. Therefore, select **Shut Down Instances Upon Group Expiration**.
-   Select **Shut Down Excessive Instances When Target Capacity Is Exceeded** to save cost. |

## Ticketing website scenarios

For example, you need to build a ticketing website to provide reliable ticketing services at all hours, especially during peak hours. You have the following requirements on the instance cluster:

-   Region: China \(Hangzhou\).
-   Instances: The number of vCPUs on a single instance does not exceed eight.
-   Target capacity: 80 vCPUs.
-   Minimum capacity: 60 vCPUs.
-   The website access experience is optimized based on the minimum computing requirements of the cluster to minimize costs.
-   The cluster must have disaster recovery capabilities.

The following table describes the configurations of the auto provisioning group based on the preceding requirements of the scenario.

|Section|Parameter|Description|
|-------|---------|-----------|
|**Capacity Configuration**|**Target Capacity**|Configure the following settings based on the target capacity and minimum capacity requirements:-   Select **vCPUs** from the Target Capacity drop-down list.
-   Specify 80 in the spin box.
-   Select **Use Pay-as-you-go Instances to Provide Computing Power**. |
|**Pay-as-you-go Instance Capacity**|Specify 60 in the spin box to meet the minimum capacity requirement.|
|**Instance Configuration**|**Instance Configuration**|The c6 instance family is used because it is suitable for building frontend web servers. Select the following instance types whose number of vCPUs does not exceed eight:1.  ecs.c6.large, ecs.c6.xlarge, and ecs.c6.2xlarge.

**Note:** For more information about instance types, see [Instance families](/intl.en-US/Instance/Instance families.md).

2.  Query the available resources of ecs.c6.large, ecs.c6.xlarge, and ecs.c6.2xlarge in Hangzhou Zone H, Hangzhou Zone I, and Hangzhou Zone J.

**Note:** You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.


You can add instance configurations based on the zones and instance types:

1.  Perform the following operations to add an instance configuration:
    -   Specify a vSwitch in Hangzhou Zone H.
    -   Add the ecs.c6.large, ecs.c6.xlarge, and ecs.c6.2xlarge instance types.
2.  Perform the following operations to add an instance configuration:
    -   Specify a vSwitch in Hangzhou Zone I.
    -   Add the ecs.c6.large, ecs.c6.xlarge, and ecs.c6.2xlarge instance types.
3.  Perform the following operations to add another instance configuration:
    -   Specify a vSwitch in Hangzhou Zone J.
    -   Add the ecs.c6.large, ecs.c6.xlarge, and ecs.c6.2xlarge instance types.

The following resource pools are formed after you add the preceding configurations:

-   The ecs.c6.large instance type in Hangzhou Zone H
-   The ecs.c6.xlarge instance type in Hangzhou Zone H
-   The ecs.c6.2xlarge instance type in Hangzhou Zone H
-   The ecs.c6.large instance type in Hangzhou Zone I
-   The ecs.c6.xlarge instance type in Hangzhou Zone I
-   The ecs.c6.2xlarge instance type in Hangzhou Zone I
-   The ecs.c6.large instance type in Hangzhou Zone J
-   The ecs.c6.xlarge instance type in Hangzhou Zone J
-   The ecs.c6.2xlarge instance type in Hangzhou Zone J |
|**Provisioning Policy**|Select **Balanced Distribution Policy**. After the auto provisioning group is started, it attempts to evenly create instances across multiple zones to avoid instance creation failures due to insufficient resources in a single zone. This can improve the disaster recovery capabilities of applications.|
|**Advanced**|**Group Type**|Select **Continuous Delivery and Maintain Capacity** to continuously provide ticketing service.|
|**Start Time** and **End Time**|The auto provisioning group starts immediately and can be indefinitely retained to continuously provide ticketing service.|
|**Instance Shutdown Settings**|Select **Shut Down Excessive Instances When Target Capacity Is Exceeded** to save cost.|

The target capacity is specified in terms of vCPUs. Therefore, the weight of each instance is related to the number of vCPUs of each instance type. The following table describes the weighted price of each instance type.

**Note:** Prices in the following table are for reference only. The actual prices displayed on the buy page prevail.

|Instance type|vCPUs|Price \(USD\)|Weight|Weighted price \(USD\)|
|-------------|-----|-------------|------|----------------------|
|ecs.c6.large|2|0.06/Hour|2|0.03/Hour|
|ecs.c6.xlarge|4|0.121/Hour|4|0.03025/Hour|
|ecs.c6.2xlarge|8|0.241/Hour|8|0.030125/Hour|

When an auto provisioning group attempts to create an instance cluster, the auto provisioning group first tries to satisfy the multi-zone balancing policy by evenly creating instances across multiple zones. Then, the auto provisioning group attempts to select instance types that have lower weighted prices to create instances. If the weighted prices of all instance types are the same, the auto provisioning group selects instance types at random to create instances.

