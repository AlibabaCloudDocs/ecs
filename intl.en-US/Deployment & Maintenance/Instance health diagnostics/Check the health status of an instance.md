---
keyword: [ECS O&M, instance diagnostics, instance health, diagnose, troubleshoot]
---

# Check the health status of an instance

The instance health diagnostics feature can diagnose the system, network, and disk status of an Elastic Compute Service \(ECS\) instance. This can help you understand the health status of the instance and identify and resolve various common issues in a timely manner.

By default, the instance health diagnostics feature checks the service status of an ECS instance from outside. If you want to diagnose configurations in the instance operating system, install the Cloud Assistant client first. For more information, see [Install the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Install the Cloud Assistant client.md).

In the following scenarios, we recommend that you use the instance health diagnostics feature to check the health status of an instance and resolve the identified issues:

-   Identify and resolve issues: You can use this feature to troubleshoot issues that you encounter when you manage an instance. Example: instance startup or network connection failure.
-   Check the overall status of an instance: During daily O&M, you can use this feature to check the overall status of an instance, identify exceptions, and resolve the exceptions in a timely manner before they can affect your business.

The items that can be checked by the instance health diagnostics feature are displayed on the corresponding page. The check items fall into the following categories:

-   Instance configuration status: checks the basic configuration conditions of an instance, such as whether the instance can be properly started and managed.
-   Instance network status: checks the network conditions of an instance, such as whether exceptions exist in network links or network loading.
-   Instance disk status: checks the disk conditions of an instance, such as whether disk read and write operations are limited or whether exceptions occur while disks are being loaded.
-   Instance service status: checks the service status of an instance, such as whether an instance system check times out or whether exceptions exist in the CPUs of an instance.
-   Configurations of the instance operating system: checks whether exceptions exist in the system files or critical system processes of an instance, such as whether the CPU utilization exceeds the normal level or whether the Dynamic Host Configuration Protocol \(DHCP\) configuration is standard.
-   Billing: checks whether an instance or its associated components such as elastic IP addresses \(EIPs\) encounters billing issues. Examples: whether subscription instances expire, whether pay-as-you-go instances are stopped due to overdue payments within your account, and whether disks are unavailable for use due to overdue payments within your account.
-   Security group rules: checks whether the ports specified in security groups associated with an instance are enabled, including common ports and custom ports. You can diagnose the source address, destination port, and protocol based on your requirements.

When you use the instance health diagnostics feature, take note of the following items:

-   Instances of retired instance families do not support the instance health diagnostics feature.
-   Only one diagnostics operation can be performed on an instance at a time. The interval of two consecutive operations must be greater than 5 minutes.

## Create an instance health diagnostics task

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Use one of the following methods to create an instance health diagnostics task:

    -   Click **Diagnose** in the upper-right corner of the Instances page. In the Instance Health Diagnosis dialog box, select an instance from the drop-down list.
    -   Find the instance that you want to diagnose and choose **More** \> **Operations and Troubleshooting** \> **Diagnose Instance Health** in the **Actions** column.
    -   Find the instance that you want to diagnose and click its ID. On the Instance Details page, click the **Health Check** tab and then click **Start**.
5.  Specify the Scenario and Diagnostic Scope parameters and click **Start**.

    -   If you set Scenario to **Comprehensive Check**, the instance health diagnostics feature diagnoses the network and disk status of the instance. You can also select **Also check the operating system configurations of the ECS instance**.
    -   If you set Scenario to **Network Exception Occured**, the instance health diagnostics feature diagnoses only the network status of the instance.
    The diagnosed items are displayed in the Instance Health Diagnosis dialog box. You can click Diagnositc Item Details to view the diagnostics details and progress of each item.

    **Note:** It may take a few minutes to diagnose the items. You can check the diagnostics progress and wait for the report on the current page. You can also close the dialog box and check the diagnostics progress and report on the Health Check tab.

6.  View the diagnostics report.

    The report includes the following items:

    -   Basic information: consists of the resource ID, the report ID, and the start time of the diagnostics.
    -   Diagnostics result: If each item is normal, Passed is displayed. If exceptions are detected, the exceptional items and the corresponding solutions are displayed. You can resolve the issues based on the solutions.
    -   Report details: includes the diagnostics results of all items. The results are classified into Serious, Warning, and Passed.

## View the diagnostics history

If you want to know the historical health status of an instance, you can view the diagnostics history of the instance.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  Use one of the following methods to view the diagnostics history of one or more instances:

    -   View the diagnostics history of a single instance
        1.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
        2.  In the top navigation bar, select a region.
        3.  Find the instance whose diagnostics history you want to view and use one of the following methods to view its diagnostics history:
            -   Choose **More** \> **Operations and Troubleshooting** \> **Diagnostic History** in the **Actions** column.
            -   Click the ID of the instance to go to the Instance Details page and then click the **Health Check** tab.
    -   View the diagnostics history of all instances
        1.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **Troubleshooting**.
        2.  In the top navigation bar, select a region.
        3.  On the **Instance Health Diagnosis** tab, enter an instance ID or a report ID, and click **Search**. The corresponding diagnostics history is displayed.
    **Note:** In the diagnostics report list, you can click the ![Filter](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7222684261/p142301.png) icon to the right of the **Status** column to filter diagnostics history records by status.

3.  View the diagnostics history report of an instance or re-diagnose the instance.

    -   Click **View Report** in the **Actions** column corresponding to a report to view the report.
    -   Click **Re-diagnose** in the **Actions** column corresponding to a report to re-diagnose the instance.

