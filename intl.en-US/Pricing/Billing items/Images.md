---
keyword: [ECS billing, image billing, subscription, pay-as-you-go]
---

# Images

This topic describes the billing methods of images and provides examples of how to calculate image fees.

## Overview

You may be charged for images that you use. The following table describes the billing details for different types of images.

|Type|Billing description|
|----|-------------------|
|Public image|Public images are provided by Alibaba Cloud and are billed based on the operating system.-   Windows Server: The price is subject to the instance type that you choose. The price information is displayed on the buy page when you create an instance.
-   Red Hat Enterprise Linux: The price information of the image is displayed on the buy page when you create an instance.
-   Public images that run other operating systems are free of charge. |
|Custom image|Custom images are created from instances or snapshots, or imported from your local device. The billing involves the following two parts:

-   Snapshot fee: A snapshot is automatically generated when you create a custom image. You are charged for the snapshot if you retain the custom image. The snapshot is billed based on the storage space it occupies. For more information, see [Snapshot](/intl.en-US/Pricing/Billing items/Snapshot billing.md).
-   Image fee: If you use a custom image derived from a paid image, you are still charged for the source paid image.

**Note:** If the custom image is an imported custom image of a Windows operating system, you are charged based on the system license type. If the license type is Aliyun or Auto, you are charged for the image. If the license type is BYOL, you are not charged for the image. For more information about license types, see the "What kinds of licenses can be used when I import custom images?" section in [Image FAQ](/intl.en-US/Images/Image FAQ.md).

For example, assume that Instance A is created from Paid Image A. You create a custom image from Instance A and then you create an instance from the custom image. You must pay for Paid Image A in addition to the snapshot fee. |
|Shared image|Shared images are shared with you by other Alibaba Cloud accounts. If a shared image is derived from a paid image, you are charged for the source paid image when you use the shared image.

For example, assume that you use a paid image that is shared with you by another Alibaba Cloud account to create an instance. You must pay for the source paid image. |
|Alibaba Cloud Marketplace image|Alibaba Cloud Marketplace images are provided by independent software vendors \(ISVs\). The prices are shown on the buy page of Alibaba Cloud Marketplace images.|

## Billing methods

You must select an ECS image when you create an instance. The billing method and billing cycle of the image are the same as those of the instance.

|Billing method|Billing rule|Reference|
|--------------|------------|---------|
|Subscription|The billing method of the image is the same as that of the instance. Price = Unit price of the image × Subscription duration.|[Subscription](/intl.en-US/Pricing/Billing methods/Subscription.md)|
|Pay-as-you-go|The billing method of the image is the same as that of the instance. Price = Unit price of the image × Billing duration. The billing cycle is accurate to seconds.|[Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md)|

**Note:** Images can be used only along with ECS instances. Prices of Windows reserved instances include the prices of images and Windows reserved instances can be used to offset image bills.

## Billing examples

The following table lists examples of how to calculate image fees. Assume that you purchase an image that contains the Red Hat Enterprise Linux 8.1 64-bit operating system in the China \(Hangzhou\) region.

**Note:** The prices in the following table are for reference only and the prices on the Pricing tab of Elastic Compute Service page prevails.

|Billing method|Billing condition|Price \(USD\)|
|--------------|-----------------|-------------|
|Subscription|-   Unit price of the image: USD 43.00/month
-   Subscription duration: one month

|43.00 × 1 = 43.00|
|Pay-as-you-go|-   Unit price of the image: USD 0.089/hour
-   Billing duration: one month

|0.089 × 24 × 30 = 64.08|

## References

For more information about image billing, see the "FAQ about commercial availability of images" section in [Image FAQ](/intl.en-US/Images/Image FAQ.md).

