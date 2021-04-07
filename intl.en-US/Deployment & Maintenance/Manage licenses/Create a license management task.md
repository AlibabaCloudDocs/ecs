# Create a license management task

License Manager automates the discovery and statistics collection of cloud resources associated with licenses. This can help you monitor and manage your license usage in real time, mitigate non-compliance risks, and reduce management costs. This topic describes how to create license management tasks and the limits on license management tasks.

An increasing number of enterprise users migrate their business to the cloud, and the demand for using and managing licenses also increases. Previously, you had to manually track resource creation and license usage. Problems such as lack of monitoring of the number of licenses used, frequent creation and release of instances, and failure to update usage records in real time were common. To solve these problems, Alibaba Cloud provides License Manager to help you monitor license usage in real time.

License Manager provides simplified management and usage monitoring for your software such as Windows Server and SQL Server. This mitigates non-compliance risks that arise from overuse of licenses and reduces your management costs.

## Limits

You can create up to 25 license management tasks within a single region.

## Procedure

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **License Manager**.

3.  On the **License Manager** page, click **Create License Management Task**.

4.  When you use License Manager for the first time, you must follow the instructions to complete authorization.

    If the Cloud resource access authorization successful message appears and you are directed to the ECS console, you are authorized to use License Manager.

    **Note:** For more information about RAM roles, see [RAM role overview](/intl.en-US/RAM Role Management/RAM role overview.md).

5.  In the Create License Management Task dialog box, configure the parameters for the license management task.

    |Parameter|Description|
    |---------|-----------|
    |**License Management Task Name**|The name of the license management task. Example: Windows server1234567. The name must be 2 to 128 characters in length and can contain letters, digits, `periods (.),underscores (_), hyphens (-), and colons (:)`. It cannot start with a digit, a special character, http://, or https://.|
    |**Description**|The description of the license management task. The description must be 2 to 256 characters in length.|
    |**License Type**|The type of the managed license.    -   **Instance**: The license is associated with instances. You must set **License Limit of Instance** to specify the number of instances that can be associated with the license as the counting model used for the licenses. The value must be a positive integer. Valid values: 1 to 100000.
    -   **vCPU**: The license is associated with vCPUs. You must set **License Limit of vCPU** to specify the number of vCPUs that can be associated with the license as the counting model used for the licenses. The value must be a positive integer. Valid values: 1 to 100000. |
    |**Automated Discovery Rule**|The product and product version that correspond to the license. This can help you discover and manage licenses in a more precise manner.|

6.  After you configure the parameters, click **Create**.

    After the license management task is created, **Activated** is displayed in the Status column.


After the license management task is created, the system automatically discovers and collects statistics on cloud resources associated with the license management task based on the information that you configured. You can view and manage the resources and your license management tasks. For more information, see [View the resources associated with a license](/intl.en-US/Deployment & Maintenance/Manage licenses/View the resources associated with a license.md) and [Manage license management tasks](/intl.en-US/Deployment & Maintenance/Manage licenses/Manage license management tasks.md).

