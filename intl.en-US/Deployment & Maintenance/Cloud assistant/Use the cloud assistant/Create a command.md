---
keyword: [Cloud Assistant, remote command, ECS, Alibaba Cloud, O&M]
---

# Create a command

You can use Cloud Assistant commands to perform routine tasks on ECS instances. These tasks include running automated O&M scripts, polling processes, resetting user passwords, installing or uninstalling software, updating applications, and installing patches. Command types can be batch or PowerShell for Windows instances, and shell for Linux instances. You can specify custom parameters as variables in Cloud Assistant commands.

-   You can retain a maximum of 100 Cloud Assistant commands within each Alibaba Cloud region. This quota may increase based on your ECS usage.

    **Note:** You can also call the DescribeAccountAttributes operation with AttributeName.N set to max-axt-command-count to query the maximum number of Cloud Assistant commands that you can retain within a region.

-   A command cannot exceed 16 KB in size after it is encoded in Base64.
-   A maximum of 20 custom parameters can be specified in a Cloud Assistant command.
-   When you create a command, you must check whether the syntax, logic, and algorithm of the command are correct.

    For example, assume that you have created the /backup directory \(`mkdir /backup`\) on an instance, you can run the following shell commands to archive a file in this directory:

    ```
    #! /bin/bash 
    OF=/backup/my-backup-$(date +%Y%m%d).tgz
    tar -cf $OF {{file}}
    ```

    **Note:** In this example, `{{file}}` is a custom parameter. When you run the commands, you can set this custom parameter to the name of the file to be archived. Example: /app/usrcredential. Custom parameters can be used in scenarios of dynamic values and multi-purpose values. We recommend that you specify custom parameters for security-sensitive data or data that changes based on the environment. Such data includes AccessKey pairs, instance IDs, authorization codes, time parameters, and critical system files.


## Procedure in the console

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **Cloud Assistant**.

3.  In the top navigation bar, select a region.

4.  Click **Create or Run Command**.

5.  In the **Command Information** section, configure the corresponding parameters.

    The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |Command Source|The source of the command.    -   **New Command**: Create a command.
    -   **Existing Command**: Select a command from the existing ones. |
    |Command Name|The name of the command.|
    |Command Type|The type of the command.    -   For Linux instances, select **Shell**.
    -   For Windows instances, select **Bat** or **PowerShell**. |
    |Command|The content of the command. You can enter or paste the command content.For more information about shell commands, see [View instance configurations](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/View instance configurations.md). |
    |Use Parameters|The option that specifies whether to enable parameters.If you turn on **Use Parameters**, you can specify custom parameters in the `{{key}}` format in the **Command** field. |
    |Command Parameters|The values of the custom parameters specified in the **Command** field in the `{{key}}` format.This parameter is available only when **Use Parameters** is turned on. |
    |Save Command|The option that specifies whether to save the command.|
    |Command Description|The description of the command. We recommend that you enter information such as the purpose of the command to facilitate subsequent management and maintenance.|
    |Execution Path|The custom execution path of the command. The following list provides default execution paths for instances that have different operating systems:    -   For Linux instances, the default execution path is the /home directory of the root user.
    -   For Windows instances, the default execution path is the directory where the process of the Cloud Assistant client is located, such as C:\\ProgramData\\aliyun\\assist\\$\(version\). |
    |Timeout Period|The **timeout period** for the command to run instances. If the command times out, Cloud Assistant forcibly stops the execution process.Unit: seconds. Default value: 60. Minimum value: 10. If you set **Timeout Period** to a value less than 10 seconds, the system changes the value to 10 seconds to ensure that the execution succeeds. |

6.  In the **Select Instances** section, select the instances on which you want to run the command.

7.  Click **OK**.


## Procedure by using Alibaba Cloud CLI

-   Sample request:

    Call the CreateCommand operation to create a Cloud Assistant command named test. The command content is `echo 123` and is encoded in Base64 as plaintext. For Windows instances, set Type to RunBatScript or RunPowershellScript.

    ```
    aliyun ecs CreateCommand --RegionId TheRegionId --CommandContent ZWNobyAxMjM= --Type RunShellScript --Name test --Description test --output cols=CommandId
    ```

-   Sample response:

    ```
    CommandId
    ---------
    c-hz0b8osxk8a***
    ```


[Run commands](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Run commands.md)

**Note:** If you turn on Use Parameters when you create a command, you must enter parameter values in the **Command Parameters** fields when you run the command.

**Related topics**  


[CreateCommand](/intl.en-US/API Reference/Cloud assistant/CreateCommand.md)

[DescribeAccountAttributes](/intl.en-US/API Reference/Others/DescribeAccountAttributes.md)

