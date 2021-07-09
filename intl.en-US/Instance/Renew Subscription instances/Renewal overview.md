---
keyword: [subscription, renewal, manual renewal, auto-renewal, renewal and configuration downgrade, expiration date synchronization, billing cycle]
---

# Renewal overview

When a subscription instance expires, the services it provides may be affected. If you want to continue to use the instance, you must renew it within the specified period. Otherwise, instance resources such as vCPUs, memory, and disks are released and their stored data is lost permanently. This topic describes the renewal feature of ECS instances.

## Overview

The renewal feature is applicable only to subscription ECS instances. Pay-as-you-go instances do not need to be renewed, but you must make sure that you have sufficient balance in your linked bank card, PayPal, or Paytm \(India\) account to cover the related costs.

If you renew an instance before it expires, the instance continues to work normally and retains all of its resources. For information about the status of a subscription instance after it expires, see [Subscription](/intl.en-US/Pricing/Billing methods/Subscription.md).

The following table describes features related to the renewal of a subscription ECS instance.

|Feature|Description|Reference|
|-------|-----------|---------|
|[Manual renewal](#section_dvb_13g_rpw)|You can manually renew the instance in the ECS console at any time before the instance is automatically released.|[Manually renew an instance](/intl.en-US/Pricing/Renew instances/Manually renew an instance.md)|
|[Auto-renewal](#section_zya_ocf_0x6)|-   After the auto-renewal feature is enabled, the instance is automatically renewed before it expires. You can enable this feature for instances to reduce management costs and prevent instances from being automatically released.
-   If the auto-renewal feature is disabled, you can choose not to renew instances upon expiration. In this case, the instance is stopped upon expiration and you will receive an expiration notification only once. You can modify the renewal settings at any time before the instance is stopped.

|-   [Manually renew an instance](/intl.en-US/Pricing/Renew instances/Manually renew an instance.md)
-   [Disable auto-renewal](/intl.en-US/Pricing/Renew instances/Disable auto-renewal.md) |
|[Renewal and configuration downgrade](#section_2j3_eqq_v2s)|If current configurations of the instance exceed your requirements, you can renew the instance and downgrade its configurations within 15 days before the instance expires or after the instance expires but before the instance is automatically released.|[Downgrade the configurations of an instance during renewal](/intl.en-US/Pricing/Renew instances/Downgrade the configurations of an instance during renewal.md)|

You can use one of the following methods to renew a subscription instance during the different phases of the instance lifecycle.

![Renewal method for the International site (alibabacloud.com)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4817393061/p141318.png)

**Note:** You can enable the auto-renewal feature for a subscription instance before the instance expires. Alibaba Cloud starts to attempt to deduct the payment on the third day before the instance expires. If the deduction fails, Alibaba Cloud attempts to deduct the payment on the following days until all the allowed deduction attempts fail or the payment is deducted: the first day before the instance expires, expiration day, seventh day after the instance expires, and fifteenth day after the instance expires.

|Applicable timeframe|Renewal method|Scenario|Result|
|--------------------|--------------|--------|------|
|Before the instance expires|Manual renewal|You only renew the instance and do not change its configurations.|The new billing cycle starts from the original expiration date.|
|Auto-renewal|You only renew the instance and do not change its configurations. The renewal operation is performed by the system based on your settings to ensure your business availability.|
|Within 15 days before the instance expires|Renewal and configuration downgrade|You can renew the instance and downgrade its configurations. For example, you can downgrade the instance type, modify the public bandwidth configurations, or change the billing method of data disks.|
|After the instance expires but before the instance is automatically released|Renewal and configuration downgrade|You can renew the instance and change its configurations. For example, you can modify the public bandwidth configurations or change the billing method of data disks.|The new billing cycle starts from the day of renewal.|
|Manual renewal|You only renew the instance and do not change its configurations.|The new billing cycle starts from the day of renewal.**Note:** If you enable the auto-renewal feature for an instance, the instance remains in the Running state within 15 days after the instance expires. If you manually renew the instance during this period, the new billing cycle starts from the original expiration date. |

## Manual renewal

When you manually renew an instance, you can extend its expiration date but cannot modify its configurations. Only the base public bandwidth of the instance is renewed. The temporarily upgraded public bandwidth is not renewed.

You can manually renew an instance before it is automatically released. The following rules apply to the new billing cycle:

-   When you manually renew an instance that is in the Running state, the new billing cycle starts from the original expiration date.
-   When you manually renew an instance that has expired, the new billing cycle starts from the day of renewal.

**Note:** If the auto-renewal feature is enabled for an instance, the instance can still be running within 15 days after it expires.

You can select one of the following renewal durations when you manually renew an instance:

-   One month, two months, three months, four months, five months, six months, seven months, eight months, and nine months
-   One year

## Auto-renewal

When the auto-renewal feature is enabled for an instance, the payment is automatically deducted based on the corresponding rules. Alibaba Cloud first attempts to deduct the payment by using coupons. If you have insufficient coupons in your account, Alibaba Cloud deducts the remaining payment by using your account balance.

Before an instance expires, you can enable auto-renewal on the instance creation, Instances, or Renew page. The following table describes the available renewal durations.

|Method for enabling auto-renewal|Available renewal duration|
|--------------------------------|--------------------------|
|On the instance creation page|You cannot set the renewal duration. The auto-renewal duration is set by the system based on the subscription duration of the instance.-   When you purchase an instance for a duration of one month, two months, three months, or six months, the auto-renewal duration is one month.
-   When you purchase an instance for a duration of one year, the auto-renewal duration is one year.

**Note:** You can modify the auto-renewal duration on the Instances or Renew page. |
|On the Instances page|You can set the renewal duration to one month or one year.|
|On the Renew page|You can set the renewal duration to one month, two months, three months, six months, or one year.|

When you enable the auto-renewal feature, take note of the following items:

-   The first auto-renewal day and billing cycle are calculated based on the expiration day of the instance.
-   The auto-renewal duration is subject to the duration that you selected. For example, if you select three months, ECS renews the instance for three months each time before it expires until you disable auto-renewal.
-   If you have manually renewed an instance before the auto-renewal payment is deducted, the auto-renewal operation will not be performed during the current billing cycle.
-   If the auto-renewal deduction fails, the systemsends messages to your email address that is bound to your account. Check you email and handle the messages in a timely manner to ensure your business availability.

After auto-renewal is enabled, the instance will be automatically renewed before it expires. The following rules apply:

-   Alibaba Cloud sends an email reminder on the seventh day before the instance expires \(T-7\).
-   Alibaba Cloud deducts the payment for the next billing cycle from your bank card, PayPal, or Paytm \(India\) account on the third day before the instance expires \(T-3\). If the deduction fails, Alibaba Cloud continues to attempt to deduct the payment up to four times on the following days until all the allowed deduction attempts fail or the payment is deducted: the day before the instance expires \(T-1\), the day that the instance expires \(T\), the seventh day after the instance expires \(T+6\), and the fifteenth day after the instance expires \(T+14\).
    -   At 08:00:00 \(UTC+8\) on the deduction day, Alibaba Cloud performs auto-renewal in sequence on all ECS instances that are set to expire. This causes the actual renewal time to be between 08:00:00 \(UTC+8\) and 18:00:00 \(UTC+8\).
    -   If the payment is deducted before the fifteenth day after the instance expires \(T+14\), the next billing cycle of the instance starts on the day that the instance expires.
    -   If the instance fails to be renewed during the five preceding deduction attempts, the instance will enter the Stopped state on the sixteenth day after the instance expires \(T+15\). After the instance enters the Stopped state, you cannot log on to or connect to the instance. In this case, you must manually renew the instance. If the instance is not manually renewed within the 15 days after it enters the Stopped state, the instance is released and its data is lost permanently.

Assume that you purchased an instance at 10:00:00 on November 8, 2017. The instance has a subscription duration of one month and the auto-renewal feature is enabled for the instance. The instance is set to expire at 00:00:00 on December 9, 2017. The following figure shows the operations performed in the first auto-renewal attempt. For information about status changes after subscription resources expire, see [Subscription](/intl.en-US/Pricing/Billing methods/Subscription.md).

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2191909951/p47363.png)

## Renewal and configuration downgrade

You can renew an instance and downgrade its configurations during the following periods of time:

-   Within 15 days before the instance expires
-   After the instance expires but before the instance is automatically released

The following table describes the configurations that can be downgraded when you renew an instance.

|Item|Description|
|----|-----------|
|Instance type|You can downgrade the instance type.**Note:** When you perform renewal and configuration downgrade after an instance expires but before the instance is automatically released, you cannot change the instance type. |
|Public bandwidth|You can modify the public bandwidth configurations.-   If the instance uses the pay-by-bandwidth billing method for network usage:
    -   Downgrade the public bandwidth.
    -   Change the billing method to pay-by-traffic and set a peak value for the bandwidth.
-   If the instance uses the pay-by-traffic billing method for network usage:

Modify the peak value for the bandwidth. |
|Billing method of data disks|You can change the billing method of data disks from subscription to pay-as-you-go.|

You can select one of the following renewal durations when you renew an instance and downgrade its configurations:

-   One month, two months, three months, four months, five months, six months, seven months, eight months, and nine months
-   One year

