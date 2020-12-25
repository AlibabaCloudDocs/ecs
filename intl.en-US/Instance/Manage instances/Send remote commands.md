---
keyword: [remote command, ECS, Alibaba Cloud, O&M]
---

# Send remote commands

You can send remote commands to perform O&M operations on one or more instances without logging on to the instances.

-   The instances that are used to receive commands are in the **Running** state.
-   The Cloud Assistant client is started on the instances. For more information, see [Start or stop the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Start or stop the Cloud Assistant client.md).

You must use Cloud Assistant to send and run remote commands, and the remote commands consume the quota of Cloud Assistant commands. For more information about Cloud Assistant and its limits, see [Overview](/intl.en-US/Deployment & Maintenance/Cloud assistant/Overview.md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Select one of the following methods to send a remote command:

    -   To send a remote command to a single instance, find the instance on the Instances page and click its ID to go to the **instance details** page. Click the **Remote Commands** tab and then click **Send Command**.
    -   To send a remote command to multiple instances, select the instances on the Instances page. In the lower part of the page, choose **More** \> **Send Command**.
5.  In the dialog box that appears, perform the following operations.

    **Note:** If some instances run Linux and others run Windows, you must configure the instances based on their operating systems when you perform batch operations on multiple instances.

    1.  Select a command type.

        -   Linux instances: **Shell** is selected by default.
        -   Windows instances: Select **Bat** or **PowerShell**.
    2.  Specify whether to retain commands.

        **Note:** You can view the retained commands on the Cloud Assistant page and run these commands repeatedly. For more information about how to use Cloud Assistant to run remote commands on ECS instances, see [Run a command](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Run a command.md).

    3.  In the **Command Content** code editor, enter a command.

        **Note:**

        -   The command must be able to return the results of a single execution. Interactions with returned information are not allowed.
        -   For more information about shell commands, see [View instance configurations](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/View instance configurations.md).
    4.  Click **Run**.

        -   You can click **Stop** to cancel the execution of a command.
        -   After the execution is complete, you can view the command output in the **Command Output** section.

            To view the command output and execution results of each instance, click the instance ID.

        **Note:** After an execution is complete, you can enter another command in the **Command Content** code editor to run the command.


