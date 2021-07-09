# Manage license management tasks

You can modify the status, instance or vCPU quantity limits, and automated discovery rules of your created license management tasks. If you do not want to manage or monitor your license usage, you can delete your license management tasks. This topic describes how to manage license management tasks.

## Deactivate a license management task

If you temporarily do not want to associate your cloud resources with a license management task, you can deactivate the license management task. Your created license configurations are still retained. You can reactivate the license management task at any time.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **License Manager**.

3.  On the **License Manager** page, find the license management task that you want to deactivate and click **Deactivate** in the Actions column.

4.  In the Deactivate License Configuration message, check the displayed information of the license management task and click **OK**.

    When the license management task enters the **Deactivated** state, the license management task is deactivated.


## Activate a license management task

If you want to associate your cloud resources with a license management task again, you can perform the following operations to activate the license management task:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **License Manager**.

3.  On the **License Manager** page, find the license management task that you want to activate and click **Activate** in the Actions column.

4.  In the Activate message, check the displayed information of the license management task and click **OK**.

    When the license management task enters the **Activated**, the license management task is activated.


## Set an instance or vCPU quantity limit

If you want to change the instance or vCPU quantity limit for a license management task, you can perform the following operations to set the quantity limit:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **License Manager**.

3.  On the **License Manager** page, find the license management task for which you want to change the quantity limit and click **Set License Limit** in the Actions column.

4.  In the Set License Limit dialog box, enter a value in the Instance Quantity Limit Setting or vCPU Quantity Limit Setting field and click **OK**.

    When the new value appears in the Number of Licenses Consumed column, the quantity limit is changed.


## Add an automated discovery rule

If you want to add an automated discovery rule, you can perform the following operations.

**Note:** You cannot modify or remove automated discovery rules. If you want to modify or remove an automated discovery rule, you must delete the associated license management task and then create another one.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **License Manager**.

3.  On the **License Manager** page, click the license ID to go to the Basic Information page.

4.  Click the Automated Discovery Rules tab and then click **Add License Rule**.

5.  In the Add License Rule dialog box, select the automated discovery rule that you want to add.

    **Note:** Automated discovery rules can be configured for a service of multiple versions. If you have an existing rule for a service, you can add rules only for other versions of the service.

6.  Click **OK**.

    The added automated discovery rule is displayed on the Automated Discovery Rules tab.


## Delete a license management task

If you no longer want to associate your cloud resources with a license management task, you can delete the license management task. If you confirm the delete operation, the license management task is permanently deleted. Proceed with caution.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **License Manager**.

3.  On the **License Manager** page, find the license management task that you want to delete and click **Delete** in the Actions column.

4.  In the Delete License message, confirm the information of the license delete and click **OK**.


