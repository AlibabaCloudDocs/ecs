# Create an auto provisioning group

This topic describes how to create an auto provisioning group in the Elastic Compute Service \(ECS\) console. The auto provisioning group can create instance clusters based on your configurations.

-   Your account is granted permissions on Auto Provisioning.

    **Note:** The first time you access the Auto Provisioning page, you must follow the instructions to assume the `AliyunECSAutoProvisioningGroupRole` Resource Access Management \(RAM\) role.

-   A launch template is created. For more information, see [Create a launch template](/intl.en-US/Elasticity/Launch template/Create a launch template.md).

    Auto provisioning groups use specific versions of launch templates as instance configuration sources. Properties such as instance images, security groups, and logon credentials from the launch templates are used by auto provisioning groups to create instances.


1.  Go to the Auto Provisioning page.

    1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

    2.  In the top navigation bar, select a region.

    3.  In the left-side navigation pane, choose **Deployment & Elasticity** \> **Auto Provisioning**.

2.  Click **Create Auto Provisioning Group**.

3.  In the **Group Name** field, enter the name for the auto provisioning group.

    The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\).

4.  In the **Target Capacity** section, configure parameters related to the capacity of the auto provisioning group.

    The capacity-related parameters determine the sum of computing power provisioned by the auto provisioning group and the proportions of computing power provided by preemptible and pay-as-you-go instances. The following table describes these parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Target Capacity**|The computing power that the auto provisioning group is scheduled to provision. You can specify this capacity based on **Instances** or **vCPUs**. After you select **Use Pay-as-you-go Instances to Provide Computing Power**, you can specify the computing power provided by the pay-as-you-go instances. By default, only preemptible instances are created. Pay-as-you-go instances are created only after you set Pay-as-you-go Instance Capacity to a value greater than 0. **Note:** If the target capacity involves multiple instance type factors such as vCPUs and memory, call the [CreateAutoProvisioningGroup](/intl.en-US/API Reference/Auto provisioning group/CreateAutoProvisioningGroup.md) operation to create an auto provisioning group and set weights for the specified instance types. |
    |**Pay-as-you-go Instance Capacity**|The target capacity of pay-as-you-go instances that the auto provisioning group is scheduled to provision. You can specify this number of instances. You can use pay-as-you-go instances to ensure that the lowest computing power requirement can be met because preemptible instances may be reclaimed.|

    Auto Provisioning uses the weight of an instance type to indicate the capacity of a single instance of this instance type in an auto provisioning group.

    -   If the target capacity is specified based on **Instances**, the weights of all instance types are the same.
    -   If the target capacity is specified based on **vCPUs**, the weight of an instance type depends on the number of vCPUs. The more vCPUs that an instance type has, the higher the weight of the instance type and the fewer instances of the instance type that are required to meet the target capacity. The following table describes an example in which different weights are set for three instance types based on the number of vCPUs.

        |Instance type|vCPU|Weight|
        |-------------|----|------|
        |ecs.c6.large|2|2|
        |ecs.c6.xlarge|4|4|
        |ecs.c6.2xlarge|8|8|

        **Note:** When you create an auto provisioning group in the ECS console, you do not need to set a weight for each instance type. Weights are automatically assigned based on the number of vCPUs of each instance type.

        If the target capacity is 24 vCPUs, the auto provisioning group can deliver instances of one or more of the ecs.c6.large, ecs.c6.xlarge, and ecs.c6.2xlarge instance types based on their weights to meet the target capacity. Examples:

        -   12 ecs.c6.large instances
        -   8 ecs.c6.large instances and 1 ecs.c6.2xlarge instance
        -   4 ecs.c6.large instances, 2 ecs.c6.xlarge instances, and 1 ecs.c6.2xlarge instance
    -   If the target capacity involves multiple instance type factors such as vCPUs and memory, evaluate the computing power that each specified instance type is able to contribute to the target capacity and set a weight for each instance type. A larger weight indicates that the instance type is able to contribute more computing power. For example, an application requires an instance cluster that provides a total computing power of 20 vCPUs and 48 GiB memory and also requires that the computing power of each instance is a multiple of 2 vCPUs and 4 GiB memory. You can set the target capacity of the auto provisioning group to 48 and set a weight for each instance type, as shown in the following table.

        |Instance type|vCPU|Memory|Weight|
        |-------------|----|------|------|
        |ecs.c6.large|2|4 GiB|4|
        |ecs.c6.xlarge|4|8 GiB|8|
        |ecs.c6.2xlarge|8|16 GiB|16|

        The auto provisioning group can deliver instances of one or more of the ecs.c6.large, ecs.c6.xlarge, and ecs.c6.2xlarge instance types based on their weights to meet the target capacity. Examples:

        -   12 ecs.c6.large instances
        -   8 ecs.c6.large instances and 1 ecs.c6.2xlarge instance
        -   4 ecs.c6.large instances, 2 ecs.c6.xlarge instances, and 1 ecs.c6.2xlarge instance
        **Note:** If the target capacity involves multiple instance type factors such as vCPUs and memory, call the [CreateAutoProvisioningGroup](/intl.en-US/API Reference/Auto provisioning group/CreateAutoProvisioningGroup.md) operation to create an auto provisioning group and set weights for the specified instance types.

5.  In the **Configuration Source** and **Instance Configuration** sections, configure instance properties.

    You can use an auto provisioning group to create instances of multiple instance types across multiple zones. If an instance cannot be created due to insufficient resources of a specific instance type or in a specific zone, the auto provisioning group attempts to create instances of another instance type or create instances in a different zone. This can improve the success rate of creating instances.

    You can specify vSwitches in multiple zones to create instances across multiple zones, and add instance types to create instances of multiple instance types. The following figure shows an example of parameter configurations. For more information, see [Configure an auto provisioning group](/intl.en-US/Elasticity/Manage auto provisioning groups/Configure an auto provisioning group.md).

    ![multi-zone-type](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2359695161/p244716.png)

    Two zones and three instance types are used in the preceding example. The following table describes operations involved in the example.

    |No.|Procedure|
    |---|---------|
    |①|Select a launch template and then a specific version of the launch template as the configuration source. **Note:** When you create instances, the vSwitches and instance types specified in section ② and section ④ are used. However, other properties such as the image, security groups, and logon credential are obtained from the configuration source. |
    |②|Complete instance configurations. By default, the vSwitch and instance type specified in the configuration source are used. You can select other vSwitches, and select or add other instance types. **Note:** You must specify at least one instance configuration for an auto provisioning group. |
    |③|Add an instance configuration to create instances across multiple zones.|
    |④|Complete the instance configuration. The following parameters are required:    -   **Specify**: the vSwitch to which the instances are connected. Make sure that the vSwitch belongs to a zone different from that of the vSwitch specified in section ②.

**Note:** If you specify multiple vSwitches within the same zone, only the first vSwitch takes effect.

    -   **Add Instance Type**: You can select one or more instance types to increase the success rate of creating instances. In this example, two instance types are specified. In the Select Instance Type dialog box, instance types that have the same instance size or vCPU-to-memory ratio as the instance type specified in the selected configuration source are listed. You can also select other instance types. |

    In addition to vSwitches and instance types, you can also set the maximum hourly prices for preemptible instances of each instance type. You can use one of the following methods to set the maximum hourly prices:

    -   Select Automatic Bidding. The real-time market price is used as the maximum hourly price for the bids. This way, preemptible instances do not fail to be created due to low bids. The instance costs are subject to changes to the market price.
    -   Choose Set Maximum Price \> Maximum Price, and set a maximum hourly price. If you select this option, preemptible instances cannot be created if your bid is lower than the market price. This prevents instance costs from spiraling out of control if the market price increases.
    -   Choose Set Maximum Price \> Pay-as-you-go Price, and set a percentage of the pay-as-you-go price to obtain the maximum hourly price. This costs you less than pay-as-you-go prices. For example, if you set the percentage to 50%, preemptible instances fail to be created when the market price is higher than 50% of the pay-as-you-go price.
    **Note:** We recommend that you learn the market price trends of preemptible instances before you set the maximum hourly prices. This way, you can prevent high costs or failures to meet the target capacity. You can click **Price History** in the **Actions** column to view historical prices.

6.  In the **Provisioning Policy** section, select the policy used to create instances.

    The following table describes the options for this parameter.

    |Option|Description|
    |------|-----------|
    |**Capacity Optimization Policy**|The auto provisioning group selects the most cost-effective instance type based on the prices and reclaim rates to create preemptible instances. **Note:** Preemptible instances may be reclaimed due to factors such as price and inventory. Instance types that have low reclaim rates are preferred. |
    |**Cost Optimization Policy**|The auto provisioning group attempts to create ECS instances based on the unit prices of vCPUs in ascending order.|
    |**Balanced Distribution Policy**|The auto provisioning group evenly distributes ECS instances across the zones that are specified in the instance configurations. This parameter takes effect only when multiple zones are specified. The preemptible instances of each instance type are reclaimed together. Instance resources are shared within the same instance family. For example, if an instance of the ecs.c6.large instance type fails to be created, a possible cause is that instance resources in the c6 instance family are insufficient. Instances of other c6 instance types such as ecs.c6.xlarge may also fail to be created.

**Note:** If you select Balanced Distribution Policy, we recommend that you configure instance types from different instance families to prevent instances from being reclaimed at the same time and ensure that your instance clusters remain available. |

7.  Configure advanced options.

    The following table describes the parameters in the Advanced section.

    |Parameter|Description|
    |---------|-----------|
    |**Group Type**|    -   **One-time Delivery**: After the auto provisioning group is started, it tries only once to create an instance cluster that has the target capacity. If the instance cluster fails to be created, the auto provisioning group does not try again to create the instance cluster.
    -   **Continuous Delivery and Maintain Capacity**: After the auto provisioning group is started, it attempts to create an instance cluster until the cluster reaches the target capacity. If the real-time capacity does not match the target capacity, the auto provisioning group scales in or out to meet the target capacity. |
    |**Start Time**|The time when the auto provisioning group is started. The period of time between this point in time and the point in time specified by End Time is the validity period of the auto provisioning group.     -   **Now**: The auto provisioning group is immediately started after it is created.
    -   **Specify Start Time**: Specify a point in time at which to start the auto provisioning group. |
    |**End Time**|The time when the auto provisioning group expires. The period of time between this point in time and the point in time specified by Start Time is the validity period of the auto provisioning group.     -   **Never**: The auto provisioning group never expires and must be manually deleted.
    -   **Specify End Time**: Specify the point in time at which the auto provisioning group expires. |
    |**Global Maximum Price for Preemptible Instances**|The global maximum hourly price for preemptible instances created in the auto provisioning group. This parameter applies to preemptible instances of all instance types. If the global maximum hourly price is different from the maximum hourly price specified for a single instance type in the instance configurations, the lower one of the two prices takes precedence.     -   **Automatic Bidding**: The real-time market price is used as the maximum hourly price for the bids. This way, preemptible ECS instances do not fail to be created due to low bids. The instance costs are subject to changes to the market price.
    -   **Set Maximum Price**: a fixed maximum hourly price. If you select this option, preemptible instances cannot be created if your bid is lower than the market price. This prevents instance costs from spiraling out of control if the market price increases. |

8.  Click **Create Provisioning Group**.


After the auto provisioning group is created, it is started and attempts to create the instance cluster at the specified time. If Group Type is set to **Continuous Delivery and Maintain Capacity**, the auto provisioning group continuously maintains the instance cluster. The auto provisioning group attempts to create instances to meet the target capacity when preemptible instances are reclaimed, and replaces unhealthy instances in a timely manner.

**Related topics**  


[CreateAutoProvisioningGroup](/intl.en-US/API Reference/Auto provisioning group/CreateAutoProvisioningGroup.md)

