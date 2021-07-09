---
keyword: [pay-as-you-go, billable resources, billing duration, settlement, overdue payment]
---

# Pay-as-you-go

Pay-as-you-go is a billing method that allows you to pay only for resources that you actually use. Resources can be purchased and released as needed. Pay-as-you-go resources help reduce costs by 30% to 80% compared with traditional hosts. This topic describes the billing and settlement rules for pay-as-you-go Elastic Compute Service \(ECS\) resources.

## Overview

You are billed for pay-as-you-go resources based on an hourly basis. If you have a quota agreement with Alibaba Cloud, fees are deducted when the cumulative consumption of your account exceeds the quota. You must complete the payment at least once a month.

After you create a pay-as-you-go ECS resource, you can change its configurations. For more information, see [Change the instance type of a pay-as-you-go instance](/intl.en-US/Instance/Change configurations/Change instance types/Change the instance type of a pay-as-you-go instance.md) and [Modify the bandwidth configurations of pay-as-you-go instances](/intl.en-US/Instance/Change configurations/Modify bandwidth configurations/Modify the bandwidth configurations of pay-as-you-go instances.md).

You can change the billing method of your pay-as-you-go ECS resources. For more information, see [Change the billing method of an instance from pay-as-you-go to subscription](/intl.en-US/Pricing/Change the billing method/Change the billing method of an instance from pay-as-you-go to subscription.md).

You can use one of the following methods to view your bills:

-   To view the fee calculation method, see [Billing](#section_rbk_ldg_c2b).
-   To understand how the ECS resource status affects the billing duration, see [Billing duration](#section_28d_kj8_yh8).

    **Note:** If you stop an ECS instance but do not release related resources, you continue to be charged for the resources.

-   For information about settlement, see [Settlement cycle](#section_ipb_4x2_zdb).

## Applicable resources

The pay-as-you-go billing method is available for the following ECS resources:

-   Computing resources \(vCPUs and memory\)
-   Image
-   Cloud disk
-   Public bandwidth \(pay-by-bandwidth\)
-   Snapshot

When you create an ECS instance, you must configure the computing resources \(vCPUs and memory\), Elastic Block Storage \(EBS\), image, and network type. The image and cloud disks created along with the pay-as-you-go ECS instance also use the pay-as-you-go billing method. However, you can select the billing method for network usage.

**Note:** After you create a pay-as-you-go instance, you can attach a separately created pay-as-you-go cloud disk to the instance. For more information, see [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md).

You are charged for a snapshot only after you create the snapshot.

You can view the total price of the preceding resources in the lower-left part of the instance buy page.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1890359951/p72527.png)

-   **Total** indicates the total price of the following resources:
    -   Computing resource \(vCPUs and memory\)
    -   Cloud disk
    -   Public bandwidth \(pay-by-bandwidth\)

        **Note:** If you select pay-by-traffic as the billing method for network usage, the total price does not include the price for public bandwidth. For more information, see [Public bandwidth](/intl.en-US/Pricing/Billing items/Public bandwidth.md).

-   **Marketplace Image Fees** indicates that you selected a paid Alibaba Cloud Marketplace image.

## Billing

After you create pay-as-you-go ECS resources, you are charged on their billing cycles. You are separately billed for resources. You can calculate the total fee that you must pay for a period of time based on the configurations you choose. The following table describes the billing cycle of each ECS resource and the formula used to calculate the fee of each ECS resource.

|Resource|Billing cycle|Formula|Unit price|
|--------|-------------|-------|----------|
|Computing resources \(vCPUs and memory\)|Second|Unit price of an instance type × Billing duration|For more information, see the **Instance** section on the [Pricing](https://www.alibabacloud.com/product/ecs) tab of the Elastic Compute Service page. **Note:** Local disks are tied to specific instance types. The prices of local disks are included in the prices of corresponding instance types. |
|Image|Second|Unit price of an image × Billing duration|You can view the price on the instance buy page and in Alibaba Cloud Marketplace.|
|Cloud disk \(system disk\)|Second|Unit price of a cloud disk × Disk capacity × Billing duration|For more information, see System Cloud Disk Fee of the Storage section on the [Pricing](https://www.alibabacloud.com/product/ecs) tab of the Elastic Compute Service page. **Note:** The price for a pay-as-you-go disk on the page is displayed in the USD/100 GiB/hour format. Divide the unit price by 100 to obtain the unit price per GiB. |
|Cloud disk \(data disk\)|Second|Unit price of a cloud disk × Disk capacity × Billing duration|For more information, see Data Cloud Disk Fee of the Storage section on the [Pricing](https://www.alibabacloud.com/product/ecs) tab of the Elastic Compute Service page. **Note:** The price for a pay-as-you-go disk on the page is displayed in the USD/100 GiB/hour format. Divide the unit price by 100 to obtain the unit price per GiB. |
|Public bandwidth \(pay-by-bandwidth\)|Second|Unit price of bandwidth × Bandwidth value × Billing duration For more information, see [Public bandwidth](/intl.en-US/Pricing/Billing items/Public bandwidth.md).

|A tiered billing model is used for bandwidth. You can select a bandwidth value on the buy page to view the changes in fees.|
|Snapshot|Hour|Unit price of a snapshot × Snapshot capacity × Billing duration For more information, see [Snapshots](/intl.en-US/Pricing/Billing items/Snapshots.md).

|For more information, see the **Snapshot** section on the [Pricing](https://www.alibabacloud.com/product/ecs) tab of the Elastic Compute Service page.|

**Note:**

-   If the billing cycle is 1 second, the fee generated each second is added to the bill. If an hourly price is displayed, you can divide the price by 3,600 to obtain the price per second.
-   If the billing cycle is 1 hour, the fee generated every hour is added to the bill. A usage duration of less than 1 hour is calculated as 1 hour.

For example, you created a pay-as-you-go instance in the China \(Qingdao\) region, and the resource was in use from 11:00:00 to 12:00:00 on August 8, 2019. The following figure shows the process for calculating the price of the instance.

**Note:** The price in the preceding figure is for reference only. For more information about the actual price, visit the URLs in the preceding table.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1890359951/p54836.png)

## Billing duration

If a pay-as-you-go instance is automatically stopped due to an overdue payment, the billing of the ECS resources is suspended. The billing resumes after you complete the overdue payment and reactivate the instance.

The following table describes the billing duration of each resource type on the premise that you have no overdue payments.

|Resource|Billing duration|
|--------|----------------|
|Computing resources \(vCPUs and memory\)|The billing duration of computing resources \(vCPUs and memory\) is affected by the network type of the instance: -   For an ECS instance in the classic network, the billing starts when the instance is created and stops when the instance is released.
-   For an ECS instance in a virtual private cloud \(VPC\), the billing duration depends on whether the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled.
    -   If this feature is not enabled, the billing starts when the instance is created and stops when the instance is released.
    -   If this feature is enabled, the billing starts when the instance is created and is suspended when you stop the instance by using the ECS console. The billing resumes when the instance is restarted in the ECS console and stops when the instance is released. For more information, see [No Fees for Stopped Instances \(VPC-Connected\)](/intl.en-US/Pricing/Billing methods/No Fees for Stopped Instances (VPC-Connected).md).

**Note:** If you stop the instance by shutting down its operating system, you cannot trigger the No Fees for Stopped Instances \(VPC-Connected\) feature.


 You can purchase reserved instances to reduce your costs. For more information, see [Overview](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Overview.md). |
|Image|The billing starts when the instance is created and stops when the instance is released.|
|Cloud disk \(system disk\)|The billing starts when the instance is created and stops when the instance is released.|
|Cloud disk \(data disk\)|The billing starts when the data disk is created and stops when the data disk is released.|
|Public bandwidth \(pay-by-bandwidth\)|The billing starts when public bandwidth \(pay-by-bandwidth\) is enabled and stops when public bandwidth is disabled or when the ECS instance is released. For information about how to disable public bandwidth, see [Modify the bandwidth configurations of pay-as-you-go instances](/intl.en-US/Instance/Change configurations/Modify bandwidth configurations/Modify the bandwidth configurations of pay-as-you-go instances.md). |
|Snapshot|The billing starts when the snapshot is created and stops when the snapshot is deleted.|

**Note:** If a pay-as-you-go instance incurs less than USD 0.01 in charges during its entire lifecycle, you are charged USD 0.01.

To avoid unexpected fees incurred when a pay-as-you-go instance is not released in a timely manner, we recommend that you enable the automatic release feature. If automatic release is enabled, the billing stops when the resources are released. The automatic release time is accurate to seconds.

## Settlement cycle

You are billed for pay-as-you-go resources on an hourly basis. These resource fees are paid together with the fees incurred by subscription resources within your account. If you have a quota agreement with Alibaba Cloud, fees are deducted when the cumulative consumption of your account exceeds the quota. If the cumulative monthly consumption of your account is less than the quota, fees are deducted on the first day of the following month.

-   If your default payment method is bank card, the quota is USD 1,000.
-   If your default payment method is PayPal or Paytm \(India\), the quota depends on your ECS resource usage.

Fee deduction is attempted three times: on the due date \(T\), T+7, and T+14. If fee deduction fails on the due date \(T\), the system attempts to deduct fees again on day T+7 and day T+14. If fee deduction fails all three times, the instance is stopped on day T+15 and the billing of its resources also stops.

The following changes occur on the resource status after a payment becomes overdue:

1.  Within 15 days after the payment becomes overdue, you can use existing ECS resources but cannot purchase new instances, upgrade instance configurations, or renew instances.
2.  Within 15 days after the instance is stopped, you must submit a ticket to complete the overdue payment and then reactivate the instance. Otherwise, the instance is released. For information about the resource status, see [Resource status when an ECS instance is stopped](#section_rpb_4x2_zdb).
3.  More than 15 days after the instance is stopped, the pay-as-you-go ECS resources are released.

## Resource status when an ECS instance is stopped

**Note:** If you have overdue payments within your account, your ECS instances may be stopped. The system sends you notifications about the overdue payments. We recommend that you complete the overdue payments in time to ensure your service availability. If you still have problems, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

If all three deductions for an instance fail, the instance is stopped. The following table describes the resource status after your instance is stopped due to an overdue payment.

|Resource|Within 15 days after the instance is stopped|More than 15 days after the instance is stopped|
|--------|--------------------------------------------|-----------------------------------------------|
|Computing resources \(vCPUs and memory\)|The computing resources \(vCPUs and memory\) are retained, but the instance is stopped and does not provide services. When a pay-as-you-go instance is automatically stopped due to an overdue payment, it enters the Expired state and the billing stops. After an ECS instance is stopped, you cannot connect to the instance or access websites deployed on the instance, and service errors may occur.

|The computing resources \(vCPUs and memory\) are released. **Note:** If your computing resources \(vCPUs and memory\) are released due to overdue payments, the system sends an email notification. |
|Image|The image is unavailable.|The image is unavailable.|
|Elastic Block Storage|-   Cloud disks and data stored on them are retained, but the cloud disks cannot be used.
-   Local disks and data stored on them are retained, but the local disks cannot be used.

 **Note:** After cloud disks or local disks become unusable, they cannot properly process I/O read and write requests. This affects the normal running of ECS instances to which these disks are attached, such as excessive time needed to perform operations and unpredictable power-off, or restart failures for some operating systems.

|-   Cloud disks are released and data stored on them cannot be restored.

**Note:** Cloud disks \(data disks\) created along with pay-as-you-go instances and pay-as-you-go cloud disks \(data disks\) separately created on the Disks page in the ECS console are released.

-   Local disks are released and data stored on them cannot be restored. |
|IP address|-   In the classic network: The public IP address is retained.
-   In a VPC:
    -   The public IP address is retained.
    -   The elastic IP address \(EIP\) associated with the instance remains unchanged.

|-   In the classic network: The public IP address is released.
-   In a VPC:
    -   The public IP address is released.
    -   The EIP is disassociated from the instance. |
|Snapshot|All snapshots are retained, but automatic snapshots cannot be created.|All snapshots are deleted, except for those that were used to create cloud disks or custom images.|

