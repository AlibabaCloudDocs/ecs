---
keyword: [ECS billing, EBS billing, subscription, pay-as-you-go]
---

# Elastic Block Storage devices

This topic describes the billing methods of Elastic Block Storage \(EBS\) devices and provides examples of how to calculate their fees.

## Overview

EBS devices include cloud disks and local disks. EBS devices are billed based on their capacity. The prices of the EBS devices of the same category may vary with regions. For more information, see the Pricing tab on the [ECS](https://www.alibabacloud.com/product/ecs).

-   Cloud disks: Cloud disks are divided into system disks and data disks based on their purposes. Cloud disks are billed based on their categories and capacity.
-   Local disks: Local disks must be created together with instances and cannot be purchased separately. The prices of local disks are included in the prices of instance types.

    For information about instance families equipped with local disks, see [Instance families](/intl.en-US/Instance/Instance families.md).


## Billing methods

The following table describes the billing methods of cloud disks and the billing rules of each billing method.

|Billing method|Billing rule|Reference|
|--------------|------------|---------|
|Subscription|Price = Unit price of a cloud disk × Cloud disk capacity × Subscription duration

|[Subscription](/intl.en-US/Pricing/Billing methods/Subscription.md)|
|Pay-as-you-go|Price = Unit price of a cloud disk × Cloud disk capacity × Billing duration

|[Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md)|

The billing methods of cloud disks depend on how the disks are created.

-   Cloud disks created along with an ECS instance use the same billing method as the ECS instance.
-   If a cloud disk is created for and attached to an existing subscription instance, the billing method of the cloud disk may be subscription or pay-as-you-go. If a cloud disk is created for and attached to an existing pay-as-you-go instance, the billing method of the cloud disk must be pay-as-you-go.
-   If cloud disks are created independently and are not attached to instances, the billing method of these cloud disks must be pay-as-you-go.

## Billing examples

The following table lists examples of how to calculate EBS device fees. Assume that you purchase a system disk and a data disk when you create an instance in China \(Hangzhou\).

-   System disk: a standard SSD with a capacity of 50 GiB
-   Data disk: an ultra disk with a capacity of 100 GiB

**Note:** The prices in the following table are for reference only and the prices on the Pricing tab of the Elastic Compute Service page prevails.

|Billing method|Billing condition|Price \(USD\)|
|--------------|-----------------|-------------|
|Subscription|-   System disk: The unit price of the standard SSD is USD 15.30/100 GiB/month.
-   Data disk: The unit price of the ultra disk is USD 7.70/100 GiB/month.
-   Subscription duration: one month.

|\(15.30/100 × 50 + 7.70\) × 1 = 15.35|
|Pay-as-you-go|-   System disk: The unit price of the standard SSD is USD 0.03/100 GiB/hour.
-   Data disk: The unit price of the ultra disk is USD 0.02/100 GiB/hour.
-   Billing duration: 24 hours.

|\(0.03/100 × 50 + 0.02\) × 24 = 0.84|

## References

The billing methods of cloud disks can be changed from subscription to pay-as-you-go or from pay-as-you-go to subscription. For more information, see [Change the billing method of a disk](/intl.en-US/Pricing/Change the billing method/Change the billing method of a subscription disk.md)

