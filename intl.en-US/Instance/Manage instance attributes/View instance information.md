---
keyword: [Alibaba Cloud, ECS, polling, view instance information before submitting a ticket]
---

# View instance information

This topic describes how to view an overview of instances and details of a single instance under your account.

## View instance resources on the Overview page

When you log on to the [ECS console](https://ecs.console.aliyun.com/#/home), the Overview page appears.

When you log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs), the Overview page appears.

On the Overview page, you can view the following information of ECS instances under your account, including:

-   **Pending Events**: lists all pending events and instances that are associated with the events.
-   **Security Score**: lists security risk information, such as unfixed vulnerabilities, unhandled alerts, and baseline risks.
-   **My Resources**: lists ECS instances and other resources in each region.

## View instance resources on the Resource Overview page

The Resource Overview page provides an overview of resources and status-based visual statistics. You can switch between **Grouped By Network Type** and **Grouped by Tag**. You can also export statistical data to view the information of all resources.

Perform the following steps to go to the Resource Overview page:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).

3.  On the Overview page, click **Resource Overview**.

    ![Click Resource Overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0101359951/p5369.png)

4.  On the Resource Overview page, view the information of all instances.

    The following table describes the dimensions of visual statistical data on the Resource Overview page.

    |Visual statistical dimension|Description|
    |----------------------------|-----------|
    |**Status**|Lists all instances that are in various states.|
    |**Instances Expiring Within 30 Days**|Lists subscription instances that will expire within 30 days. You can renew the subscription and make a budget based on the statistical data.|
    |**Billing Method**|Lists pay-as-you-go and subscription instances.|
    |**Instance Type**|Lists all instance types that have various architectures or categories. You can determine whether the current instance type arrangement is appropriate based on the statistical data. For example, if entry-level instances or entry-level burstable instances occupy a high proportion in a large enterprise, you must review whether the current arrangement can meet business requirements.|
    |**Zone**|Lists the distribution of instances in all zones of the specified region.|
    |**Instances Created Last 30 Days**|Lists the number of instances that were created during the last 30 days. You can manage the computing capacity based on the statistical data.|
    |**Instance Image Distribution**|Lists the distribution of all images. You can manage image types and versions based on the statistical data. For example, if you deploy an application on multiple instances, you need to use the same image.|


## View information of instances on the Instances page

Perform the following steps to go to the Instances page:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).

3.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

4.  In the top navigation bar, select a region.

5.  View the information of all ECS instances in the specified region, such as **Instance ID/Name**, **Zone**, **IP Address**, **Status**, **Network Type**, **Billing Method**, and **Actions**. You can use **Column Filters** to customize your columns:

    1.  In the upper-right corner of the Instances page, click the ![Icon of Column Filters](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/25441/cn_zh/1514174627852/icon_CustomizeItem.png) icon.

    2.  In the Column Filters dialog box that appears, select the instance information that you want to view and click **OK**.

        ![Select the instance information that you want to view](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0101359951/p5368.png)


## View information of a single instance on the Instance Details page

You can perform the following steps to view the information of a single instance on the Instance Details page:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).

3.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

4.  In the top navigation bar, select a region.

5.  Find the ECS instance that you want to view and click the instance ID or **Manage** in the corresponding **Actions** column.

    **Note:** The following table describes the information of an instance on the Instance Details page.

    |Information|Description|
    |-----------|-----------|
    |**Basic Information**|The information that is related to instance identification, such as instance ID, name, zone, region, instance type, instance family, image ID, and key pair name \(applicable only to Linux instances\).|
    |**Configuration Information**|The information that is related to instance configuration, such as vCPU, memory, instance type, operating system, IP address, bandwidth billing method, current bandwidth, and VPC \(applicable only to VPC instances\).|
    |**Payment Information**|The information that is related to billing, such as billing method, stop mode, creation time, and automatic release time \(applicable only to pay-as-you-go instances\).|
    |**Monitoring Information**|The information that is related to instance running, such as CPU and network usage.|


You can switch from the Instance Details page to the Disks, Snapshots, or Security Groups page to view other types of resources of the instance.

**Related topics**  


[DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md)

