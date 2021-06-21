# Subscribe to an event notification

You can configure alert rules for system events by using Cloud Monitor. Notifications will be sent to you when the specified events occur.

An application group is created and resources are added to the application group. If you need to apply alert rules to instances by application group, you must create an application group first. For more information about how to create an application group and add resources to the application group, see [t6144.md\#](/intl.en-US/Application groups/Create an application group.md) and [Add resources to an application group](/intl.en-US/Application groups/Add resources to an application group.md).

Cloud Monitor can notify you of events immediately after the events occur in Alibaba Cloud services. You can automate the process of handing these events. Cloud Monitor supports the following notification methods for events:

-   Sends alert notifications to you by using emails or DingTalk chatbots.
-   Pushes events to Message Service \(MNS\), Function Compute, Log Service, or the specified callback URL. Then, you can automate the handling process based on your scenario.

## Create an event-triggered alert rule

1.  Log on to the [Cloud Monitor console](https://cms-intl.console.aliyun.com).

2.  In the left-side navigation pane, choose **Alerts** \> **Alert Rules**.

3.  On the Alert Rules page, click the **Event Alert** tab.

4.  On the Event Alert tab, click **Create Event Alert**.

5.  In the Create / Modify Event Alert panel, set the alert rule and alert notification method.

    -   System events

        If you set the **Event Type** parameter to **System Event**, you must set the Product Type, Event Type, Event Level, Event Name, Resource Range, and Notification Method parameters as required.

        The notification methods for system events include alert notification, MNS queue, Function Compute, Log Service, and callback URL.

    -   Custom events

        If you set the **Event Type** parameter to **Custom Event**, you must set the Application Groups, Event Name, Rule Description, and Notification Method parameters as required.

        The notification methods for custom events include alert notification and callback URL.

6.  Click **OK**.


## Test a system event-triggered alert rule

After you create a system event-triggered alert rule, you can test the alert rule. You can check whether alert notifications can be received or whether events can be pushed to MNS, Function Compute, Log Service, or the specified callback URL as configured.

1.  Log on to the [Cloud Monitor console](https://cms-intl.console.aliyun.com).

2.  In the left-side navigation pane, choose **Alerts** \> **Alert Rules**.

3.  On the Alert Rules page, click the **Event Alert** tab.

4.  On the Event Alert tab, find the system event-triggered alert rule that you want to test and click **test** in the **Actions** column.

5.  In the Create event test panel, select a system event and modify the event content as required.

6.  Click **OK**.

    Cloud Monitor generates the selected system event. Check whether an alert notification is received or the event is pushed to MNS, Function Compute, Log Service, or the specified callback URL as configured.


