---
keyword: [Cloud Assistant, remote command, ECS, Alibaba Cloud, O&M]
---

# Immediate execution

You can create and run a command simultaneously by using the immediate execution feature.

-   The instances on which to run a command are in the **Running** \(Running\) state.
-   You can retain a maximum of 100 Cloud Assistant commands within an Alibaba Cloud region. This quota may increase based on your ECS usage. For more information about how to view the quota, see [Step 1: View resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md). If you click **Run** when you are creating a command, the command does not count against your command quota.

    **Note:** You can also call the DescribeAccountAttributes operation with AttributeName.N set to max-axt-command-count to query the maximum number of Cloud Assistant commands that you can retain within a region.

-   You can run Cloud Assistant commands up to 5,000 times within a region per day. This quota may increase based on your ECS usage. For more information about how to query the quota, see [Step 1: View resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).

    **Note:** You can also call the DescribeAccountAttributes operation with the AttributeName.N parameter set to max-axt-invocation-daily to query the maximum number of times that you can run Cloud Assistant commands within in a region per day.


When you use the immediate execution feature, take note of the following items:

-   A command cannot exceed 16 KB in size after it is encoded in Base64.
-   A maximum of 20 custom parameters can be specified in a Cloud Assistant command.
-   You can call an API operation to run a command on up to 50 instances.
-   When you create a command, you must check whether the syntax, logic, and algorithm of the command are correct.

    For example, assume that you have created the /backup directory \(`mkdir /backup`\) on an instance, you can run the following shell commands to archive a file in this directory:

    ```
    #!/bin/bash 
    OF=/backup/my-backup-$(date +%Y%m%d).tgz
    tar -cf $OF {{file}}
    ```

    **Note:** In the preceding example, `{{file}}` is a custom parameter. When you run the commands, you can set this custom parameter to the name of the file to be archived. Example: /app/usrcredential. Custom parameters can be used in scenarios of dynamic values and multi-purpose values. We recommend that you specify custom parameters for security-sensitive data or data that changes based on the environment, including AccessKey pairs, instance IDs, authorization codes, time parameters, and critical system files.


## Procedure in the console

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **ECS Cloud Assistant**.

3.  In the top navigation bar, select a region.

4.  Click **Create or Run Command**.

5.  In the **Command Information** section, configure the parameters described in the following table.

    |Parameter|Description|
    |---------|-----------|
    |Command Source|The source of the command.     -   **Enter Command Content**: creates a command.
    -   **Select Saved Command**: selects an existing command. |
    |Command Name|The name of the command.|
    |Implementation plan|The command execution time.     -   **Immediate execution**: If this value is selected, the command is run immediately after you click **Run** or **Execute and Save**.
    -   **After the next startup of the system**: If this value is selected, the command is run the next time the selected instances are started after you click **Run** or **Execute and Save**.
    -   **After each system startup**: If this value is selected, the command is run each time the selected instances are started after you click **Run** or **Execute and Save**. |
    |Command Type|The type of the command.     -   For Linux instances, select **Shell**.
    -   For Windows instances, select **Bat** or **PowerShell**. |
    |Command|The content of the command. You can enter or paste the command content. For more information about shell commands, see [View instance configurations](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/View instance configurations.md). |
    |Use Parameters|Specifies whether to use parameters. If you turn on **Use Parameters**, you can specify custom parameters in the `{{key}}` format in the **Command** field. |
    |Command Parameters|The values of the custom parameters specified in the `{{key}}` format in the **Command** field. This parameter is available only when **Use Parameters** is turned on.

**Note:** You can use the parameter store of Operation Orchestration Service \(OOS\) in Cloud Assistant commands. For more information, see [Use OOS Parameter Store in Cloud Assistant commands](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/Use OOS Parameter Store in Cloud Assistant commands.md) |
    |Command Description|The description of the command. We recommend that you enter information such as the purpose of the command to make it easier to manage and maintain.|
    |Username|The name of the user running the command on the ECS instance. The best practice in permission management is to run commands based on the least privilege principle. We recommend that you run Cloud Assistant commands as a regular user. For more information, see [Run Cloud Assistant commands as a regular user](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/Run Cloud Assistant commands as a regular user.md).

By default, Cloud Assistant commands are run by the root user on Linux instances and by the system user on Windows instances. |
    |Password Name|The password of the execution user that is hosted in Operation Orchestration Service \(OOS\). This parameter is required only when the command is run by a regular user other than the system user on Windows instances. If the password of the execution user is not hosted in OOS, you must create and host the password in the parameter store of OOS. For more information, see [Run Cloud Assistant commands on Windows instances as a regular user](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/Run Cloud Assistant commands as a regular user.md). |
    |Execution Path|The custom execution path of the command. The following list provides default execution paths for instances that use different operating systems:    -   For Linux instances, the default execution path is the /home directory of the root user.
    -   For Windows instances, the default execution path is the directory where the process of the Cloud Assistant client is located. Example: C:\\ProgramData\\aliyun\\assist\\$\(version\). |
    |Timeout Period|The timeout period for the command to run on instances. If a task that runs a command times out, Cloud Assistant forcibly stops the task process.**** Unit: seconds. Default value: 60. Minimum value: 10. If you set **Timeout Period** to a value of less than 10, the system changes the value to 10 to ensure that the execution succeeds. |

6.  In the **Select Instances**section, select the instances on which you want to run the command.

7.  Click **Execute and Save** or **Run**.


## Procedure by using the CLI

-   Sample request:

    Call the RunCommand operation to create a Cloud Assistant command named update to update the operating system on instances.

    ```
    aliyun ecs RunCommand --RegionId 'cn-hangzhou' \
    --Name 'update' --Username 'root' --Type 'RunShellScript' \
    --CommandContent 'eXVtIC15IHVwZGF0ZQ==' \
    --Timeout '60' --RepeatMode 'Once' --ContentEncoding 'Base64' \
    --InstanceId.1 'i-bp12e0ib2ztibede****'
    ```

    **Note:** Values enclosed in single quotation marks \(''\) are example values of the parameters and must be changed based on actual conditions.

    |Parameter|Example|Description|
    |---------|-------|-----------|
    |RegionId|cn-hangzhou|The region ID.|
    |Name|update|The name of the command.|
    |Username|root|The name of the user running the command on the ECS instance.|
    |Type|RunShellScript|The type of the command. Valid values:     -   Linux: RunShellScript
    -   WWindows:RunBatScript or RunPowershellScript |
    |CommandContent|eXVtIHVwZGF0ZSAteQ==|The Base64-encoded content of the command.|
    |Timeout|60|The timeout period.|
    |RepeatMode|Once|The execution plan.|
    |ContentEncoding|Base64|The encoding format.|
    |InstanceId.1|i-bp12e0ib2ztibede\*\*\*\*|The ID of the ECS instance on which to run the command.|

    For more information, see [RunCommand](/intl.en-US/API Reference/Cloud assistant/RunCommand.md).

-   Sample response:

    ```
    {
            "CommandId": "c-hz018qlm868****",
            "InvokeId": "t-hz018qlm86d****",
            "RequestId": "1D24FA80-64DB-4842-AB20-25207994418F"
    }
    ```


**Related topics**  


[Query execution results and fix common problems](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Query execution results and fix common problems.md)

[RunCommand](/intl.en-US/API Reference/Cloud assistant/RunCommand.md)

[DescribeAccountAttributes](/intl.en-US/API Reference/Others/DescribeAccountAttributes.md)

