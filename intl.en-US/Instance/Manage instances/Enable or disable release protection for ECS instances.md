# Enable or disable release protection for ECS instances

You can enable release protection for pay-as-you-go instances to prevent potential irreversible consequences arising from accidental manual instance release. This topic describes how to enable and disable release protection for ECS instances, how to check whether release protection is enabled, and how release protection is implemented.

The instance is a pay-as-you-go instance.

The release protection feature cannot prevent the automatic release of instances in normal scenarios such as the following ones:

-   A payment in your account is overdue for more than 15 days.
-   The automatic release time that you set for the instance has been reached.
-   The instance does not comply with the applicable security compliance policies.
-   The instance was automatically created by Auto Scaling and is removed by subsequent scale-in events.

The following examples show how release protection is implemented:

-   When you attempt to manually release instances in the ECS console, instances with release protection enabled are automatically skipped.

    ![Release protection alert](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5101359951/p35403.png)

-   When you attempt to manually release instances in the ECS console, the selected instances cannot be released if they all have release protection enabled.

    ![Release protection enabled for all instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5101359951/p132507.png)

-   The `InvalidOperation.DeletionProtection` error code is returned if you attempt to call the DeleteInstance operation to release an instance with release protection enabled.

## Enable release protection when you create an instance

This section describes how to configure release protection settings when you create an instance. For more information about how to create an instance, see [Create an instance by using the provided wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  On the **Instances** page, click **Create Instance**.

5.  In the **Basic Configurations** step, set **Billing Method** to **Pay-As-You-Go** and complete the remaining configurations. Click **Next: Networking**.

6.  In the **Networking** step, complete all configurations. Click **Next: System Configurations**.

7.  In the **System Configurations** step, select **Prevent users from releasing the instance inadvertently by using the console or API** and complete the remaining configurations. Click **Next: Grouping**.

    ![Enable release protection when you create an instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5101359951/p35416.png)

8.  Complete the remaining configurations until the instance is created.


When you call the RunInstances or CreateInstance operation to create an instance, you can enable or disable release protection for the instance by setting the DeletionProtection parameter.

## Change the release protection settings

You can also enable or disable release protection for an instance by modifying the attributes of the instance.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  On the **Instances** page, use one of the following methods to change the release protection settings of instances:

    -   Change the release protection settings of a single instance: Find the instance for which you want to change the release protection setting, and choose **More** \> **Instance Settings** \> **Change Release Protection Setting** in the **Actions** column.
    -   Change the release protection settings of one or more instances: Select multiple instances and choose **More** \> **Instance Settings** \> **Change Release Protection Setting** in the lower part of the Instances page.
5.  In the Change Release Protection Setting dialog box, turn on or off **Release Protection**.

6.  Click **OK**.


When you call the ModifyInstanceAttribute operation to modify the attributes of an instance, you can enable or disable release protection for the instance by setting the DeletionProtection parameter.

## Check whether release protection is enabled

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  On the **Instances** page, use one of the following methods to view details of an instance:

    -   In the **Instance ID/Name** column, click the ID of the instance.
    -   Find the instance and click **Manage** in the **Actions** column.
5.  On the **Instance Details** tab, check whether release protection is enabled in the **Release Protection** item of the **Other Information** section.

    ![Check whether release protection is enabled](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5101359951/p35419.png)


**References**  


[DeleteInstance](/intl.en-US/API Reference/Instances/DeleteInstance.md)

[RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md)

[CreateInstance](/intl.en-US/API Reference/Instances/CreateInstance.md)

[ModifyInstanceAttribute](/intl.en-US/API Reference/Instances/ModifyInstanceAttribute.md)

