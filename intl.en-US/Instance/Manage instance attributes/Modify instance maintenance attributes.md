---
keyword: [event, system event, automation, message notification, ECS]
---

# Modify instance maintenance attributes

By default, Alibaba Cloud automatically restarts an ECS instance if an automatic recovery event occurs for the instance, such as when the instance goes down unexpectedly or when an active O&M plan is performed. You can customize the automatic recovery mode for an instance by modifying its maintenance attributes.

For more information about automatic recovery and the applicable scope and impact of each maintenance attribute, see [Automatic recovery events of instances](/intl.en-US/Deployment & Maintenance/System events/Automatic recovery events of instances.md).

## Procedure

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance and use one of the following methods to modify the instance maintenance attribute.

    -   Method 1: Choose **More** \> **Operations and Troubleshooting** \> **Modify Instance Maintenance Attribute** in the **Actions** column corresponding to the instance.
    -   Method 2: Click the instance ID to go to the Instance Details tab. In the Basic Information section, choose **All Operations** \> **Instance Properties** \> **Modify Instance Maintenance Attribute**.
5.  In the **Modify Instance Maintenance Attribute** dialog box, modify the instance maintenance attribute. Click **OK**.

    -   If only cloud disks are attached to the instance, you can select one of the following options for Maintenance Action:
        -   Automatically Restart
        -   Stop
    -   If local disks are also attached to the instance, you can select one of the following options for Maintenance Action:
        -   Automatically Restart
        -   Stop
        -   Automatically Redeploy
6.  In the **Basic Information** section of the **Instance Details** tab, confirm the settings that you configured for **Maintenance Attribute**.


**Related topics**  


[ModifyInstanceMaintenanceAttributes](/intl.en-US/API Reference/Operations and monitoring/ModifyInstanceMaintenanceAttributes.md)

[DescribeInstanceMaintenanceAttributes](/intl.en-US/API Reference/Operations and monitoring/DescribeInstanceMaintenanceAttributes.md)

