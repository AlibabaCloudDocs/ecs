---
keyword: [Cloud Assistant, failure diagnosis, execution result, execution failed]
---

# Query execution results and fix common problems

You can run a Cloud Assistant command only when all requirements are met, regardless of whether you run the command in the ECS console or after you log on to an instance. To ensure that the intended operation is complete, we recommend that you view the command execution result and status after you run a command. If the execution fails, you can identify and fix the problem based on common error messages.

Different execution results and status are displayed for a command if exceptions occur. These exceptions include the lack of dependencies, network disruptions, command semantic errors, command debugging errors, and abnormal instance status. You can use the console or call an API operation to view error messages in the execution results, and diagnose and fix the problems.

## View execution results in the console

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **Cloud Assistant**.

3.  In the top navigation bar, select a region.

4.  Click the **Command Execution Result** tab to view the execution results and status.

    -   If the command execution succeeds, you can view the output in the execution results.
        1.  Find a record where **Task Completed** appears in the **Status** column.
        2.  In the **Actions** column, click **View**.
        3.  In the **Task Execution Results** panel, view the **Task Output** section.
    -   If the command execution fails, view error messages in the execution results, and diagnose and fix the problem based on the error messages.
        1.  Find a task where **Task Failed** appears in the **Status** column.
        2.  In the **Actions** column, click **View**.
        3.  In the **Task Execution Results** panel, view the error messages of the task.

            For information about common error messages and the solutions to the errors, see the [Command errors and solutions](#section_ar5_j06_zre) section.

            ![Error message](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5724390061/p161059.png)


## View execution results by using Alibaba Cloud CLI

If you use Cloud Assistant by means of Alibaba Cloud CLI or OpenAPI Explorer, you can call the DescribeInvocations or DescribeInvocationResults operation to query the execution results of Cloud Assistant commands. If the execution fails, you can refer to the ErrorCode and ErrorInfo fields for error details.

In the following examples, the DescribeInvocations and DescribeInvocationResults operations are used to describe how to use Alibaba Cloud CLI to query execution results.

-   Call the DescribeInvocations operation to query the execution status of a command.

    ```
    aliyun ecs DescribeInvocations --RegionId TheRegionId --InvokeId your-invoke-id
    ```

-   Call the DescribeInvocationResults operation to query the execution result of a command on a specific instance.

    ```
    aliyun ecs DescribeInvocationResults --RegionId TheRegionId --InstanceId i-bp1g6zv0ce8og\*\*\*\*\*\*p --InvokeId your-invoke-id
    ```


## Command errors and solutions

|Error code|Error message|Solution|
|----------|-------------|--------|
|InstanceNotRunning|The error message returned because the instance is not in the Running state while the task is being created.|Check whether the instance is running properly.|
|ClientNotRunning|The error message returned because the Cloud Assistant client is not running.|The Cloud Assistant client is stopped or not installed. Perform the following operations to install or start the Cloud Assistant client:1.  Check whether the process of the Cloud Assistant client runs properly.
    -   For Linux instances, run the following command:

        ```
ps -ef |grep aliyun-service
        ```

    -   For Windows instances, check whether the aliyun\_assist\_service process exists in the Task Manager.
2.  If the process does not exist, start the Cloud Assistant client.
    -   For Linux instances, run one of the following commands:

        ```
#If the Linux instances support systemctl, run the following command:
systemctl start aliyun.service

#If the Linux instances do not support systemctl, run the following command:
/etc/init.d/aliyun-service start
        ```

    -   For Windows instances, start AliyunService by using the Server Manager.

**Note:** If the preceding operations fail to start the Cloud Assistant client, re-install Cloud Assistant. For more information, see [Install the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Install the Cloud Assistant client.md). |
|ClientNetworkBlocked|The error message returned because the instance network environment is abnormal.|1.  Run the following command to check the network connectivity. If `ok` is returned, the network is normal.

    ```
curl https://{region-id}.axt.aliyun.com/luban/api/connection_detect
    ```

`{region-id}` specifies the region ID of the instance. For example, if the instance is in the China \(Hangzhou\) region, set this parameter to `cn-hangzhou`.

2.  If the return value indicates that the network fails, check the instance security groups, firewall, DNS configurations, and route table to troubleshoot the problem.

**Note:** You must enable TCP port 443, TCP port 80, and UDP port 53 in the outbound direction to ensure that Cloud Assistant can access https://\{region-id\}.axt.aliyun.com:443/ and http://100.100.100.200:80/ over the internal network. |
|ClientNotResponse|The error message returned because the Cloud Assistant client does not respond.|Troubleshoot the problem based on logs of the Cloud Assistant client.1.  Open the log file of the Cloud Assistant client. The following section lists the default paths of the log file:
    -   Linux instances: /usr/local/share/aliyun-assist/<Version number of Cloud Assistant\>/log/aliyun\_assist\_main.log
    -   Windows instances: C:\\ProgramData\\aliyun\\assist\\<Version number of Cloud Assistant\>\\log\\aliyun\_assist\_main.log
2.  Query whether the task ID exists in the log file.
    -   If the task ID exists, check whether exceptions exist in the context. For example, you can check whether the command execution is complete and reported.
    -   If the task ID does not exist, run the Cloud Assistant command again. If the execution fails again, we recommend that you restart the Cloud Assistant client.
        -   For Linux instances, run one of the following commands:

            ```
#If the Linux instances support systemctl, run the following command:
systemctl restart aliyun.service

#If the Linux instances do not support systemctl, run the following command:
/etc/init.d/aliyun-service restart
            ```

        -   For Windows instances, start AliyunService by using the Server Manager. |
|DeliveryTimeout|The error message returned because the Cloud Assistant server failed to send the command to the Cloud Assistant client.|If the Cloud Assistant command is not sent to the instance, we recommend that you run the command again. If the problem persists, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).|

**Related topics**  


[DescribeInvocationResults](/intl.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md)

[DescribeInvocations](/intl.en-US/API Reference/Cloud assistant/DescribeInvocations.md)

