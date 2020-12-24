# Query monitoring information of an instance

You can monitor the status of your ECS instances to ensure that your users can always access your websites and applications, process data, and render videos. Alibaba Cloud provides data monitoring, visualization of monitoring data, and real-time alerts to ensure that your ECS instances are running without interruptions.

You can monitor your ECS instances by using the ECS monitoring service or Cloud Monitor. ECS provides monitoring of vCPU utilization, network traffic, and disk I/O for instances. Cloud Monitor provides finer-grained monitoring of data. The following section describes some of the monitoring metrics for ECS instances:

-   vCPU utilization: the percentage of allocated ECS compute units that are currently in use on an instance. A higher percentage indicates a higher vCPU load on the instance. You can view the vCPU utilization of an ECS instance in the ECS console or the Cloud Monitor console. You can also obtain the monitoring data by calling ECS API operations or by connecting to the instance. You can use one of the following methods to view the vCPU utilization of an ECS instance after you connect to the instance:
    -   Windows instance: View the vCPU utilization in Task Manager. You can sort the tasks by vCPU utilization to find the process that is consuming the vCPUs of the specified ECS instance.
    -   Linux instance: Run the top command to view the vCPU utilization. To find the process that is consuming the vCPUs of the specified ECS instance, press **Shift**+**P** to sort the tasks by vCPU utilization.
-   Network traffic: the bandwidth usage for the inbound and outbound traffic of the ECS instance in Kbit/s. ECS monitors Internet traffic, whereas Cloud Monitor monitors both Internet traffic and internal network traffic. If the outbound Internet traffic reaches 1,024 Kbit/s and the outbound public bandwidth is 1 Mbit/s, the outbound public bandwidth for the specified ECS instance is fully utilized.

## ECS monitoring service

To view monitoring data in the ECS console, perform the following steps.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance that you want to monitor and click its ID.

5.  On the Instance Details page, click the **Monitoring** tab.

6.  Specify the time period to query and view the monitoring data such as vCPU utilization.

    ![Latest status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8897919951/p9888.png)

    **Note:** The length of the specified time period affects the granularity of the data displayed. The longer the time period, the finer granularity of the data displayed. For example, the average values for monitoring data within 1 hour and 6 hours are different.


You can also use ECS API operations such as DescribeInstanceMonitorData, DescribeDiskMonitorData, and DescribeEniMonitorData to query monitoring data.

The following table describes the monitoring metrics in ECS. The sampling interval for each metric is 1 minute.

|Metric|Description|
|:-----|:----------|
|Instance|The ID of the instance.|
|vCPU|The percentage of allocated ECS compute units that are currently in use on the instance.|
|Inbound traffic over the internal network|The internal network traffic to your instance. Unit: Kb.|
|Outbound traffic over the internal network|The internal network traffic from your instance. Unit: Kb.|
|Internal bandwidth|The internal network traffic of the instance per unit time. Unit: Kbit/s.|
|Inbound traffic over the Internet|The Internet traffic to the instance. Unit: Kb.|
|Outbound traffic over the Internet|The Internet traffic from the instance. Unit: Kb.|
|Public bandwidth|The Internet traffic of the instance per unit time. Unit: Kbit/s.|
|System disk read IOPS|The number of read operations on the system disk per second.|
|System disk write IOPS|The number of write operations on the system disk per second.|
|System disk read BPS|The number of bytes read from the system disk per second. Unit: byte/s.|
|System disk write BPS|The number of bytes written to the system disk per second. Unit: byte/s.|

**Note:**

-   The following section describes differences between Kb and KB:
    -   1 byte = 8 bits \(1 B = 8 b\).
    -   If K or k indicates kilo, one kilobit \(Kb\) equals 1,000 bits, and a kilobyte \(KB\) equals 1,000 bytes.
    -   In the ECS monitoring service, network traffic is measured in Kbit/s, which is kilobit per second. Kbit/s indicates network speed, which is the number of kilobits transmitted per second. The unit bit/s is always omitted when bandwidth is described. For example, the full form of 4 M in the bandwidth scenario is 4 Mbit/s.
-   In theory, if a network bandwidth is 1 Mbit/s, the download speed can reach 125 KB/s. Download units are converted in the following ways: 1 KB = 8 Kb, 1 Mbit/s = 125 KB/s, and 1 kbit/s = 1,000 bit/s. However, some applications such as remote desktop programs that run on the instance consume a small amount of bandwidth. Therefore, the actual download speed is typically from 100 KB/s to 110 KB/s instead of 125 KB/s for a 1 Mbit/s network bandwidth.

## Cloud Monitor

Cloud Monitor provides end-to-end and out-of-the-box monitoring solutions for enterprises in the cloud. Cloud Monitor provides you with the host monitoring service.

-   For more information about the host monitoring service, see [Overview](/intl.en-US/Host monitoring/Overview.md).
-   For the items and metrics related to host monitoring, see [Metrics](/intl.en-US/Host monitoring/Metrics.md).

To obtain monitoring data of an ECS instance in the Cloud Monitor console, perform the following steps.

1.  Log on to the [Cloud Monitor console](https://cloudmonitor.console.aliyun.com/).

2.  In the left-side navigation pane, click **Host Monitoring**.

3.  Find the instance that you want to monitor.

4.  If the instance is not installed with the Cloud Monitor agent, click **Click to install**.

5.  To obtain the monitoring data, click **Monitoring Charts** in the Actions column.

    **Note:** Monitoring data can be retained for up to 30 days.

6.  To configure alert rules, click **Alert Rules** in the Actions column.


![Configure alert rules](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8897919951/p3939.png)

**Related topics**  


[DescribeInstanceMonitorData](/intl.en-US/API Reference/Operations and monitoring/DescribeInstanceMonitorData.md)

[DescribeDiskMonitorData](/intl.en-US/API Reference/Operations and monitoring/DescribeDiskMonitorData.md)

[DescribeEniMonitorData](/intl.en-US/API Reference/Operations and monitoring/DescribeEniMonitorData.md)

