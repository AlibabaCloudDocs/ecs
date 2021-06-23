---
keyword: [Cloud Assistant, remote command, O&M plug-in, Alibaba Cloud, ECS]
---

# Run a command

After you create a Cloud Assistant command, you can run it on one or more Elastic Compute Service \(ECS\) instances. The execution status and results of this command on multiple instances do not affect each other.

Before you run a Cloud Assistant command on ECS instances, make sure that the instances meet the following requirements:

-   The instances are in the **Running** \(`Running`\) state.
-   The instances are installed with the Cloud Assistant client. For more information, see [Install the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Install the Cloud Assistant client.md).

-   You can call an API operation to run a command on up to 50 instances.
-   If you select more than 50 instances to run a command in the ECS console, the system runs the command on the instances in batches.
-   You can run Cloud Assistant commands up to 5,000 times within a region per day. This quota may increase based on your ECS usage. For more information about how to query the quota, see [Step 1: View resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).

    **Note:** You can also call the DescribeAccountAttributes operation with the AttributeName.N parameter set to max-axt-invocation-daily to query the maximum number of times that you can run Cloud Assistant commands within in a region per day.


## Procedure in the console

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **ECS Cloud Assistant**.

3.  In the top navigation bar, select a region.

4.  Find the command that you want to run and click **Create Task** in the **Actions** column.

5.  In the **Create Task** panel, configure the execution parameters.

    ![Check the command information before you run the command](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4597919951/p83754.png)

    1.  In the **Command Information** section, check the command content and set Command Parameters and Username.

        |Parameter|Description|
        |---------|-----------|
        |Command|Click **View** to check the command.|
        |Implementation plan|The command execution time.         -   **Immediate execution**: If this value is selected, the command is run immediately after you click **Run** or **Execute and Save**.
        -   **After the next startup of the system**: If this value is selected, the command is run the next time the selected instances are started after you click **Run** or **Execute and Save**.
        -   **After each system startup**: If this value is selected, the command is run each time the selected instances are started after you click **Run** or **Execute and Save**. |
        |Username|The name of the user who runs the command on the ECS instance. The best practice for managing permissions is to run commands based on the least privilege principle. We recommend that you run Cloud Assistant commands as a regular user. For more information, see [Run Cloud Assistant commands as a regular user](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/Run Cloud Assistant commands as a regular user.md).

By default, Cloud Assistant commands are run by the root user on Linux instances and by the system user on Windows instances. |
        |Password Name|The password used by the user hosted in Operation Orchestration Service \(OOS\) that is executing the command. This parameter is required only when the command is run by a regular user other than the system user on Windows instances. If the password of the user executing the command is not hosted in OOS, you must create and host the password in the parameter repository of OOS. For more information, see [Create encryption parameters]() and [Run Cloud Assistant commands on Windows instances as a regular user](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/Run Cloud Assistant commands as a regular user.mdsection_rgk_3gp_gdi). |
        |Command Parameters|In the **Command Parameters** fields, enter values for the custom parameters specified in the command. No format limits apply to the data types of values for the custom parameters. If the current task does not require values for these fields, you can leave the fields empty. **Note:** If you did not select **Use Parameters** when you create the command, the **Command Parameters** fields are not displayed in the Create Task panel. |

    2.  In the **Select Instances** section, select one or more instances.

        If you have multiple instances, you can enter instance IDs or names to search for instances, and select tags or client status as filter conditions from the drop-down list to narrow down the search results.

6.  Click **Create Task**.


## Procedure by using the CLI

1.  Check the status of the instances on which you want to run a command. If the instances are not in the **Running** \(`Running`\) state, call the StartInstance operation to start the instances.

    ```
    aliyun ecs StartInstance --InstanceId 'i-bp1f4f6o8lv0wqof****' 
    ```

    **Note:** Values enclosed within single quotation marks \(''\) are example values of the parameters and must be changed based on actual conditions.

    For more information, see [StartInstance](/intl.en-US/API Reference/Instances/StartInstance.md).

2.  Call the DescribeCloudAssistantStatus operation to check whether the Cloud Assistant client is installed on the instances.

    ```
    aliyun ecs DescribeCloudAssistantStatus --RegionId 'cn-hangzhou' \
    --InstanceId.1 'i-bp1f4f6o8lv0wqof****' 
    ```

    If the value of `CloudAssistantStatus` is true in the response, the Cloud Assistant client is installed on the instances. Otherwise, call the InstallCloudAssistant operation to install the Cloud Assistant client on the instances. For more information, see [DescribeCloudAssistantStatus](/intl.en-US/API Reference/Cloud assistant/DescribeCloudAssistantStatus.md) and [InstallCloudAssistant](/intl.en-US/API Reference/Cloud assistant/InstallCloudAssistant.md).

3.  Call the InvokeCommand operation to run a created Cloud Assistant command on the instances and obtain the InvokeId response parameter.

    ```
    aliyun ecs InvokeCommand --RegionId 'cn-hangzhou' \
    --InstanceId.1 'i-bp1f4f6o8lv0wqof****' \
    --InstanceId.2 'i-bp137qu6142s3mhm****' \
    --CommandId 'c-hz018qp243j****' \
    --Timed 'false' \
    --output cols=InvokeId
    ```

    |Parameter|Example|Description|
    |---------|-------|-----------|
    |RegionId|cn-hangzhou|The region ID.|
    |InstanceId.1|i-bp1f4f6o8lv0wqof\*\*\*\*|The ID of the first instance on which to run the command.|
    |InstanceId.2|i-bp137qu6142s3mhm\*\*\*\*|The ID of the second instance on which to run the command.|
    |CommandId|c-hz018qp243j\*\*\*\*|The ID of the command.|
    |Timed|false|Specifies whether to periodically run the command. If you want to periodically run a command, set **Timed** to true. The **Frequency** parameter specifies the execution cycle. For example, 0 \*/20 \* \* \* \* indicates that the command is run every 20 minutes. For more information, see [Cron expression](/intl.en-US/Deployment & Maintenance/Cloud assistant/Cron expression.md). |

    For more information, see [InvokeCommand](/intl.en-US/API Reference/Cloud assistant/InvokeCommand.md).


**Related topics**  


[Query execution results and fix common problems](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Query execution results and fix common problems.md)

[DescribeAccountAttributes](/intl.en-US/API Reference/Others/DescribeAccountAttributes.md)

[InvokeCommand](/intl.en-US/API Reference/Cloud assistant/InvokeCommand.md)

