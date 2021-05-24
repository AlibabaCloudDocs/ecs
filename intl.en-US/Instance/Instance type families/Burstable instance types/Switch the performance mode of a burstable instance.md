# Switch the performance mode of a burstable instance

Burstable instances support the standard and unlimited modes to suit the requirements of different business scenarios. This topic describes how to query and switch the performance mode of a burstable instance.

The performance of a burstable instance in standard mode is limited by the availability of its CPU credits. After its initial credits and CPU credit balance are exhausted, the instance is unable to burst beyond its performance baseline. The performance of a burstable instance in unlimited mode is not limited by the availability of CPU credits. You can overdraw or pay for additional CPU credits to obtain performance boosts at any time.

**Note:** In this case, you may be charged for the consumption of these CPU credits. For more information, see [Impact of performance modes on billing](/intl.en-US/Instance/Instance type families/Burstable instance types/Billing.md).

In the following scenarios, the system selects or switches the performance mode for a burstable instance:

-   By default, the standard mode is enabled for newly created burstable instances.
-   If a burstable instance is in the **Stopped** state and the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled, the instance runs in standard mode by default after it is started.
-   If a burstable instance is in the **Stopped** state and the No Fees for Stopped Instances \(VPC-Connected\) feature is disabled, the performance mode used before the instance is stopped continues to take effect after the instance is started.
-   If you have overdue payments within your account, the unlimited mode is automatically disabled for burstable instances and is not re-enabled until you settle the payments.

## Query the performance mode of a burstable instance

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  If the **Unlimited Mode** column is not displayed on the **Instances** page, configure the column to be displayed.

    1.  Click the ![Column Filters](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6495558161/p96779.png) icon in the upper-right corner.

        ![Column Filters icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6495558161/p96781.png)

    2.  In the Column Filters dialog box, select **Unlimited Mode** and click **OK**.

4.  In the **Unlimited Mode** column, view the mode of the burstable instance.

    -   **Disabled**: indicates that the instance runs in standard mode.
    -   **Enabled**: indicates that the instance runs in unlimited mode.

## Enable the unlimited mode

If a burstable instance is running in standard mode, you can enable the unlimited mode for the instance.

**Note:** Make sure that the burstable instance is in the **Running** state. Otherwise, you cannot switch the performance mode for the instance.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  Find the burstable instance and use one of the following methods to enable the unlimited mode for the instance:

    -   To enable the unlimited mode for a single burstable instance, choose **More** \> **Instance Settings** \> **Enable Unlimited Mode** in the **Actions** column corresponding to the instance.
    -   To enable the unlimited mode for one or more burstable instances, select the instances and choose **More** \> **Instance Settings** \> **Enable Unlimited Mode** in the lower-left corner of the Instances page.
4.  In the **Enable Unlimited Mode** message, click **OK**.


## Disable the unlimited mode

If a burstable instance is running in unlimited mode, you can disable the unlimited mode for the instance.

**Note:** Make sure that the burstable instance is in the **Running** state. Otherwise, you cannot switch the performance mode for the instance.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  Find the burstable instance and use one of the following methods to disable the unlimited mode for the instance:

    -   To disable the unlimited mode for a single burstable instance, choose **More** \> **Instance Settings** \> **Disable Unlimited Mode** in the **Actions** column corresponding to the instance.
    -   To disable the unlimited mode for one or more burstable instances, select the instances and choose **More** \> **Instance Settings** \> **Disable Unlimited Mode** in the lower-left corner of the Instances page.
4.  In the **Disable Unlimited Mode** message, click **OK**.


**Related topics**  


[ModifyInstanceAttribute](/intl.en-US/API Reference/Instances/ModifyInstanceAttribute.md)

