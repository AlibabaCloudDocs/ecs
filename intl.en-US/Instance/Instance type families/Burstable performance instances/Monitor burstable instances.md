---
keyword: [t5, t6, retran, credit consumption, credit pushing]
---

# Monitor burstable instances

This topic describes how to query the CPU utilization and credits of a burstable instance in the ECS console, and how to set CPU credit alert rules in the Cloud Monitor console.

To set the contacts who receive notifications, you must create a contact group in advance. For more information, see [Create an alert contact or alert group](/intl.en-US/Alarm service/Alert contacts/Create an alert contact or alert group.md).

Changes to the CPU credits of a burstable instance directly affect the CPU utilization and load performance of the instance. You can set monitoring alert rules for one or more burstable instances in the Cloud Monitor console. The following items can be monitored: consumed CPU credits, banked CPU credits, overdrawn CPU credits, and advance CPU credits. The following table describes the monitoring metrics of CPU credits for burstable instances.

|Monitoring metric|Descripition|
|-----------------|------------|
|Burstable Instance-CPU Credit Consumption|Displays changes in consumed CPU credits. Consumption trends are consistent with CPU utilization. For more information, see [CPU credits](/intl.en-US/Instance/Instance type families/Burstable performance instances/Overview.md).|
|Burstable Instance-CPU Credit Balance|Displays changes in banked CPU credits. Banked CPU credits are used to maintain CPU utilization. For more information, see [CPU credits](/intl.en-US/Instance/Instance type families/Burstable performance instances/Overview.md).|
|Burstable Instance-Overdrawn CPU Credits|Displays changes in overdrawn CPU credits. Overdrawn CPU credits can be used only when the unlimited mode is enabled. For more information, see [Performance mode](/intl.en-US/Instance/Instance type families/Burstable performance instances/Overview.md).|
|Burstable Instance-Advance CPU Credits|Displays changes in advance CPU credits. Advance CPU credits can be used only when the unlimited mode is enabled. For more information, see [Performance mode](/intl.en-US/Instance/Instance type families/Burstable performance instances/Overview.md).|

## Query CPU credit usage information

You can perform the following steps to query the real-time credit trend of a burstable instance in the ECS console.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the burstable instance and click its ID. The **Instance Details** tab appears.

5.  Click the **Monitoring** tab and view the CPU credit usage and CPU utilization information of the instance.


## Create CPU credit alert rules

You can perform the following steps to create alert rules for **Total Credit** and **Notpaid Surplus Credit** in the Cloud Monitor console. Two modes are available: standard and unlimited.

-   In standard mode, if a burstable instance does not have any available CPU credits, the CPU utilization cannot exceed the baseline performance. When the **Total Credit** item is monitored, you can receive notifications when the instance performance is limited to decide whether to enable the unlimited mode.
-   In unlimited mode, if a burstable instance has consumed all of its advance CPU credits, overdrawn CPU credits are consumed and billed on an hourly basis. This ensures that the CPU utilization exceeds the baseline performance. When the **Notpaid Surplus Credit** item is monitored, you can receive notifications when overdrawn CPU credits are billed to determine whether to disable the unlimited mode.

1.  Log on to the [CloudMonitor console](https://cloudmonitor.console.aliyun.com).

2.  In the left-side navigation pane, choose **Alerts** \> **Alert Rules**.

3.  On the **Alert Rules** page, click **Create Alert Rule**.

4.  On the Create Alert Rule page, configure the following parameters:

    1.  Configure parameters in the **Related Resource** section.

        -   **Product**: Select **ECS** from the drop-down list.
        -   **Resource Range**: Select **Instances** from the drop-down list.
        -   **Instances**: Select one or more burstable instances.
    2.  Configure parameters in the **Set Alert Rules** section.

        -   **Alert Rule**: Customize an alert rule name.
        -   **Rule Description**: Set alert rules and judgment standards.
            -   Monitoring of **Total Credit**: Select **Total Credit** to monitor banked CPU credits. The values of 1Minute cycle, Continue for 1 periods, Average, <, and 1 are used in this example. If the average value of **Total Credit** is less than 1 and the status lasts for at least 1 minute, an alert is triggered.

                **Note:** In standard mode, if the banked CPU credits are less than 1, the CPU utilization of the burstable instance cannot exceed the baseline performance. In unlimited mode, if the CPU utilization exceeds the baseline performance, the burstable instance will consume advance CPU credits. If all advance CPU credits are consumed, the burstable instance will consume overdrawn CPU credits. You can also configure the average value for multiple consecutive periods as the alert triggering condition based on your actual requirements on CPU performance.

                ![Total Credit](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4790359951/p58012.png)

            -   Monitoring of **Notpaid Surplus Credit**: Select **Notpaid Surplus Credit** to monitor overdrawn CPU credits. The values of 1Minute cycle, Continue for 1 periods, Average, \>, and 0 are used in this example. If the average value of **Notpaid Surplus Credit** is greater than 0 and the status lasts for at least 1 minute, an alert is triggered.

                **Note:** If overdrawn CPU credits are greater than 0, overdrawn CPU credits are being used and billed. You can also configure the average value for multiple consecutive periods as the alert triggering condition based on your actual requirements on billing of overdrawn CPU credits.

                ![Notpaid Surplus Credit](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4790359951/p58013.png)

            -   Monitoring of **Burst Credit**: Select **Burst Credit** to monitor consumed CPU credits.
            -   Monitoring of **AdvanceCredit**: Select **AdvanceCredit** to monitor advance CPU credits.
        -   **Mute for**: Select the interval at which notifications are pushed. The value of **10 min** is used in this example.
        -   **Effective Period**: Select the time range during which you can receive notifications.
    3.  Set parameters in the **Notification Method** section.

        -   **Notification Contact**: Select a contact group to receive notifications.
        -   **Notification Methods**: Select **Email + DingTalk \(Info\)** or other methods.
5.  Click **Confirm**.


**Related topics**  


[Create a threshold-triggered alert rule](/intl.en-US/Alarm service/Alarm rules/Create a threshold-triggered alert rule.md)

[Manage a monitoring chart in a custom dashboard](/intl.en-US/Dashboard/Use dashboards/Manage a monitoring chart in a custom dashboard.md)

[Switch the performance mode of a burstable instance](/intl.en-US/Instance/Instance type families/Burstable performance instances/Switch the performance mode of a burstable instance.md)

