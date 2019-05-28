# Billing method comparison {#billingMethod_china .concept}

This article describes the pricing, billing methods, and payment methods of an ECS instance.

## Pricing {#section_ssd_kz2_zdb .section}

The price of an ECS instance varies according to the following:

-   Instance type, including the memory capacity and the number of CPU cores.
-   Region: The price for the same instance type varies in different regions.
-   Image: Windows images are more expensive than Linux or UNIX images for the same instance type in the same region because Microsoft charges an additional license fee for Windows images.

For more information, see Pricing.

## Billing methods {#section_usd_kz2_zdb .section}

Currently, ECS instances support two billing methods:

-   Subscription

    A prepaid method that allows you to use an instance only after you make the payment for it. Instance usage is billed on a monthly basis, and the billing unit is USD/month. Subscription is applicable to fixed 24/7 services, such as Web services. For more information, see [Subscription](reseller.en-US/Pricing/Subscription.md#).

-   Pay-As-You-Go

    A postpaid method in which you can pay after using the instance. Instance usage is billed on a minute basis, and the billing unit is US$/hour. The minimum charge for the lifecycle of an ECS instance \(from creation to release\) is USD 0.01. Pay-As-You-Go is applicable to scenarios where sudden traffic spikes occur, such as temporary scaling, interim testing, and scientific computing. For more information, see [Pay-As-You-Go](reseller.en-US/Pricing/Pay-As-You-Go.md#).


## Functions {#section_wsd_kz2_zdb .section}

The functions of an ECS instance vary depending on the billing method. The following table lists the differences between Subscription and Pay-As-You-Go billing.

|Function|Subscription|Pay-As-You-Go|
|:-------|:-----------|:------------|
|Renew|Supported. You can [manually renew](reseller.en-US/Pricing/Renew instances/Manual renewal.md#), [activate auto-renewal](reseller.en-US/Pricing/Renew instances/Auto-renewal.md#), or [renew for downgrade](reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#) for your ECS instance.|Not supported.|
|Release instances at any time|Not supported. The instance will be automatically released if it is not renewed within the grace period after the instance expires.|Supported. If you do not need an instance any longer, [release it](../../../../reseller.en-US/User Guide/Instances/Release an instance.md#) immediately. Otherwise, the instance is still billed even after it is stopped until it is out of service and automatically released because of overdue payment. You can enable the [No fees for stopped instances \(VPC-Connected\)](reseller.en-US/Pricing/No fees for stopped instances (VPC-Connected).md#) feature.|
|Change instance specification|Supported. For more information, see [Overview of configuration changes](../../../../reseller.en-US/User Guide/Instances/Change configurations/Overview of configuration changes.md#).|Supported.|
|Upgrade bandwidth|Supported. For more information, see [Overview of configuration changes](../../../../reseller.en-US/User Guide/Instances/Change configurations/Overview of configuration changes.md#).|Supported.|
|Change billing method|Not supported.|Supported. You can switch from Pay-As-You-Go to Subscription. For more information, see [Switch from Pay-As-You-Go to subscription](reseller.en-US/Pricing/Limits.md#).|
|ICP Filing for instances in regions inside mainland China|Supported.|Not supported.|
|Use API to create instances|Supported.|Supported.|

## Payment methods {#section_arq_j2x_kfb .section}

Credits are used to pay for the resources of the Subscription billing method.

