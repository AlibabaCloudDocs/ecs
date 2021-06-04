---
keyword: [pay-as-you-go, no fees for stopped instances, computing resources, public IP address, retain and bill, stop mode]
---

# No Fees for Stopped Instances \(VPC-Connected\)

If the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled and the prerequisites described in this topic are met, some Elastic Compute Service \(ECS\) resources are recycled and their billing stops. This helps reduce maintenance costs. The billing stops only for some resources of the ECS instances.

## Prerequisites

The No Fees for Stopped Instances \(VPC-Connected\) feature is applicable to instances that meet the following requirements:

-   The network type of the instances is VPC.
-   The instances are pay-as-you-go or preemptible instances.

    You can change the billing method of an instance from subscription to pay-as-you-go. For more information, see [Change the billing method of an instance from subscription to pay-as-you-go](/intl.en-US/Pricing/Change the billing method/Change the billing method of an instance from subscription to pay-as-you-go.md).

-   The instance families are not equipped with local disks.

    Instance families equipped with local disks do not support No Fees for Stopped Instances \(VPC-Connected\), such as big data instance families and instance families with local SSDs. For more information, see the Local storage \(GiB\) column in [Instance families](/intl.en-US/Instance/Instance families.md).

-   The instance families are not equipped with persistent memory.

    Instance families equipped with persistent memory do not support No Fees for Stopped Instances \(VPC-Connected\), such as re6p and re6p-redis. For more information, see the Persistent memory \(GiB\) column in [Instance families](/intl.en-US/Instance/Instance families.md).


By default, the No Fees for Stopped Instances \(VPC-Connected\) feature is disabled. For information about how to enable this feature, see the [Enable the No Fees for Stopped Instances \(VPC-Connected\) feature](#default) section.

## Applicable resources

This feature recycles some resources while retaining ECS instances to reduce overall costs.

-   The No Fees for Stopped Instances \(VPC-Connected\) feature is applicable to the following resources:
    -   Computing resources \(vCPUs and memory\)
    -   Public IP addresses and bandwidth
-   The No Fees for Stopped Instances \(VPC-Connected\) feature is not applicable to some ECS resources. The following list provides some examples of these resources:
    -   System disks
    -   Data disks attached to ECS instances
    -   Elastic IP addresses \(EIPs\) and bandwidth
    -   Images
    -   Snapshots

## Trigger conditions

After the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled, the feature is triggered for a VPC-type pay-as-you-go instance only when the instance is stopped due to one of the following reasons:

-   Operations in the ECS console. For more information, see [Stop an instance](/intl.en-US/Instance/Manage instances/Stop an instance.md).
-   API requests initiated by using Alibaba Cloud CLI or SDKs. For more information, see [StopInstance](/intl.en-US/API Reference/Instances/StopInstance.md).
-   Overdue payments.

**Note:** If you stop an instance from within the operating system, the No Fees for Stopped Instances \(VPC-Connected\) feature is not triggered.

If an instance is in the start period, the No Fees for Stopped Instances \(VPC-Connected\) feature cannot be triggered. The start period is the amount of time it takes for a new instance that is started for the first time to enter the Running state from the Stopped state. For more information, see [ECS instance lifecycle](/intl.en-US/Instance/ECS instance lifecycle.md).

## Impacts

After the No Fees for Stopped Instances \(VPC-Connected\) feature is triggered for an ECS instance, the computing resources \(vCPUs and memory\) and public IP address of the instance are recycled. You are no longer charged for these resources. However, the following risks exist:

-   After the computing resources \(vCPUs and memory\) are recycled, the instance may fail to be restarted due to insufficient resources. In this case, you can try again later or switch to another instance type. For more information, see [Change the instance type of a pay-as-you-go instance](/intl.en-US/Instance/Change configurations/Change instance types/Change the instance type of a pay-as-you-go instance.md).

    **Note:** We recommend that you restart the instance in advance to ensure that resources are sufficient to start the instance. This can avoid service interruptions caused by instance start failures.

-   After the public IP address is recycled, the public IP address may change when the instance is restarted. However, the private IP address remains unchanged.

    **Note:** If your application depends on a specific public IP address, we recommend that you disable the No Fees for Stopped Instances \(VPC-Connected\) feature or convert the public IP address to an EIP. For more information, see [Disable the No Fees for Stopped Instances \(VPC-Connected\) feature](#section_4h6_utd_2yr) or [Convert the public IP address of a VPC-type instance to an Elastic IP address](/intl.en-US/Network/Change IPv4 addresses/Convert the public IP address of a VPC-type instance to an Elastic IP address.md).

-   If the instance is a burstable instance, the instance stops earning CPU credits and its current CPU credit balance is cleared. After you restart the burstable instance, the instance starts to earn CPU credits again. For more information about CPU credits of burstable instances, see [CPU credits](/intl.en-US/Instance/Instance type families/Burstable instance types/Overview.md).

In some cases, you may need to restart your instances multiple times within a short period of time. We recommend that you disable the No Fees for Stopped Instances \(VPC-Connected\) feature to ensure that the instances can be restarted and provide services. You can disable this feature in the following scenarios:

-   [Replace the system disk](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace the system disk (public images).md) \([ReplaceSystemDisk](/intl.en-US/API Reference/Disk/ReplaceSystemDisk.md)\)
-   [Roll back a disk by using a snapshot](/intl.en-US/Block Storage/Cloud disks/Roll back a disk by using a snapshot.md) \([ResetDisk](/intl.en-US/API Reference/Disk/ResetDisk.md)\)
-   [Re-initialize a system disk](/intl.en-US/Block Storage/Cloud disks/Reinitialize a cloud disk/Re-initialize a system disk.md) \([ReInitDisk](/intl.en-US/API Reference/Disk/ReInitDisk.md)\)

For an instance that is stopped due to an overdue payment, if you clear the overdue payment within the specified period of time and reactivate the instance, whether the public IP address is retained is determined by the status of the No Fees for Stopped Instances \(VPC-Connected\) feature.

-   If the feature is enabled, the instance enters the No Fees for Stopped Instances \(VPC-Connected\) state when the instance is stopped due to an overdue payment. The computing resources \(vCPUs and memory\) and public IP address of the instance are automatically released and the public IP address may change when the instance is reactivated.
-   If the feature is disabled, the billing of the instance stops when the instance is stopped due to an overdue payment. The public IP address is retained and does not change when the instance is reactivated.

**Note:** If all three deductions for an instance fail, the instance is stopped. For information about the status changes of resources whose payments are overdue, see [Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md).

## Enable the No Fees for Stopped Instances \(VPC-Connected\) feature

By default, the No Fees for Stopped Instances \(VPU-Connected\) feature is disabled to avoid unexpected impacts on your applications. Enable the No Fees for Stopped Instances \(VPC-Connected\) feature after you make sure that it is suitable for your applications. For more information, see [Impacts](/intl.en-US/Pricing/Billing methods/No Fees for Stopped Instances (VPC-Connected).md).

This section describes how to enable the No Fees for Stopped Instances \(VPC-Connected\) feature for all applicable instances within your account. After this feature is enabled, the instances enter the No Fees for Stopped Instances \(VPC-Connected\) state when they are stopped. For more information, see [Prerequisites](/intl.en-US/Pricing/Billing methods/No Fees for Stopped Instances (VPC-Connected).md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the **Common Features** section of the **Overview** page, click **Custom Settings**.

    ![No Fees for Stopped Instances (VPC-Connected)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5091909951/p87545.png)

3.  Turn on **No Fees for Stopped Instances \(VPC-Connected\)**.

4.  In the message that appears, read the note and click **OK**.

5.  Click **OK**.


## Disable the No Fees for Stopped Instances \(VPC-Connected\) feature

This section describes how to disable the No Fees for Stopped Instances \(VPC-Connected\) feature for all applicable instances within your account. After this feature is disabled, the instances do not enter the No Fees for Stopped Instances \(VPC-Connected\) state when they are stopped.

If an instance is in the No Fees for Stopped Instances \(VPC-Connected\) state, its computing resources \(vCPUs and memory\) and public IP address are already recycled. Therefore, after the No Fees for Stopped Instances \(VPC-Connected\) feature is disabled, you are not charged for the computing resources \(vCPUs and memory\) until these resources are reassigned when the instance is restarted. The status of the IP address is subject to the type of the IP address.

-   If the instance uses a public IP address before it is stopped, a new public IP address is assigned to the instance.
-   If the instance is associated with an EIP before it is stopped, the EIP remains unchanged.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the **Common Features** section of the **Overview** page, click **Custom Settings**.

    ![No Fees for Stopped Instances (VPC-Connected)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5091909951/p87545.png)

3.  Turn off **No Fees for Stopped Instances \(VPC-Connected\)**.

4.  In the message that appears, read the note and click **OK**.

5.  Click **OK**.


## Configure a single instance to enter the No Fees for Stopped Instances \(VPC-Connected\) state when it is stopped

You can configure the stop mode when you stop a single instance regardless of whether the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled. For more information, see [Stop an instance](/intl.en-US/Instance/Manage instances/Stop an instance.md).

-   If you select **Retain Instance and Continue Charging After Instance Is Stopped**, the instance enters the Keep Instances and Continue Billing state.
-   If you select **No Charges After Instance Is Stopped**, the instance enters the No Fees for Stopped Instances \(VPC-Connected\) state.

![No Charges After Instance Is Stopped](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6091909951/p52884.png)

## View the stop mode

After a pay-as-you-go instance is stopped, you can view the stop mode of the instance in the ECS console to check whether the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled.

On the Instances page, click the **Column Filters** icon and select **Stop Mode** to view the stop mode of the stopped instance.

![Stop mode of the pay-as-you-go instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1747172261/p240720.png)

## References

You can also use the scheduled startup and shutdown feature of Operation Orchestration Service \(OOS\) to automatically manage the startup and shutdown time of multiple ECS instances. You can combine this feature with the No Fees for Stopped Instances \(VPC-Connected\) feature to reduce costs. For more information, see [Scheduled startup and shutdown]().

