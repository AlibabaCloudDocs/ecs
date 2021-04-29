---
keyword: [Cloud Assistant, remote commands, O&M plug-ins, send files]
---

# Overview

Cloud Assistant is a native automated operations and maintenance \(O&M\) tool designed for Elastic Compute Service \(ECS\). It can batch maintain ECS instances, execute shell, PowerShell and batch scripts, and send files on ECS instances. You do not need to enter passwords, log on to instances, or use jump servers when you perform these operations. Typically, you can use Cloud Assistant to install and uninstall software, start and stop services, distribute configuration files, and execute other commands or scripts.

## Features

After ECS instances that are installed with the Cloud Assistant client enter the **Running** \(`Running`\) state, you can use Cloud Assistant to perform the following operations on the instances by using the ECS console or by calling API operations:

-   Run batch and PowerShell scripts on Windows instances, or run shell scripts on Linux instances.
-   Upload files to the instances.
-   Run the same command on multiple instances. The execution status and results on an instance do not affect other instances.
-   Configure custom parameters in Cloud Assistant commands to adapt the commands to the needs of different scenarios.

**Note:** Cloud Assistant does not proactively initiate operations. You have full control over all Cloud Assistant operations.

## Scenarios

Cloud Assistant can help you perform deployment and O&M tasks on ECS instances. The following list provides some examples:

-   Uploading and running automated O&M scripts
-   Running existing scripts installed on instances
-   Managing software lifecycle
-   Deploying code or applications
-   Polling processes
-   Installing patches or security updates
-   Obtaining updates from Object Storage Service \(OSS\) or YUM repositories
-   Changing hostnames or user logon passwords

## Billing

Cloud Assistant is provided free of charge.

However, you may be charged for the ECS resources used by Cloud Assistant to deploy and maintain ECS instances. For more information about the billing of ECS resources, see [Billing overview](/intl.en-US/Pricing/Billing overview.md).

## Service limits

-   Only API operations can be used to configure the recurring executions of a Cloud Assistant command. The interval at which the command is run cannot be less than 10 seconds.
-   For each command, the total size of the Base64-encoded batch, PowerShell, or shell scripts together with the Base64-encoded custom parameters cannot exceed 16 KB.
-   The Base64-encoded file to send cannot exceed 32 KB in size.
-   Each command can contain a maximum of 20 custom parameters.
-   Cloud Assistant commands can be run only on instances that use the following operating systems:
    -   Alibaba Cloud Linux
    -   CentOS 6, CentOS 7, CentOS 8, and later
    -   CoreOS
    -   Debian 8, Debian 9, Debian 10, and later
    -   OpenSUSE
    -   Red Hat 5, Red Hat 6, Red Hat 7, and later

        For Red Hat instances, you must download the RPM package to install the Cloud Assistant client. For more information, see [Install the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Install the Cloud Assistant client.md).

    -   SUSE Linux Enterprise Server \(SLES\) 11, SLES 12, SLES 15, and later
    -   Ubuntu 12, Ubuntu 14, Ubuntu 16, Ubuntu 18, and later
    -   Windows Server 2012, Windows Server 2016, Windows Server 2019, and later

For more information about the limits and service quotas of Cloud Assistant, see the "Cloud Assistant limits" section of [Limits](/intl.en-US/Product Introduction/Limits.md).

## Terms

The following table describes relevant terms in Cloud Assistant.

|Term|Description|
|:---|:----------|
|Cloud Assistant|A tool provided by Alibaba Cloud that can help you perform routine maintenance tasks on multiple ECS instances and ECS bare metal instances at a time. Cloud Assistant is available in all Alibaba Cloud regions.|
|Cloud Assistant client|A lightweight plug-in that can be installed on ECS instances to run Cloud Assistant commands. -   In Windows instances, the process of the client program is AliyunService.
-   In Linux instances, the process of the client program is aliyun.service. |
|Cloud Assistant daemon process|A daemon process that is used to monitor the resource consumption of the Cloud Assistant client, report the running status of the client, and restart the client when the client fails. -   Service name: `AssistDaemon`
-   Path: /usr/local/share/assist-daemon/assist\_daemon

**Note:** The Cloud Assistant daemon process is available only for Linux instances. |
|task execution path|A path in which Cloud Assistant saves your command as a file on an ECS instance before the file is executed. The path varies based on the operating system.

-   Linux: /tmp
-   Windows: <Installation path of Cloud Assistant\>/work/script |
|command|A specific command such as a shell script or a PowerShell script that can be run on ECS instances.|
|custom parameter|A variable that you configure in the \{\{key\}\} format in a command. You can configure a custom parameter and its value in the \{\{"key":"value"\}\} format when you create a task to run the command. You can have a limited number of Cloud Assistant commands in each Alibaba Cloud region. To adapt Cloud Assistant commands to multiple scenarios, we recommend that you configure custom parameters.|
|one-time execution|An execution \(`Invocation`\) that runs a command only once on one or more instances.|
|recurring execution|An execution that periodically runs a command on one or more instances based on your specified time series or interval.|
|execution status|The relationships among different types of execution status. For more information, see the [t9581.md\#](/intl.en-US/Deployment & Maintenance/Cloud assistant/Overview.md) section.|

## Execution status

The following table describes the instance-level execution status of a command that is run only once on a single instance. The InvocationStatus parameter in API indicates the execution status of the command.

|Status in an API operation|Status in the ECS console|Description|
|--------------------------|:------------------------|:----------|
|`Running`|Task Running|The command is being run.|
|`Stopping`|Task Stopping|The command is being stopped.|
|`Stopped`|Manually Stopped|The command is stopped.|
|`Finished`|Task Completed|The command is run to completion. This does not indicate that the command succeeds. You can check whether the command succeeds based on the output \(`Output`\) and the exit code \(`ExitCode`\).|
|`Failed`|Task Failed|The command cannot be run or the command process is not run to completion before the timeout period specified by `Timeout` expires.|

## Status of batch executions and recurring executions

To better manage batch executions and recurring executions, you can manage the lifecycles of the executions from the perspectives of the overall execution status, the instance-level execution status, and the record-level execution status. The InvokeStatus parameter in API indicates the execution status of a command. The following figure shows the relationships among the three types of execution status.

![Relationships among the three types of execution status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7497919951/p5245.png)

-   The following table shows the overall execution status of a command that is run on multiple instances at the same time.

    |Status in an API operation|Status in the ECS console|Description|Priority|
    |--------------------------|-------------------------|-----------|--------|
    |`Running`|Task Running|The instance-level execution status is Running on some or all instances.|1|
    |`Stopping`|Task Stopping|The instance-level execution status is Stopping on some or all instances.|2|
    |`Stopped`|Manually Stopped|The instance-level execution status is Stopped on all instances.|3|
    |`Failed`|Task Failed|The instance-level execution status is Failed on all instances, or is Failed on some instances and is Stopped on the other instances.|4|
    |`Finished`|Task Completed|The instance-level execution status is Finished on all instances, or is Finished on some instances and is Stopped on the other instances.|5|
    |`PartialFailed`|Partially Failed|The instance-level execution status is Failed on some instances and is Finished on the other instances.|6|

    The following figure shows the relationship between the overall execution status and the instance-level execution status of the execution that runs a command on three instances at the same time.

    ![Lifecycle of a one-time execution on multiple instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7497919951/p5246.png)

-   The following table shows the status of recurring executions of a command.

    |Status|Description|
    |:-----|:----------|
    |Overall execution status|The overall execution status is always **Running** \(`Running`\) unless you stop the command on all the instances.|
    |Instance-level execution status|The instance-level execution status is always **Running** \(`Running`\) unless you stop the command on the instance.|
    |Record-level execution status|For more information, see the [t9581.md\#](/intl.en-US/Deployment & Maintenance/Cloud assistant/Overview.md) section.|


## API operations

You can use Cloud Assistant by using the ECS console or by calling an API operation.

|Business requirement|Reference|API operation|
|--------------------|---------|-------------|
|The Cloud Assistant client must be installed on an ECS instance before Cloud Assistant can be used on the instance. By default, ECS instances created from public images after December 01, 2017 are pre-installed with the Cloud Assistant client. Therefore, you must manually install the Cloud Assistant client on some ECS instances.|[Install the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Install the Cloud Assistant client.md)|-   [InstallCloudAssistant](/intl.en-US/API Reference/Cloud assistant/InstallCloudAssistant.md)
-   [DescribeCloudAssistantStatus](/intl.en-US/API Reference/Cloud assistant/DescribeCloudAssistantStatus.md) |
|You are familiar with using OpenAPI Explorer and this is the first time that you use Cloud Assistant.|-   [Use Java to manage ECS instances without logon](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/Use Java to manage ECS instances without logon.md)
-   [Use Python to manage ECS instances without logging on to the instances](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/Use Python to manage ECS instances without logging on to the instances.md)

|N/A|
|Create a Cloud Assistant command.|[Create a command](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Create a command.md)|-   [RunCommand](/intl.en-US/API Reference/Cloud assistant/RunCommand.md)
-   [CreateCommand](/intl.en-US/API Reference/Cloud assistant/CreateCommand.md) |
|Run a created command on ECS instances.|[Run a command](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Run a command.md)|-   [RunCommand](/intl.en-US/API Reference/Cloud assistant/RunCommand.md)
-   [InvokeCommand](/intl.en-US/API Reference/Cloud assistant/InvokeCommand.md) |
|View the execution status and results of commands. Execution results are the actual outputs generated on the specified instances.|[Query execution results and fix common problems](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Query execution results and fix common problems.md)|-   [DescribeInvocations](/intl.en-US/API Reference/Cloud assistant/DescribeInvocations.md)
-   [DescribeInvocationResults](/intl.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md) |
|Modify a created command. You can modify the name and description of the command.|[Modify a command](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Modify a command.md)|N/A|
|Create a new version of an existing Cloud Assistant command or modify the properties of the command such as the name, description, type, content, execution path, or timeout period.|[Clone a command](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Clone a command.md)|N/A|
|Stop a running command.|[Stop a command](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Stop a command.md)|[StopInvocation](/intl.en-US/API Reference/Cloud assistant/StopInvocation.md)|
|Delete Cloud Assistant commands that are no longer needed so that you can have sufficient quota balance to create new commands.|[Delete a command](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Delete a command.md)|[DeleteCommand](/intl.en-US/API Reference/Cloud assistant/DeleteCommand.md)|

