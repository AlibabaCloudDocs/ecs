---
keyword: [savings plans, pay-as-you-go, discount]
---

# Overview

A savings plan is a discount plan that can be applied to offset the bills of pay-as-you-go instances \(excluding preemptible instances\). A combination of savings plans and pay-as-you-go instances is more flexible in use than subscription instances or a combination of reserved instances and pay-as-you-go instances.

## Introduction

A savings plan is a discount plan that allows you to receive pay-as-you-go billing discounts in exchange for a commitment to use a consistent amount \(measured in dollars per hour\) of resources over a one- or three-year period. After you purchase a savings plan, the hourly bills of your pay-as-you-go instances are covered up to the amount of the plan.

When you use a savings plan, your pay-as-you-go instances of each instance type have a regular pay-as-you-go price and a savings plan price. Resource usage within your commitment is charged at the savings plan price. Any resource usage beyond your commitment is charged at the regular pay-as-you-go price.

For example, the regular pay-as-you-go price of Instance A is USD 2/hour, and the savings plan price is USD 0.5/hour. You have 25 running Instances A and make a commitment of USD 10/hour. Your hourly bills are calculated based on the following formula: 10 + 2 × \(25 - 10/0.5\) = USD 20. Comparatively, if you do not purchase a savings plan, your hourly bills are 2 × 25 = USD 50.

**Note:** The prices used in this example are for demonstration only. For the actual prices, see the [ECS pricing](https://www.alibabacloud.com/product/ecs) and [Discount details](https://usercenter2.aliyun.com/resource/spn/price) pages.

## Plan types

Savings plans are available in two types: general purpose and ECS compute. The following table compares the two types of savings plans. ECS compute savings plans are less flexible but offer higher discounts than general purpose savings plans.

|Comparison item|General purpose|ECS compute|
|---------------|---------------|-----------|
|Use across services|Can be used across services and supports the following services and resources:-   ECS: instance computing resource \(vCPUs and memory\). system disks, and public bandwidth
-   Elastic Container Instance \(ECI\): instance computing resources \(vCPUs and memory\)

|Can be used for only the following ECS resources: instance computing resources \(vCPUs and memory\), system disks, and public bandwidth|
|Region limits|Has no limits on regions|Can be applied only within a single region|
|Instance limits|Has no limits on instance families, instance sizes, or operating systems|Can be applied only to one instance family at a time but has no limits on the instance sizes or operating systems|

## Scenarios

Both savings plans and reserved instances can be applied to offset the bills of pay-as-you-go instances. The following table describes scenarios where a combination of savings plans and pay-as-you-go instances serves as an optimal billing solution.

|Scenario|Combination of savings plans and pay-as-you-go instances|Combination of reserved instances and pay-as-you-go instances|
|--------|--------------------------------------------------------|-------------------------------------------------------------|
|You need to change the instance family of your instances for business adjustment purposes or you want to upgrade your instances to a next-generation instance family.|Has no limits on instance sizes or operating systems. General purpose savings plans support more services and have no limits on regions or instance families.|Does not support changes of the instance family.|
|You want to deploy your instances in multiple regions.|A reserved instance can be used only within a single region.|
|You want to make it simple to select resources in the budgeting phase.|Requires an estimate of the approximate usage range but not details about the instance family or operating system.|Requires details about the region, instance family, and operating system.|

For more information about instance billing, see [Instances](/intl.en-US/Pricing/Billing items/Instances.md).

## Billing

Savings plans support three payment options: All Upfront, Partial Upfront, and No Upfront. You can receive different discounts based on the selected payment option of your savings plan. Your savings plans are automatically applied to the usage of your pay-as-you-go instances based on specific rules within the terms of the plans. For more information, see [Billing of savings plans]().

## Lifecycle management

The following rules apply to the lifecycle management of savings plans:

-   Taking effect and expiration

    When a savings plan is purchased, the savings plan immediately takes effect on the hour of purchase. Savings plans take effect and expire on the hour.

    For example, assume that you purchased a one-year savings plan at 13:45 of May 29, 2020. The savings plan takes effect at 13:00 of May 29, 2020 and expires at 24:00 of May 30, 2021. If you have eligible pay-as-you-go instances, the savings plan is applied to offset the bills of your pay-as-you-go instances starting from 13:00 of May 29, 2020 by hour until it expires.

    **Note:** Expired savings plans cannot continue to offset the bills of pay-as-you-go instances. However, the pay-as-you-go instances are not released, which ensures that your business can continue. Make sure that your account balance is sufficient to ensure that the services on your pay-as-you-go instances are available.

-   Overdue payment, suspension, payment, and resumption

    If you select the Partial Upfront or No Upfront payment option and you are unable to pay your hourly commitment because you have overdue payments in your account, the overdue payment management procedure is triggered. 72 hours after a payment in your account becomes overdue, your savings plans are suspended. The discounts of your savings plans are no longer applied from the next hour and do not resume until the overdue bills are paid.

    **Note:** If your savings plans are suspended, only the discounts of your savings plans are not applied. Pay-as-you-go bills are still generated on an hourly basis.


## Limits

The following table describes the limits of savings plans.

|Limited object|Limited item|Description|
|--------------|------------|-----------|
|Savings plan|Maximum number|You can purchase up to 40 savings plans for each account.|
|Eligible instance|Savings plans cannot be applied to retired Generation I instance families, which include t1, s1, s2, s3, m1, m2, c1, and c2.|
|Order of application|When multiple discount plans take effect, they are applied in the following order:1.  Reserved instances and resource plans
2.  Savings plans
3.  Coupons
4.  Vouchers |
|ECS instance|Billing method|-   Savings plans are applicable to only pay-as-you-go instances \(excluding preemptible instances\).
-   Savings plans are applicable to the following resources:
    -   ECS instance computing resources \(vCPUs and memory\)
    -   System disks
    -   Public bandwidth |
|Instance family|ECS compute savings plans can be applied to only pay-as-you-go instances of compute optimized instance families within a specific region.|

## Use across accounts

If you want to centralize the financial relationships of multiple Alibaba Cloud accounts, you can use the corporate finance feature in the User Center. The corporate finance feature allows you to establish trusteeship between multiple Alibaba Cloud accounts. You can use the main account to pay bills of linked accounts. After a trusteeship is established between multiple accounts, you can share savings plans in the main account to offset bills of pay-as-you-go instances in the linked accounts.

**Note:** In corporate finance, the main account and linked accounts are independent Alibaba Cloud accounts that are used to grant financial management permissions. The relationships between these accounts are different from that between regular Alibaba Cloud accounts and RAM users.

The following limits apply to the use of savings plans across accounts:

-   Savings plans in linked accounts cannot be shared.
-   If a linked account wants to use savings plans, its own savings plans take a higher priority than shared ones.

## References

-   [Billing of savings plans]()
-   [t1950747.md\#]()
-   [Instance FAQ](/intl.en-US/Instance/ECS instance FAQ.md)

