# Use Cloud Monitor to monitor ECS instances

Cloud Monitor helps greatly reduce the O&M costs and workloads of cloud services. The ECS monitoring service of Cloud Monitor provides real-time operation data that you can use to identify risks in advance, avoid potential loss, and troubleshoot problems.

Before you begin, perform the following operations:

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   Make sure that the Cloud Monitor agents are running on the ECS instances to be monitored and are able to collect metric data. If the Cloud Monitor agent is not installed, manually install it. For more information, see [Install the Cloud Monitor Java agent]().
-   Add alert contacts and contact groups. We recommend that you add at least two contacts to ensure real-time responses to monitoring alerts. For more information about metrics, see [Delete an alert contact or alert group](/intl.en-US/Alarm service/Alert contacts/Delete an alert contact or alert group.md) and [Overview](/intl.en-US/Quick Start/Overview.md).

The dashboard feature of Cloud Monitor provides you with system-wide visibility into resource utilization and operational health. In this topic, the CPU utilization, memory usage, and disk usage of ECS instances are separately displayed and the four metrics of ApsaraDB RDS instances are displayed in two groups.

![Dashboard metrics](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5134798161/p73804.png)

In this example, a website is used to describe how to configure Cloud Monitor. ECS, ApsaraDB RDS, OSS, and SLB instances are used.

![Architecture](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5414488951/p12496.png)

## Configure alert thresholds and alert rules

We recommend that you configure alert thresholds based on your business requirements. A low threshold may lead to frequent alerts and affect user experience. A high threshold may leave you with insufficient time to respond to events.

For example, to reserve some processing capacity to ensure the normal operation of the system, you can set the alert threshold for CPU utilization to 70% and trigger an alert when the threshold is exceeded three consecutive times, as shown in the following figure.

![Configure an alert threshold for CPU utilization](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8314658161/p73788.png)

If you need to configure alert rules for other metrics, click **Add Alarm Rule**. Examples:

-   Configure monitoring for ApsaraDB RDS instances

    We recommend that you configure the alert threshold for CPU utilization of ApsaraDB RDS instances to 70% and trigger an alert when the threshold is exceeded three consecutive times. You can configure the disk utilization, IOPS utilization, total number of connections and other metrics based on your requirements. For more information about how to view the information about monitoring items, see [Cloud service monitoring](/intl.en-US/.md).

    ![Configure monitoring for ApsaraDB RDS instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8314658161/p73789.png)

-   Configure monitoring for SLB instances

    Before you begin, make sure that health check is enabled for your SLB instance. Then, configure the alert threshold to 70% of the bandwidth value of SLB instances, as shown in the following figure.

    ![Configure monitoring for SLB instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8314658161/p73791.png)


## Configure process monitoring

For web applications, you can configure process monitoring to monitor application processes in real time, and use monitoring data to troubleshoot problems. For more information, see [Process monitoring](/intl.en-US/Host monitoring/Process monitoring.md).

## Configure site monitoring

Site monitoring is an external monitoring service, and is used to simulate real user access conditions and test the business availability in real time. The monitoring data can also be used to troubleshoot problems.

![Configure site monitoring](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8314658161/p37762.png)

If the preceding monitoring options do not meet your needs, you can use the custom monitoring feature. For more information, see [Overview](/intl.en-US/Custom monitoring/Overview.md).

