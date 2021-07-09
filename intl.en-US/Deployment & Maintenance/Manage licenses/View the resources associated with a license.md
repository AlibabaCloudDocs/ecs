# View the resources associated with a license

After you create a license management task, the system automatically discovers and collects statistics on resources associated with the licenses managed by the license management task, automated discovery rules, and resources that fail to be associated with the licenses based on the parameters such as License Type, Automated discovery rules, and Instance Quantity Limit Setting.

## View the resources associated with a license

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **License Manager**.

3.  On the **Managed license** page, click the license ID to go to the Basic Information page.

4.  Click the Tracked resources tab to view the associated resources that meet the configured conditions and rules of the license management task.

    **Note:** License Manager automatically tracks the cloud resources that match your configured rules every 24 hours and updates the displayed information.


## View the resources that fail to be associated with a license

Some cloud resources may fail to be associated with your license because these cloud resources exceed the usage limits of your license or do not match your configured rules, or because system errors occur. You can perform the following operations to view these resources:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **License Manager**.

3.  On the **Managed license** page, click the license ID to go to the Basic Information page.

4.  Click the Associated wrong resource tab to view the resources that fail to be associated with the licenses managed by the license management task.


## View automated discovery rules

**Note:** You cannot modify or remove automated discovery rules. If you want to modify or remove an automated discovery rule, you must delete the license management task and create another one.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **License Manager**.

3.  On the **Managed license** page, click the license ID to go to the Basic Information page.

4.  Click the Automatic Identification License Rules tab to view the discovery rules of your license management task.


