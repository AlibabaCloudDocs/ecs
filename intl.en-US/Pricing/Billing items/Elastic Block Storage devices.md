---
keyword: [ECS billing, EBS billing, subscription, pay-as-you-go]
---

# Elastic Block Storage devices

This topic describes the billing methods of Elastic Block Storage \(EBS\) devices and provides examples on how to calculate their fees.

## Overview

EBS devices are classified into cloud disks and local disks. The following section describes the billing methods of EBS devices:

-   Cloud disks: Cloud disks include enhanced SSDs \(ESSDs\) and standard SSDs, and are billed based on the unit price, capacity, and duration.

    The prices of cloud disks of the same category may vary with regions. You can go to the **Pricing** tab of the [Elastic Compute Service](https://www.alibabacloud.com/product/ecs) page and click the **Storage** tab to view the prices of cloud disks in different regions.

-   Local disks: Local disks must be created together with instances and cannot be purchased separately. The prices of local disks are included in the prices of instance types.

    For information about instance families equipped with local disks, see [Instance families](/intl.en-US/Instance/Instance families.md).


## Billing methods

The following table describes the billing methods of cloud disks and the billing rule of each billing method.

|Billing method|Billing rule|Reference|
|--------------|------------|---------|
|Subscription|Price = Cloud disk capacity × Unit price of a cloud disk × Subscription duration|[Subscription](/intl.en-US/Pricing/Billing methods/Subscription.md)|
|Pay-as-you-go|Price = Cloud disk capacity × Unit price of a cloud disk × Billing duration|[Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md)|
|SCU|Storage capacity units \(SCUs\) are subscription storage resource plans that automatically match cloud disks to offset the bills of pay-as-you-go disks.|[Storage capacity units](/intl.en-US/Pricing/Billing methods/Storage capacity units.md)|

The billing methods of cloud disks depend on how they are created.

-   Cloud disks created along with an ECS instance use the same billing method as the ECS instance.
-   If a cloud disk is created for and attached to an existing subscription instance, the billing method of the cloud disk may be subscription or pay-as-you-go. If a cloud disk is created for and attached to an existing pay-as-you-go instance, the billing method of the cloud disk must be pay-as-you-go.
-   If a cloud disk is created separately and attached to an instance, the billing method of the cloud disk must be pay-as-you-go.

## Billing examples

The following table lists examples on how to calculate EBS device fees. Assume that you purchase a system disk and a data disk when you create an instance in China \(Hangzhou\).

-   System disk: a PL0 ESSD with a capacity of 50 GiB
-   Data disk: a PL1 ESSD with a capacity of 100 GiB

**Note:** The prices in the following table are for reference only and the prices on the Pricing tab of the Elastic Compute Service page shall prevail.

|Billing method|Billing condition|Price \(USD\)|
|--------------|-----------------|-------------|
|Subscription|-   System disk: The unit price of the PL0 ESSD is USD 7.65/100 GiB/month.
-   Data disk: The unit price of the PL1 ESSD is USD 15.30/100 GiB/month.
-   Subscription duration: one month.

|-   System disk: \(50/100\) × 7.65 × 1 = 3.825
-   Data disk: \(100/100\) × 15.30 × 1 = 15.30
-   Total price: 3.825 + 15.30 = 19.125 |
|Pay-as-you-go|-   System disk: The unit price of the PL0 ESSD is USD 0.0160/100 GiB/hour.
-   Data disk: The unit price of the PL1 ESSD is USD 0.0320/100 GiB/hour.
-   Billing duration: 24 hours.

|-   System disk: \(50/100\) × 0.0160 × 24 = 0.192
-   Data disk: \(100/100\) × 0.0320 × 24 = 0.768
-   Total price: 0.192 + 0.768 = 0.96 |

## References

The billing methods of cloud disks can be changed from subscription to pay-as-you-go or from pay-as-you-go to subscription. For more information, see [Change the billing method of a disk](/intl.en-US/Pricing/Change the billing method/Change the billing method of a subscription disk.md).

