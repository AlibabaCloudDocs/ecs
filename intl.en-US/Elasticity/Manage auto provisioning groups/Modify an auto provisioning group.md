# Modify an auto provisioning group

This topic describes how to modify the configurations of an auto provisioning group. You can modify the name, target capacity, and some capacity-related settings of an auto provisioning group.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Deployment & Elasticity** \> **Auto Provisioning**.

3.  In the top navigation bar, select a region.

4.  Find the auto provisioning group that you want to modify and click **Modify** in the **Actions** column.

    The following table lists the parameters that can be modified.

    |Section|Description|
    |-------|-----------|
    |**Basic Information**|The auto provisioning group name can be modified.|
    |**Group Capacity**|The following capacities can be modified:    -   **Target Capacity**: the capacity that the auto provisioning group is scheduled to provision. You can specify this capacity in terms of **Instances** or **vCPUs**. After you select **Use Pay-as-you-go Instances to Provide Computing Power**, you can specify the computing power provided by the pay-as-you-go instances.
    -   **Target Capacity of Pay-As-You-Go Instances**: the target capacity of pay-as-you-go instances that the auto provisioning group is scheduled to provision. You can specify this capacity in terms of instances or vCPUs. You can use pay-as-you-go instances to ensure that the lowest computing power requirement can be met because preemptible instances may be reclaimed.
**Note:** When you create an auto provisioning group by calling the [CreateAutoProvisioningGroup](/intl.en-US/API Reference/Auto provisioning group/CreateAutoProvisioningGroup.md) operation, you can specify the target capacity in terms of instances, vCPUs, or the amount of memory. |
    |**Capacity-related Settings**|The following capacity-related configurations can be modified:    -   **Default Billing Method of Supplemental Instances**: **Preemptible Instances** and **Pay-As-You-Go Instances** are supported. When the sum of the Target Capacity of Pay-As-You-Go Instances and Target Capacity of Preemptible Instances values is less than the Target Capacity value, the auto provisioning group automatically creates instances that use the specified billing method to fulfill the target capacity.
    -   **Global Maximum Price for Preemptible Instances**: You can modify the fixed maximum hourly price. If the specified maximum hourly price is less than the market price, preemptible instances fail to be created and high instance costs are prevented. |

    **Note:** Regardless of the auto provisioning group type, a scheduling task is triggered after you modify the capacity or capacity-related settings.

5.  Click **OK**.


**Related topics**  


[ModifyAutoProvisioningGroup](/intl.en-US/API Reference/Auto provisioning group/ModifyAutoProvisioningGroup.md)

