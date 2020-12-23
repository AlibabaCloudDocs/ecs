# Query monitoring information of an instance

You can monitor the status of your ECS instances to ensure that your users can always access your websites and applications, process data, and render videos. Alibaba Cloud provides data monitoring, visualization of monitoring data, and real-time alerts to ensure that your ECS instances are running without interruption.

You can monitor your ECS instances by using the ECS monitoring service or Cloud Monitor. ECS provides vCPU utilization, network traffic, and disk I/O monitoring for an instance. Cloud Monitor provides finer-granularity monitoring on data. The following section describes some of the metrics provided by the two services:

-   vCPU utilization: the percentage of allocated ECS compute units that are currently used on the instance. A higher percentage indicates a higher vCPU load on an instance. You can view the vCPU utilization in the ECS console or the Cloud Monitor console. You can also obtain the monitoring data by calling the ECS API operations or connecting to the specified instance. You can use one of the following methods to view the vCPU utilization of an ECS instance after you connect to the instance:

    -   Windows instances: View the vCPU utilization in Task Manager. You can sort the tasks by vCPU utilization to find the process that is consuming vCPUs of the specified ECS instance.
    -   Linux instances: Run the top command to view the vCPU utilization. To find the process that is consuming vCPUs of the specified ECS instance, press **Shift**+**P** to sort the tasks by vCPU utilization.
    **Note:**

    -       -   -   Network traffic: the bandwidth usage for the inbound and outbound traffic of the ECS instance in Kbit/s. ECS monitors Internet traffic and Cloud Monitor monitors both Internet and internal network traffic. If the outbound traffic reaches 1,024 Kbit/s and the outbound bandwidth limit is 1 Mbit/s, the outbound bandwidth for the specified ECS instance is fully utilized.

## ECS monitoring service

To view the monitoring data in the ECS console, perform the following steps:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance that you want to monitor and click its ID.

5.  On the Instance Details page, click the **Monitoring** tab.

6.  Configure the time range of monitoring data and view the monitoring information such as vCPU utilization.

    ![Latest status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8897919951/p9888.png)

    **Note:** The specified start time and end time affect the granularity of the data displayed. Smaller sampling intervals result in finer granularity of data displayed. For example, the average values for monitoring data within one hour and six hours are different.


You can also call the ECS API operations such as DescribeInstanceMonitorData, DescribeDiskMonitorData, and DescribeEniMonitorData to query monitoring data.

The following table describes the monitoring metrics in ECS. The sampling interval for each metric is one minute.

|Metric|Description|
|:-----|:----------|
|Instance|The ID of the instance.|
|vCPUs|The percentage of allocated ECS compute units that are currently in use on the instance.|
|Internal inbound traffic|The internal network traffic to your instance. Unit: Kbit/s.|
|Internal outbound traffic|The internal network traffic from your instance. Unit: Kbit/s.|
|Internal bandwidth|The internal network traffic of the instance per unit time. Unit: Kbit/s.|
|Internet inbound traffic|The Internet traffic to the instance. Unit: Kbit/s.|
|Internet outbound traffic|The Internet traffic from the instance. Unit: Kbit/s.|
|Public bandwidth|The Internet traffic of the instance per unit time. Unit: Kbit/s.|
|Disk read IOPS|The number of disk read operations per second.|
|Disk write IOPS|The number of disk write operations per second.|
|Disk read BPS|The number of bytes read from disk per second. Unit: byte/s.|
|Disk write BPS|The number of bytes written to disk per second. Unit: byte/s.|

**Note:**

-   The following list describes differences between Kb and KB:
    -   1 byte = 8 bits \(1B = 8b\).
    -   If K or k indicates kilo, one Kb equals one thousand bits, and a kilobyte \(KB\) equals 1,024 bytes.
    -   In the ECS monitoring service, network traffic is measured in Kbit/s, which is kilobit per second. Kbit/s indicates network speed, which is the number of kilobits transmitted per second. The unit bit/s is always omitted when bandwidth is described. For example, the full form of 4 M in the bandwidth scenario is 4 Mbit/s.
-   In theory, if a network bandwidth is 1 Mbit/s, the download speed can reach 125 KB/s. Download units are converted in the following ways: 1 KB = 8 Kb, 1 Mbit/s = 125 KB/s, and 1 kbit/s = 1,000 bit/s. However, some applications running in the instance consume a small amount of bandwidth, such as remote desktop programs. Therefore, the actual download speed is typically from 100 to 110 KB/s for a 1 Mbit/s network bandwidth instead of 125 KB/s.

## Cloud Monitor

Cloud Monitor provides end-to-end and out-of-the-box monitoring solutions for enterprises in the cloud. Cloud Monitor provides you with the host monitoring service.

-   For more information about the host monitoring service, see [Overview](/intl.en-US/Host monitoring/Overview.md).
-   For more information about items and metrics related to host monitoring, see [Metrics](/intl.en-US/Host monitoring/Metrics.md).

To obtain monitoring data of an ECS instance in the Cloud Monitor console, perform the following steps:

1.  Log on to the [Cloud Monitor console](https://cloudmonitor.console.aliyun.com/).

2.  In the left-side navigation pane, click **Host Monitoring**.

3.  Find the instance that you want to monitor.

4.  If the instance is not installed with the Cloud Monitor agent, click **Click to install**.

5.  Click **Monitoring Charts** in the Actions column to obtain the monitoring data.

    **Note:** The maximum number of days for which the monitoring data can be retained is 30.

6.  Click **Alert Rules** in the Actions column to configure alert rules.


![Configure alert rules](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8897919951/p3939.png)

**Related topics**  


[DescribeInstanceMonitorData](/intl.en-US/API Reference/Operations and monitoring/DescribeInstanceMonitorData.md)

[DescribeDiskMonitorData](/intl.en-US/API Reference/Operations and monitoring/DescribeDiskMonitorData.md)

[DescribeEniMonitorData](/intl.en-US/API Reference/Operations and monitoring/DescribeEniMonitorData.md)

