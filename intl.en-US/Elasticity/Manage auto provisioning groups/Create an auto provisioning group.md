# Create an auto provisioning group

This topic describes how to create an auto provisioning group in the ECS console. The auto provisioning group can create an instance cluster based on your configurations.

-   Your account is granted permissions on Auto Provisioning.

    **Note:** When you access the Auto Provisioning page for the first time, follow the instructions to assume the `AliyunECSAutoProvisioningGroupRole` RAM role.

-   A launch template is created. For more information, see [Create a launch template](/intl.en-US/Elasticity/Launch template/Create a launch template.md).

    Auto provisioning groups use specific versions of launch templates as sources of instance configurations. Properties such as instance images, security groups, and logon credentials from the launch templates are used by auto provisioning groups to create instances.


1.  Go to the Auto Provisioning page.

    1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

    2.  In the top navigation bar, select a region.

    3.  In the left-side navigation pane, choose **Deployment & Elasticity** \> **Auto Provisioning**.

2.  Click **Create Provisioning Group**.

3.  In the **Group Name** field, enter the name of the auto provisioning group.

    The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain digits, underscores \(\_\), hyphens \(-\), and periods \(.\).

4.  In the **Target Capacity** section, configure parameters related to the capacity of the auto provisioning group.

    The capacity-related parameters determine the sum of computing power provisioned by the auto provisioning group, and the proportions of computing power provided by preemptible and pay-as-you-go instances. The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Target Capacity**|The target capacity that the auto provisioning group is scheduled to provision. You can specify this capacity in terms of **Instances** or **vCPUs**. After you select **Use Pay-as-you-go Instances to Provide Computing Power**, you can specify the computing power provided by the pay-as-you-go instances.**Note:** By default, only preemptible instances are created. Pay-as-you-go instances are created only after you set the value of Pay-as-you-go Instance Capacity to a number greater than 0. |
    |**Pay-as-you-go Instance Capacity**|The target capacity of pay-as-you-go instances that the auto provisioning group is scheduled to provision. You can specify this capacity in terms of instances or vCPUs. You can use pay-as-you-go instances to ensure that the lowest computing power requirement can be met because preemptible instances may be reclaimed.|

    **Note:** When you create an auto provisioning group by calling the [CreateAutoProvisioningGroup](/intl.en-US/API Reference/Auto provisioning group/CreateAutoProvisioningGroup.md) operation, you can specify the target capacity in terms of instances, vCPUs, or the amount of memory.

    Auto Provisioning uses weights to indicate the capacity of a single instance in an auto provisioning group.

    -   If the target capacity is specified in terms of **Instances**, the weights of all instance types are the same.
    -   If the target capacity is specified in terms of **vCPUs**, the weight of an instance type depends on the number of vCPUs of the instance type. The more vCPUs that an instance type has, the higher the weight of the instance type and the fewer instances of the instance type that are needed to meet the target capacity. The following table describes an example in which different weights are set for three instance types based on the number of vCPUs.

        |Instancetype|vCPU|Weight|
        |------------|----|------|
        |ecs.c6.large|2|2|
        |ecs.c6.xlarge|4|4|
        |ecs.c6.2xlarge|8|8|

        **Note:** When you create an auto provisioning group in the ECS console, you do not need to manually set a weight for each instance type. Auto provisioning automatically assigns weights based on the number of vCPUs of each instance type.

        For example, the target capacity is 24 vCPUs, and the auto provisioning group can deliver instances of one or more of the ecs.c6.large, ecs.c6.xlarge, ecs.c6.2xlarge instance types to meet the target capacity. The required number of instances is determined based on the combination of instance types:

        -   12 ecs.c6.large instances
        -   8 ecs.c6.large instances and 1 ecs.c6.2xlarge instance
        -   4 ecs.c6.large instances, 2 ecs.c6.xlarge instances, and 1 ecs.c6.2xlarge instance
    -   If the target capacity is specified in terms of the amount of memory, the weight of an instance type depends on the amount of memory of the instance type. The larger the amount of memory that an instance type has, the higher the weight of the instance type and the fewer the instances of the instance type that are needed to meet the target capacity. The following table describes an example in which different weights are set for three instance types based on the amount of memory.

        |Instancetype|Memory|Weight|
        |------------|------|------|
        |ecs.c6.large|4 GiB|4|
        |ecs.c6.xlarge|8 GiB|8|
        |ecs.c6.2xlarge|16 GiB|16|

        For example, the target capacity is 48 GiB memory, and the auto provisioning group can deliver instances of one or more of the ecs.c6.large, ecs.c6.xlarge, ecs.c6.2xlarge instance types to meet the target capacity. The required number of instances is determined based on the combination of instance types:

        -   12 ecs.c6.large instances
        -   8 ecs.c6.large instances and 1 ecs.c6.2xlarge instance
        -   4 ecs.c6.large instances, 2 ecs.c6.xlarge instances, and 1 ecs.c6.2xlarge instance
        **Note:** To specify the target capacity of an auto provisioning group in terms of the amount of memory, call the CreateAutoProvisioningGroup operation to create the auto provisioning group and set the weight of each alternative instance type based on the amount of memory.

5.  In the **Configuration Source** and **Instance Configuration** fields, configure instance properties.

    You can use an auto provisioning group to create instances of multiple instance types across multiple zones. If an instance fails to be created due to insufficient resources of a specific instance type or in a specific zone, the auto provisioning group attempts to create instances of another instance type or in another zone. This can improve the success rate of creating instances.

    You can specify vSwitches in multiple zones to create instances across multiple zones, and add instance types to create instances of multiple instance types. The following figure shows an example of parameter configurations. For more examples, see[Configure an auto provisioning group](/intl.en-US/Elasticity/Manage auto provisioning groups/Configure an auto provisioning group.md).

    ![multi-zone-type](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2359695161/p244716.png)

    Two zones and three instance types are used in the preceding example. The following table describes operations involved in the example.

    |No.|Procedure|
    |---|---------|
    |①|Select a launch template and then a specific version of the launch template as the configuration source.**Note:** When you create instances, the vSwitches and instance types specified in the sections tagged with ② and ④ are used. However, other properties such as the image, security groups, and logon credential are obtained from the configuration source. |
    |②|Complete instance configurations. By default, the vSwitch and instance type specified in the configuration source are used. You can select other vSwitches, and select or add other instance types.**Note:** You must specify at least one instance configuration for an auto provisioning group. |
    |③|Add an instance configuration to create instances across multiple zones.|
    |④|Complete the instance configuration. The following parameters are required:    -   **Specify VSwitch**: the vSwitch to which the instances are connected. Make sure that the vSwitch belongs to a different zone from the vSwitch specified in the section tagged with ②.

**Note:** If you specify multiple vSwitches within the same zone, only the first vSwitch takes effect.

    -   **Add Instance Type**: You can select one or more instance types to increase the success rate of creating instances. Two instance types are specified in this example. In the Select Instance Type dialog box, instance types that have the same instance size or vCPU-to-memory ratio as the instance type specified in the selected configuration source are provided. You can also select other instance types. |

    In addition to vSwitches and instance types, you can also set the maximum hourly prices for preemptible instances of each instance type. You can set the maximum hourly prices in the following ways:

    -   Select Automatic Bidding. The real-time market price is used as the maximum hourly price for the bids. This way, preemptible ECS instances do not fail to be created due to low bids. The instance costs are subject to change with the market price.
    -   Choose Set Maximum Price \> Maximum Price, and set a maximum hourly price. If you select this option, preemptible instances cannot be created if your bid is less than the market price. This prevents instance costs from spiraling out of control if the market price increases.
    -   Choose Set Maximum Price \> Pay-as-you-go Price, and set a percentage of the pay-as-you-go price to obtain the maximum hourly price. This costs you less than pay-as-you-go prices. For example, if you set the percentage to 50%, preemptible ECS instances fail to be created when the market price is higher than 50% of the pay-as-you-go price.
    **Note:** We recommend that you learn the market price trends of preemptible instances before you set the maximum hourly prices. This way, you can prevent high costs or failures to meet the target capacity. You can click **Price History** in the **Actions** column to view historical prices.

6.  In the **Provisioning Policy** section, select the policy used to create instances.

    The following table describes the options for this parameter.

    |Option|Description|
    |------|-----------|
    |**Capacity Optimization Policy**|The auto provisioning group selects the most cost-effective instance type based on the prices and reclaim rates to create preemptible ECS instances. **Note:** Preemptible instances may be reclaimed due to factors such as price and inventory. Instance types that have low reclaim rates are preferred. |
    |**Cost Optimization Policy**|The auto provisioning group attempts to create ECS instances based on the unit prices of vCPUs in ascending order.|
    |**Balanced Distribution Policy**|The auto provisioning group evenly distributes ECS instances across the zones that are specified in the instance configurations. This parameter takes effect only when multiple zones are specified.The preemptible instances of each instance type are reclaimed together. Instance resources are shared within the same instance family. For example, if an instance of the ecs.c6.large instance type fails to be created, a possible cause is that instance resources in the c6 instance family are insufficient. Instances of other c6 instance types such as ecs.c6.xlarge may also fail to be created.

**Note:** If you select Balanced Distribution Policy, we recommend that you configure instance types from different instance families to prevent instances being reclaimed at the same time and ensure your instance clusters remain available. |

7.  Configure advanced options.

    The following table describes the parameters in the Advanced section.

    |Parameter|Description|
    |---------|-----------|
    |**Group Type**|    -   **One-time Delivery**: After the auto provisioning group is started, it attempts to create an instance cluster that has the target capacity only once. If the instance cluster fails to be created, the auto provisioning group does not retry to create the instance cluster again.
    -   **Continuous Delivery and Maintain Capacity**: After the auto provisioning group is started, it attempts to create an instance cluster repeatedly until it reaches the target capacity. If the real-time capacity does not match the target capacity, the auto provisioning group scales in or out to meet the target capacity. |
    |**Start Time**|The time when the auto provisioning group is started. The period of time between this point in time and the point in time specified by End Time is the validity period of the auto provisioning group.     -   **Now**: The auto provisioning group is started immediately after it is created.
    -   **Specify Start Time**: Specify a point in time at which to start the auto provisioning group. |
    |**End Time**|The time when the auto provisioning group expires. The period of time between this point in time and the point in time specified by Start Time is the validity period of the auto provisioning group.     -   **Never**: The auto provisioning group never expires unless you delete it.
    -   **Specify End Time**: Specify the point in time at which the auto provisioning group expires. |
    |**Global Maximum Price for Preemptible Instances**|The global maximum hourly price for preemptible instances created in the auto provisioning group. This parameter applies to preemptible instances of all instance types. If the global maximum hourly price is different from the maximum hourly price specified for a single instance type in the instance configurations, the lower one of the two prices takes precedence.    -   **Automatic Bidding**: The real-time market price is used as the maximum hourly price for the bids. This way, preemptible ECS instances do not fail to be created due to low bids. The instance costs are subject to change with the market price.
    -   **Set Maximum Price**: a fixed maximum hourly price. If you select this option, preemptible instances cannot be created if your bid is less than the market price. This prevents instance costs from spiraling out of control if the market price increases. |

8.  Click **Create Provisioning Group**.


After the auto provisioning group is created, it is started and attempts to create the instance cluster at the specified time. If **Continuous Delivery and Maintain Capacity** is selected for Group Type, the auto provisioning group continuously maintains the instance cluster. The auto provisioning group attempts to create new instances to meet the target capacity when preemptible instances are reclaimed, and replaces unhealthy instances in a timely manner.

**Related topics**  


[CreateAutoProvisioningGroup](/intl.en-US/API Reference/Auto provisioning group/CreateAutoProvisioningGroup.md)

