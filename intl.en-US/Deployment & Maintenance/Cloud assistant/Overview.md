---
keyword: [Cloud Assistant, remote command, O&M plug-in, Alibaba Cloud, ECS]
---

# Overview

Cloud Assistant is an Alibaba Cloud proprietary tool used to perform O&M and deployment tasks for ECS. Cloud Assistant can automatically run batch, PowerShell, or shell commands on multiple instances at a time without the need to connect to the instances. You can use Cloud Assistant to perform different tasks such as running automated O&M scripts, polling processes, installing or uninstalling software, updating applications, and installing patches.

## Features

After you install the Cloud Assistant client on ECS instances, you can use Cloud Assistant to perform the following operations on the instances in the ECS console or through calls to API operations:

-   Run batch, PowerShell \(for Windows instances\), or shell \(for Linux instances\) commands on one or more instances that are in the **Running** \(`Running`\) state.
-   Run the same command on multiple instances. The execution status and results on different instances do not affect each other.
-   Configure custom parameters in Cloud Assistant commands to adapt the commands to the needs of different scenarios.

    **Note:** Cloud Assistant does not proactively initiate operations. You have full control over all Cloud Assistant operations.


## Scenarios

Cloud Assistant can help you perform deployment and O&M tasks on ECS instances. The following list provides some examples:

-   Uploading and running automated O&M scripts
-   Running existing scripts on instances
-   Managing software lifecycle
-   Deploying code or applications
-   Polling processes
-   Installing patches or security updates
-   Obtaining updates from Object Storage Service \(OSS\) or YUM repositories
-   Changing hostnames or user logon passwords

## Billing method

Cloud Assistant is provided free of charge.

However, you may be charged for the ECS resources used by Cloud Assistant to deploy and maintain ECS instances. For more information about the billing of ECS resources, see [Billing overview](/intl.en-US/Pricing/Billing overview.md).

## Limits

-   Only API operations can be used to configure recurring commands. The recurring interval cannot be less than 10 seconds.
-   For each command, the total size of the Base64-encoded batch, PowerShell, or shell script together with the custom parameters cannot exceed 16 KB.
-   Each command can contain a maximum of 20 custom parameters.
-   Cloud Assistant commands can be run only on instances that use the following operating systems:
    -   Alibaba Cloud Linux
    -   CentOS 6, CentOS 7, CentOS 8, and later
    -   CoreOS
    -   Debian 8, Debian 9, Debian 10, and later
    -   OpenSUSE
    -   RedHat 5, RedHat 6, RedHat 7, and later

        For RedHat instances, you need to download the RPM package to install the Cloud Assistant client. For more information, see [Install the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Install the Cloud Assistant client.md).

    -   SUSE Linux Enterprise Server \(SLES\) 11, SLES 12, SLES 15, and later
    -   Ubuntu 12, Ubuntu 14, Ubuntu 16, Ubuntu 18, and later
    -   Windows Server 2012, Windows Server 2016, Windows Server 2019, and later

For the limits and quotas of Cloud Assistant, see the "Cloud Assistant limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md).

## Terms

The following table describes relevant terms in Cloud Assistant.

|Term|Description|
|:---|:----------|
|Cloud Assistant|A tool provided by Alibaba Cloud that can automatically perform routine maintenance tasks on ECS instances such as ECS bare metal instances. Cloud Assistant is available in all Alibaba Cloud regions.|
|Cloud Assistant client|A lightweight plug-in that can be installed on ECS instances to run Cloud Assistant commands on the instances. -   In Windows instances, the process of the client program is AliyunService.
-   In Linux instances, the process of the client program is aliyun.service. |
|Cloud Assistant daemon|A daemon that is used to monitor the resource consumption of the Cloud Assistant client, report the running status of the client, and restart the client when the client fails.-   Service name: `AssistDaemon`
-   Path: /usr/local/share/assist-daemon/assist\_daemon

**Note:** The Cloud Assistant daemon is available only for Linux instances. |
|task execution path|A path in which Cloud Assistant saves your command as a file on an ECS instance before the file is executed. The path varies based on the operating system.

-   Linux: /tmp
-   Windows: <Installation path of Cloud Assistant\>/work/script |
|command|A specific command such as a shell script or a PowerShell script that can be run on ECS instances.|
|custom parameter|A variable that you set in the \{\{key\}\} format in a command. You can set a custom parameter and its value in the \{\{"key":"value"\}\} format when you run a command. You can have a limited number of Cloud Assistant commands in each Alibaba Cloud region. We recommend that you configure custom parameters to adapt Cloud Assistant commands to multiple scenarios.|
|one-time task|A task \(`Invocation`\) that runs one command once on one or more instances.|
|recurring task|A task in which you can specify the time series or period to run one command periodically on one or more instances.|
|task status|The execution status of a command task. For more information, see [t9581.md\#](/intl.en-US/Deployment & Maintenance/Cloud assistant/Overview.md).|

## Execution status of a command task

The following table describes the execution status of a task that runs a command on an instance. The corresponding API parameter is InvocationStatus.

|Status in an API operation|Status in the console|Description|
|--------------------------|:--------------------|:----------|
|`Running`|Task Running|The task is being run.|
|`Stopping`|Task Stopping|The task is being stopped.|
|`Stopped`|Manually Stopped|The task is stopped.|
|`Finished`|Task Completed|The task is complete. This does not indicate that the task succeeds. You can check whether the task succeeds based on the output \(`output`\) and exit code \(`exitcode`\).|
|`Failed`|Task Failed|The task cannot be run or the execution process exceeds the timeout period specified by `Timeout`.|

## Execution status of a batch task

Every time a command task is executed on an instance, an execution record is generated with execution status. To better manage batch tasks and recurring tasks, you can manage the lifecycle of a task from the perspectives of the overall execution status, the instance-level execution status, and the record-level execution status. The corresponding API parameter is InvokeStatus. The following figure shows the relationships among the three types of execution status.

![Relationships among the three types of execution status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7497919951/p5245.png)

-   The following table shows the overall execution status of a batch task that runs a command on multiple instances.

    |Status in an API operation|Status in the console|Description|Priority|
    |--------------------------|---------------------|-----------|--------|
    |`Running`|Task Running|The task is running on some or all instances.|1|
    |`Stopping`|Task Stopping|The task is being stopped on some or all instances.|2|
    |`Stopped`|Manually Stopped|The task is stopped on all instances.|3|
    |`Failed`|Task Failed|The task fails on all instances or the task fails on some instances and is stopped on the other instances.|4|
    |`Finished`|Task Completed|The task is complete on all instances or the task is complete on some instances and is stopped on the other instances.|5|
    |`PartialFailed`|Partially Failed|The task fails on some instances and is complete on the other instances.|6|

    The following figure shows the relationship between the overall execution status and the instance-level execution status of a one-time batch task that runs a command on three instances at the same time.

    ![Lifecycle of a one-time batch task](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7497919951/p5246.png)

-   The following table shows the execution status of a recurring task.

    |Status|Description|
    |:-----|:----------|
    |Overall execution status|The overall execution status is always **Running** \(`Running`\) unless you stop the task from running on all the instances.|
    |Instance-level execution status|The execution status on a single instance is always **Running** \(`Running`\) unless you stop the task from running on the instance.|
    |Record-level execution status|For more information, see [t9581.md\#](/intl.en-US/Deployment & Maintenance/Cloud assistant/Overview.md).|


## Operations

You can use Cloud Assistant in the ECS console or by calling an API operation.

|Business requirement|Reference|API operation|
|--------------------|---------|-------------|
|The Cloud Assistant client must be installed on an ECS instance before Cloud Assistant can be used. By default, ECS instances created from public images after December 01, 2017 are pre-installed with the Cloud Assistant client. You need to manually install the Cloud Assistant client on some ECS instances.|[Install the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Install the Cloud Assistant client.md)|-   [InstallCloudAssistant](/intl.en-US/API Reference/Cloud assistant/InstallCloudAssistant.md)
-   [DescribeCloudAssistantStatus](/intl.en-US/API Reference/Cloud assistant/DescribeCloudAssistantStatus.md) |
|You are familiar with using OpenAPI Explorer and this is the first time that you use Cloud Assistant.|-   [Use Java to manage ECS instances without logon](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/Use Java to manage ECS instances without logon.md)
-   [Use Python to manage ECS instances without logon](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/Use Python to manage ECS instances without logon.md)

|N/A|
|Create a Cloud Assistant command.|[Create a command](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Create a command.md)|-   [RunCommand](/intl.en-US/API Reference/Cloud assistant/RunCommand.md)
-   [CreateCommand](/intl.en-US/API Reference/Cloud assistant/CreateCommand.md) |
|Run a created command on ECS instances.|[Run commands](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Run commands.md)|-   [RunCommand](/intl.en-US/API Reference/Cloud assistant/RunCommand.md)
-   [InvokeCommand](/intl.en-US/API Reference/Cloud assistant/InvokeCommand.md) |
|View the execution status and results of tasks. Execution results are the actual outputs generated on the specified instances.|[Query execution results and fix common problems](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Query execution results and fix common problems.md)|-   [DescribeInvocations](/intl.en-US/API Reference/Cloud assistant/DescribeInvocations.md)
-   [DescribeInvocationResults](/intl.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md) |
|Modify a created command. You can modify the name and description of the command.|[Modify a command](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Modify a command.md)|N/A|
|Create a new version of an existing Cloud Assistant command or modify the attributes of the command such as the name, description, type, content, execution path, or timeout period.|[Clone a command](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Clone a command.md)|N/A|
|Stop a running command|[Stop a command](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Stop a command.md)|[StopInvocation](/intl.en-US/API Reference/Cloud assistant/StopInvocation.md)|
|Delete Cloud Assistant commands that are no longer needed so that you can have sufficient quota balance to create new commands.|[Delete a command](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Delete a command.md)|[DeleteCommand](/intl.en-US/API Reference/Cloud assistant/DeleteCommand.md)|

