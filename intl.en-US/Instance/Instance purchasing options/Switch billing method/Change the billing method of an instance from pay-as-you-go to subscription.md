---
keyword: [subscription, pay-as-you-go, change the billing method, ECS billing]
---

# Change the billing method of an instance from pay-as-you-go to subscription

This topic describes how to change the billing method of an instance from pay-as-you-go to subscription in the ECS console. After you create a pay-as-you-go instance, you can change its billing method to subscription to have resource reserved at a discounted rate.

The ECS instance for which you want to change the billing method meets the following requirements:

-   The instance type of the instance is not retired. For more information, see [Retired instance types](/intl.en-US/Instance/Retired instance types.md).
-   The instance is not a preemptible instance.
-   No unpaid orders related to the instance exist.

    If unpaid orders related to the instance exist, you must pay for the orders or cancel the orders before you change the billing method of the instance.

-   Automatic release time is not configured for the instance.

    If automatic release time is set for the instance, you must disable the automatic release configuration before you change the billing method. For more information, see [Disable automatic release](/intl.en-US/Instance/Manage instances/Release an instance.md).

-   The instance is in the **Running** or **Stopped** state.

    Example: An order to change the billing method was placed while the ECS instance is in the Running or Stopped state. However, the instance status changes before the payment was attempted. The order fails and the billing method does not change. You can go to the Billing Management console and pay for the order when the instance is in the Running or Stopped state again.


1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Choose one of the following methods to change the billing method of an instance from pay-as-you-go to subscription:

    -   Change the billing method of a single instance: Find the instance and choose **More** \> **Configuration Change** \> **Switch to Subscription** in the **Actions** column.
    -   Change the billing method of multiple instances: Select the instances and click **Switch to Subscription** in the lower part of the page.

        **Note:** You can change the billing method of up to 20 pay-as-you-go instances at a time.

5.  Click **Batch Change**. In the Switch to Subscription dialog box, complete the billing change settings.

    1.  Select the duration of the subscription.

        Instances whose billing methods are changed at the same time must have the same subscription duration.

    2.  Select the Switch to Subscription option for data disks if you want to change the billing method of the disks attached to the instances.

6.  Click **Create Order** and then complete the payment.


