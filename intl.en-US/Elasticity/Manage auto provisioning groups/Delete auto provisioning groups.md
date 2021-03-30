# Delete auto provisioning groups

This topic describes how to delete auto provisioning groups. Auto provisioning groups can alleviate the instability caused by preemptible instances being reclaimed and eliminate the need to pay close attention to the status of preemptible instances.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Deployment & Elasticity** \> **Auto Provisioning**.

3.  In the top navigation bar, select a region.

4.  Delete auto provisioning groups by using one of the following methods:

    -   To delete a single provisioning group, find the auto provisioning group and click **Delete** in the **Actions** column.
    -   To delete one or more auto provisioning groups at a time, select the auto provisioning groups and click **Delete Group** in the lower part of the page.
5.  In the **Delete Group** dialog box, specify whether to delete instances in the auto provisioning group.

    -   If you turn on **Delete Instances**, all instances in the auto provisioning group are released after the group is deleted.
    -   If you turn off **Delete Instances**, only the auto provisioning group is deleted. All instances in the auto provisioning group are retained.
6.  Click **OK**.


