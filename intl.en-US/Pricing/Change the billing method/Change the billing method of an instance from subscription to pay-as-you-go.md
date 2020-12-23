---
keyword: [subscription, pay-as-you-go, change the billing method, refund quota, ECS billing]
---

# Change the billing method of an instance from subscription to pay-as-you-go

This topic describes how to change the billing method of an instance from subscription to pay-as-you-go. After you create a subscription instance, you can change its billing method to pay-as-you-go if you want to pay for only the actual usage of your resources. After the change, make sure that you have sufficient funds in your account. Otherwise, overdue payments will affect the running of your services.

-   The instance for which you want to change the billing method is in the **Running** or **Stopped** state.
-   The availability of this feature is dynamically determined based on your ECS usage.

After you change the billing method of an ECS instance from subscription to pay-as-you-go,

-   The billing methods of the ECS instance, system disk, and subscription data disks on the instance are changed to pay-as-you-go. The billing method for network usage remains unchanged.
-   The subscription duration that was offered for reasons such as the ICP filing, system failure, or migration from on-premises data centers is automatically invalidated.

**Note:** If the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled and the instance is in the Stopped state before the change, the instance does not enter the No Fees for Stopped Instances \(VPC-Connected\) state after its billing method is changed to pay-as-you-go. You must manually restart and then stop the instance for it to enter the No Fees for Stopped Instances \(VPC-Connected\) state.

The following refund rules apply after you change the billing method from subscription to pay-as-you-go:

-   A refund generated from the billing method change will consume the refund quota. If your account has reached the refund quota, you cannot apply for another refund until the refund record is cleared on the first day of next month. For more information about the refund quota, see [Limits](/intl.en-US/Product Introduction/Limits.md).

    The refund amount resulting from the billing method change can be calculated based on the number of vCPUs and the remaining hours in the current billing cycle. Example: 1 refund unit = `1 vCPU × 1 hour`.

    For example, you have purchased a subscription instance equipped with four vCPUs for six months. Four months later, you change the billing method to pay-as-you-go. In this case, the refund amount for this instance is calculated based on the following formula: `4 (vCPUs) × 60 (remaining days) × 24 (hours/day) = 5760 (refund)`.

-   If the instance involves renewal or upgrade orders that have not taken effect, full refunds of the orders are made. If the orders have already taken effect, only partial refunds of the orders are made.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Choose one of the following methods to change the billing method of an instance from subscription to pay-as-you-go:

    -   Change the billing method of a single instance: Find the instance, and then choose **More** \> **Configuration Change** \> **Switch to Pay-As-You-Go** in the **Actions** column.
    -   Change the billing method of multiple instances: select the instances and choose **More** \> **Configuration Change** \> **Switch to Pay-As-You-Go** in the lower part of the page.
5.  Read the notes. Read and select *ECS Service Terms* and then click **Switch**.


After the billing method is changed, you can go to the ECS console to view the billing method of the instance:

-   On the **Instances** page, the billing method of the instance has been changed to **Pay-As-You-Go** in the **Billing Method** column.
-   Click the instance ID to go to the **Instance Details** page. Click the **Cloud Disk** tab. The billing method of the system disk and data disks \(if any\) is changed to **Pay-As-You-Go** in the **Billing Method** column.

You can set the automatic release time for the instance to be automatically released when you no longer need the instance to save costs. For more information, see [Release an instance](/intl.en-US/Instance/Manage instances/Release an instance.md).

**Related topics**  


[ModifyInstanceChargeType](/intl.en-US/API Reference/Instances/ModifyInstanceChargeType.md)

