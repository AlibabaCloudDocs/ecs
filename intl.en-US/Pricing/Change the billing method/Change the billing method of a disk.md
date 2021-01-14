---
keyword: [change billing methods, disk billing, change from subscription to pay-as-you-go, ECS, change pay-as-you-go to subscription]
---

# Change the billing method of a disk

This topic describes how to change the billing method of a disk. The billing methods of data disks attached to subscription instances can be changed independently. The billing methods of data disks attached to pay-as-you-go instances and system disks can be changed only together with their instances.

The disk is attached to an instance, and the instance is in the **Running** or **Stopped** state.

Take note of the following limits when you change the billing method of a disk:

-   Whether you can change the billing method of your disk depends on your ECS usage.
-   You must wait at least five minutes between two consecutive billing method changes.

## Change the billing method from subscription to pay-as-you-go

This section describes how to change the billing method of a data disk attached to a subscription instance from subscription to pay-as-you-go. For information about how to change the billing methods of system disks, see [Change the billing method of an instance from subscription to pay-as-you-go](/intl.en-US/Pricing/Change the billing method/Change the billing method of an instance from subscription to pay-as-you-go.md).

**Note:** You may receive a refund when you use the configuration downgrade feature to change the billing method of a data disk from subscription to pay-as-you-go. The refund amount is the difference between the price of the new configurations and the remaining price of the original configurations before the configuration downgrade.A maximum of three refunds can be made for each instance, including refunds incurred when you downgrade the instance type, downgrade the public bandwidth, or change the billing methods of disks from subscription to pay-as-you-go.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the top navigation bar, select a region.

3.  Select one of the following methods to change the billing methods of your disks:

    -   If you want to change the billing methods of multiple data disks that are attached to the same instance, we recommend that you perform the operations on the Instances page.
        1.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
        2.  Find the instance and click **Upgrade/Downgrade** in the **Actions** column.
        3.  In the Upgrade/Downgrade Wizard dialog box, choose **Downgrade** \> **Disk Billing Method to Pay-as-you-go**, and click **Continue**.
        4.  Select the subscription data disks whose billing method you want to change.
    -   If you want to change the billing method of a specific data disk, we recommend that you perform the operations on the Disks page.
        1.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.
        2.  Find the data disk, and choose **More** \> **Switch to Pay-As-You-Go** in the **Actions** column.
4.  Verify the refund amount, read and select *ECS Service Terms*, and then click **Downgrade Now**.

    By default, after the billing method of a disk is changed to pay-as-you-go, the disk is not released together with the instance to which the disk is attached. You can configure whether the disk is released together with the instance to which the disk is attached in the ECS console. For more information, see [Release a disk](/intl.en-US/Block Storage/Cloud disks/Release a disk.md).


## Change the billing method from pay-as-you-go to subscription

This section describes how to change the billing method of a data disk attached to a subscription instance from pay-as-you-go to subscription. For information about how to change the billing methods of pay-as-you-go data disks attached to pay-as-you-go instances and system disks, see [Change the billing method of an instance from pay-as-you-go to subscription](/intl.en-US/Pricing/Change the billing method/Change the billing method of an instance from pay-as-you-go to subscription.md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the top navigation bar, select a region.

3.  Select one of the following methods to change the billing methods of your disks:

    -   If you want to change the billing methods of multiple data disks that are attached to the same instance, we recommend that you perform the operations on the Instances page.
        1.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
        2.  Find the instance and click **Upgrade/Downgrade** in the **Actions** column.
        3.  In the Upgrade/Downgrade Wizard dialog box, select **Upgrade** and then click **Continue**.
        4.  Select the pay-as-you-go data disks whose billing method you want to change.
    -   If you want to change the billing method of a specific data disk, we recommend that you perform the operations on the Disks page.
        1.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.
        2.  Find the data disk, and choose **More** \> **Switch to Subscription** in the **Actions** column.
4.  Read the notes, read and select *ECS Service Terms*, and then click **Create Order**.

5.  Complete the payment and confirm that the billing method of the disk is changed to subscription.


**Related topics**  


[ModifyDiskChargeType](/intl.en-US/API Reference/Disk/ModifyDiskChargeType.md)

