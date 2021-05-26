---
keyword: [Alibaba Cloud, ECS, instance type upgrade, subscription, memory upgrade, CPU upgrade]
---

# Upgrade the instance types of subscription instances

This topic describes how to upgrade the instance type of a subscription instance for more vCPUs and higher memory size. The new instance type takes effect immediately after you restart the instance.

Before you upgrade the instance type, make sure that the instance family to which the instance belongs supports instance type changes. For more information, see [Instance families that support instance type changes](/intl.en-US/Instance/Change configurations/Instance families that support instance type changes.md).

When you upgrade the instance type of a subscription instance, you are charged for the price difference between the instance types for the remainder of the current billing cycle.

When you upgrade the instance type, take note of the following limits:

-   You must specify both the vCPU and memory specifications of the instance type to which the instance is to be upgraded. You cannot upgrade only the vCPU or memory.
-   You must set the restart time for the instance whose instance type is to be upgraded. The new instance type takes effect only after the instance is restarted.
-   You can upgrade the instance type of an instance multiple times, but you must wait at least five minutes between two consecutive operations.
-   If you have renewed an instance and downgraded its instance type within the current billing cycle, you cannot upgrade the instance type of this instance until the next billing cycle.

In addition to upgrading the instance type, you can also use the configuration upgrade feature to perform the following operations:

-   Upgrade public bandwidths.
-   Change the billing method for network usage from pay-by-traffic to pay-by-bandwidth.
-   Change the billing method of disks attached to instances from pay-as-you-go to subscription.

## Upgrade the instance type of a single instance

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the subscription instance whose instance type you want to upgrade and click **Upgrade/Downgrade** in the **Actions** column.

5.  In the **Upgrade/Downgrade Wizard** dialog box, select **Upgrade**, and click **Continue**.

6.  On the **Upgrade** page, complete the instance type settings.

    1.  Select the instance type to which the instance is to be upgraded.

        **Note:** You can select only an instance type of higher specifications. You can check whether the instance can have its instance type upgraded and the instance types that you can use for the upgrade.

    2.  Set the restart time of the instance.

        **Note:** If you have scheduled the restart time of the instance, you can choose **Events** \> **Pending Events** \> **Configuration Change and Reboot** in the ECS console to view or modify the scheduled time.

7.  Read the notice. If you do not have any questions, select *ECS Service Terms*.

8.  Verify the price, click **Create Order**, and then complete the payment.

    The new instance type is displayed for the corresponding instance in the ECS console after you complete the payment. However, it does not take effect until you restart the instance.


## Upgrade the instance types of multiple instances

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Select subscription instances whose instance types you want to upgrade. In the lower part of the page, choose **More** \> **Configuration Change** \> **Upgrade/Downgrade**.

5.  In the **Upgrade/Downgrade Wizard** dialog box, select **Upgrade Instance \(Only for Same Instance Type\)** and then click **Continue**.

6.  On the **Upgrade Instance Type** page, complete the instance type settings.

    If an instance does not have the same instance type as other instances or if it is located in a different zone from the other instances, this instance is filtered out. You can continue to perform operations on only the qualified instances, as shown in the following figure.

    ![Upgrade the instance types of multiple instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6775240061/p134726.png)

    1.  Select the instance type to which the instance is to be upgraded.

        **Note:** You can select only an instance type of higher specifications. You can check whether the instance can have its instance type upgraded and the instance types that you can use for the upgrade.

    2.  Set the restart time of the instance.

        **Note:** If you have scheduled the restart time of the instance, you can choose **Events** \> **Pending Events** \> **Configuration Change and Reboot** in the ECS console to view or modify the scheduled time.

7.  Read the notice. If you do not have any questions, select *ECS Service Terms*.

8.  Verify the price, click **Upgrade**, and then complete the payment.

    The new instance type is displayed for the corresponding instances in the ECS console after you complete the payment. However, it does not take effect until you restart the instances.


**Related topics**  


[RebootInstance](/intl.en-US/API Reference/Instances/RebootInstance.md)

[DescribeResourcesModification](/intl.en-US/API Reference/Regions/DescribeResourcesModification.md)

[ModifyPrepayInstanceSpec](/intl.en-US/API Reference/Instances/ModifyPrepayInstanceSpec.md)

