---
keyword: [prepaid, subscription, weekly subscription, pay-as-you-go, billable resources]
---

# Billing overview

This topic describes the billing items of ECS and billing methods of ECS resources.

The price of an ECS resource may vary with regions. For more information about ECS resource prices, see the [Pricing](https://www.alibabacloud.com/product/ecs) tab on the Elastic Compute Service page.

## Billable items

An ECS instance includes the computing resources \(vCPUs and memory\), image, and Elastic Block Storage \(EBS\) devices. The following table describes the billable ECS resources.

|Resource|Description|Billing method|Reference|
|--------|-----------|--------------|---------|
|Computing resource \(vCPUs and memory\)|You are charged based on the instance type that you choose. The instance type determines the number of vCPUs and the size of memory that you can use.|-   Subscription
-   Pay-as-you-go
-   Pay-as-you-go and reserved instances
-   Preemptible instances

|[Instance types](/intl.en-US/Pricing/Billing items/Instance types.md)|
|Image|The image fees are determined based on the image type and your usage.|-   Subscription
-   Pay-as-you-go
-   Pay-as-you-go and reserved instances

|[Images](/intl.en-US/Pricing/Billing items/Images.md)|
|EBS device \(cloud disk or local disk\)|The disk fees are determined based on the disk capacity and duration of use.**Note:** Local disks must be created together with instances and cannot be purchased separately. Prices of local disks are included in those of the instances to which the local disks are attached.

|-   Subscription
-   Pay-as-you-go
-   Storage capacity units \(SCUs\)

|[Elastic Block Storage devices](/intl.en-US/Pricing/Billing items/Elastic Block Storage devices.md)|
|Public bandwidth|If you use a public IP address to access the Internet, you are charged only for the outbound public bandwidth.**Note:** You can also use an elastic IP address \(EIP\) or NAT gateway to access the Internet. For more information about the billing, see [EIP Billing](/intl.en-US/Pricing/Billing.md) or [NAT Billing](/intl.en-US/Pricing/Billing overview.md).

|-   Pay-by-bandwidth
-   Pay-by-traffic

|[Public bandwidth](/intl.en-US/Pricing/Billing items/Public bandwidth.md)|
|Snapshot|The snapshot fees are determined based on the snapshot size and storage duration.|-   Pay-as-you-go
-   SCUs

|[Snapshots](/intl.en-US/Pricing/Billing items/Snapshots.md)|

## Billing methods

ECS resources support the subscription and pay-as-you-go billing methods. You can combine different billing methods based on the ECS resource types to reduce costs. For more information, see [Billing overview](/intl.en-US/Pricing/Billing methods/Billing overview.md).

If your current billing methods cannot meet your business requirements after you purchase ECS resources, you can change the billing methods of the resources. The following table describes ECS resources whose billing methods can be changed.

|ECS resource|Description|Reference|
|------------|-----------|---------|
|ECS instance|When you change the billing method of an ECS instance, the billing method of its computing resources \(vCPU and memory\) and system disk is also changed.-   You can change the billing method of an ECS instance from subscription to pay-as-you-go. This allows you to recover some costs and use the instance in a more flexible manner.

**Note:** The availability of this feature is determined based on your ECS resource usage.

-   You can change the billing method of an ECS instance from pay-as-you-go to subscription. This allows you to obtain some discounts.

|-   [Change the billing method of an instance from subscription to pay-as-you-go](/intl.en-US/Pricing/Change the billing method/Change the billing method of an instance from subscription to pay-as-you-go.md)
-   [Change the billing method of an instance from pay-as-you-go to subscription](/intl.en-US/Pricing/Change the billing method/Change the billing method of an instance from pay-as-you-go to subscription.md) |
|Cloud disk|-   The billing method of data disks that are attached to a subscription instance can be changed separately.
-   The billing method of the system disk and data disks that are attached to a pay-as-you-go instance must be changed together with that of the instance.

|-   [Change the billing method of a disk](/intl.en-US/Pricing/Change the billing method/Change the billing method of a subscription disk.md)
-   [Change the billing method of an instance from subscription to pay-as-you-go](/intl.en-US/Pricing/Change the billing method/Change the billing method of an instance from subscription to pay-as-you-go.md)
-   [Change the billing method of an instance from pay-as-you-go to subscription](/intl.en-US/Pricing/Change the billing method/Change the billing method of an instance from pay-as-you-go to subscription.md) |
|Public bandwidth|For an instance that uses a public IP address, you can change its billing method for network usage by upgrading or downgrading the configurations of the instance.|[Change the billing method for network usage](/intl.en-US/Instance/Change configurations/Modify bandwidth configurations/Change the billing method for network usage.md)|

## Renewal management

When a subscription instance expires, the services provided by the instance may be affected. If you want to continue to use the instance, you must renew it within the specified period. Otherwise, instance resources such as vCPUs, memory, and disks are released and data stored in them is lost permanently. For more information about renewal, see [Renewal overview](/intl.en-US/Pricing/Renew instances/Renewal overview.md).

## Payment methods

You can use the following methods to pay for ECS resources:

-   Bank card
-   PayPal

    Alibaba Cloud pre-authorizes your PayPal account after your pay-as-you-go resources start to incur fees.

-   Paytm \(India\)

    Only for users in India. Alibaba Cloud pre-authorizes your Paytm account after your pay-as-you-go resources start to incur fees.


**Note:** Coupons are used to pay for your resource usage before bills are issued. No actual payments are involved.

Before you purchase ECS resources, you must bind a bank card, PayPal account, or Paytm \(India\) account to your Alibaba Cloud account. For more information, see [Add a payment method](https://www.alibabacloud.com/help/doc-detail/50517.htm) in *Account Management*.

If you want to purchase ECS resources in mainland China, you must complete real-name verification. For more information, see the *How can I complete real-name registration?* section in [Real-name registration FAQs](https://www.alibabacloud.com/help/doc-detail/52595.htm) of *Account Management*.

After you purchase and use ECS resources, you can view the bills and consumption details. For more information, see [View consumption details](/intl.en-US/Pricing/View consumption details.md).

