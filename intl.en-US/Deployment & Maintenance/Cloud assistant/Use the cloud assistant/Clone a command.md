---
keyword: [Cloud Assistant, remote command, O&M plug-in, Alibaba Cloud, ECS]
---

# Clone a command

A clone command operation is equivalent to an operation that creates a new version of an existing Cloud Assistant command. You can retain all the information of the original command \(cloned command\), or you can modify the name, description, type, content, execution path, or timeout period in the new command \(command clone\).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **Cloud Assistant**.

3.  In the top navigation bar, select a region.

4.  Find the Cloud Assistant command that you want to clone and click **Clone** in the **Actions** column.

5.  In the **Clone Command** panel, configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |Command Name|The name of the new command.|
    |Command Type|The type of the new command.    -   For Linux instances, select **Shell**.
    -   For Windows instances, select **Bat** or **PowerShell**. |
    |Command|The content of the new command. You can enter or paste content to the Command field.For more information about shell commands, see [View instance configurations](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/View instance configurations.md). |
    |Use Parameters|Specifies whether to enable parameters.If you turn on **Use Parameters**, you can specify custom parameters in the `{{key}}` format in the **Command** field. |
    |Command Description|The description of the new command. We recommend that you enter information such as the purpose of the command to facilitate subsequent management and maintenance.|
    |Execution Path|The custom execution path of the new command. Default execution paths are provided for instances that run different operating systems.    -   For Linux instances, the default execution path is the /home directory of the root user.
    -   For Windows instances, the default execution path is the directory where the process of the Cloud Assistant client is located, such as C:\\ProgramData\\aliyun\\assist\\$\(version\). |
    |Timeout Period|The **timeout period** for a task that runs the new command on ECS instances. If the task times out, Cloud Assistant forcibly stops the task process.Unit: seconds. Default value: 60. Minimum value: 10. If you set **Timeout Period** to a value of less than 10 seconds, the system changes the value to 10 seconds to ensure that the command can be executed. |

6.  After you confirm the configured parameters, click **OK**.


