# View an auto provisioning group

This topic describes how to view the information about an auto provisioning group, including its instance information and scheduling task execution.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Deployment & Elasticity** \> **Auto Provisioning**.

3.  In the top navigation bar, select a region.

4.  Click the ID of an auto provisioning group.

    The following table describes details of the auto provisioning group:

    |Parameter|Description|
    |---------|-----------|
    |**Group Configurations**|Includes the basic information and capacity-related settings of the auto provisioning group. For more information, see [Group configurations](/intl.en-US/Elasticity/Manage auto provisioning groups/Create an auto provisioning group.md).|
    |**Template Configurations**|Describes the template configurations that determine the alternative instance types available to the auto provisioning group. For more information, see [Template configurations](/intl.en-US/Elasticity/Manage auto provisioning groups/Create an auto provisioning group.md).|
    |**Instances**|Lists information about instances within the auto provisioning group.|
    |**Group History**|Lists the records of scheduling tasks in the auto provisioning group. You can view the results of instance creation tasks in the **Task Details** column. If most of your scheduling tasks are in the Failed state, you must check your configurations to ensure there is no conflict with actual resource or price requirements. For example, the configured alternative instance types may be limited or the maximum price may be too low.|


