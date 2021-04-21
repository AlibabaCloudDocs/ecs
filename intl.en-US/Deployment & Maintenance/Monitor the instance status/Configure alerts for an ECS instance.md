# Configure alerts for an ECS instance

You can enable initiative alert on the details page of an ECS instance or configure custom alert rules to detect exceptions of an ECS instance in a timely manner.

You can enable the initiative alert and custom alert rule features on the Monitoring tab of the instance details page.

-   After initiative alert is enabled, alert rules related to the CPU utilization, disk usage, memory usage, and network bandwidth usage are created for all ECS instances within your Alibaba Cloud account. For more information, see [Enable initiative alert](#section_u83_pol_cbv).
-   You can configure custom alert rules for an ECS instance. These custom alert rules take effect only for the current ECS instance. For more information, see [Configure custom alert rules](#section_l0p_dd5_whe).

If you want to manage alert rules or require more monitoring and alert features, you can go to the Cloud Monitor console. For more information, see [What is CloudMonitor?](/intl.en-US/Product Introduction/What is CloudMonitor?.md)

## Enable initiative alert

You can enable initiative alert for key metrics of ECS to quickly establish an alert system and obtain the exception information of key metrics in a timely manner. After initiative alert is enabled, the related alert rules apply to all ECS instances within your Alibaba cloud account.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance and click its ID.

5.  On the Instance Details page, click the **Monitoring** tab.

6.  Click **Initiative Alert**.

7.  On the **Configure Initiative Alert** tab, turn on **Initiative Alert**.

    ![Enable initiative alert](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9473098161/p228306.png)

    After initiative alert is enabled, you can view the details of an alert rule. You can also perform the following operations:

    -   Disable an alert rule: If you no longer need an alert rule, you can disable the rule.
    -   Modify an alert rule: If you find that an alert rule is not suitable for your business, you can go to the Cloud Monitor console to modify the rule.

## Configure custom alert rules

In addition to initiative alert, you can also configure custom alert rules for your instance based on your business requirements. The created custom alert rules automatically take effect for the current instance, which allows you to learn about the exceptions of the instance in a timely manner.

1.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

2.  In the top navigation bar, select a region.

3.  Find the instance and click its ID.

4.  On the Instance Details page, click the **Monitoring** tab.

5.  Click **Create Alert Rules**.

6.  On the **Create Custom Alert Rule** tab, create custom alert rules.

    1.  Configure parameters for the alert rule and click **Next**.

        ![Create a custom alert rule](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9473098161/p228702.png)

        |Parameter|Description|
        |---------|-----------|
        |**Alert Rules**|Specifies parameters for the alert rule, including the name and content of the alert rule. This parameter specifies the condition that triggers an alert. For example, if the condition specifies that the average CPU utilization every 5 minutes is greater than or equal to 90% for three consecutive cycles, Cloud Monitor checks whether the condition is met every 5 minutes only three times.

**Note:**

        -   For information about the ECS metrics of alert rules, see [Metrics](/intl.en-US/Host monitoring/Metrics.md).
        -   You can click **Add Alert Rule** to create multiple alert rules. |
        |**Mute For**|Specifies the mute period. If the alert is not cleared within the mute period, a new alert notification is sent when the mute period ends.|
        |**Validity Period**|Specifies the period during which the alert rule is in effect. The system monitors the metrics and generates alerts only when the alert rule is in effect.|

    2.  Configure the parameters in the Configure Notification Methods step and click **Create**.

        |Parameter|Description|
        |---------|-----------|
        |**Alert Contact**|The contacts or contact groups to which an alert notification is sent. For more information, see [Create an alert contact or alert group](/intl.en-US/Alarm service/Alert contacts/Create an alert contact or alert group.md).|
        |**Notification Methods**|The method to receive alert notifications and the supplementary information of alert emails. The value is set to Email and Webhook URL.

You can specify custom remarks that you want to include in the alert notification email. |
        |**Callback URL**|The callback URL that can be accessed over the Internet. Cloud Monitor sends a POST request to push alert messages to the specified callback URL. Only HTTP requests are supported.|

    The created custom alert rule takes effect only for the current instance.

7.  You can click **Manage Alert Rules** on the **Monitoring** tab to go to the Cloud Monitor console to view or modify the custom alert rule.


## References

-   [What is CloudMonitor?](/intl.en-US/Product Introduction/What is CloudMonitor?.md)
-   [Enable the initiative alert feature](/intl.en-US/Alarm service/Enable the initiative alert feature.md)
-   [Manage alert rules](/intl.en-US/Alarm service/Alarm rules/Manage alert rules.md)

