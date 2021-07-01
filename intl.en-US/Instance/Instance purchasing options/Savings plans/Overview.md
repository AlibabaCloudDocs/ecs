---
keyword: [savings plans, pay-as-you-go, discount]
---

# Overview

A savings plan is a discount plan that can be applied to offset the bills of pay-as-you-go instances, excluding preemptible instances. A combination of savings plans and pay-as-you-go instances is more flexible in use than subscription instances or a combination of reserved instances and pay-as-you-go instances.

## What is a savings plan?

A savings plan is a discount plan that allows you to receive pay-as-you-go billing discounts in exchange for a commitment to use a consistent amount \(measured in USD/hour\) of resources over a one-year or three-year period. After you purchase a savings plan, the hourly bills of your pay-as-you-go instances are covered up to the amount of the plan.

When you use a savings plan, your pay-as-you-go instances of each instance type have a regular pay-as-you-go unit price and a savings plan unit price. For more information, see the [Discount Details](https://usercenter2-intl.aliyun.com/resource/spn/price) page. You are charged for resource usage within your commitment based on the savings plan unit price. You are charged for resource usage beyond your commitment at the regular pay-as-you-go unit price.

For example, Alex has several ecs.g6.xlarge instances in the China \(Shanghai\) region and can use a three-year general-purpose savings plan to obtain the following discounts.

**Note:** The prices used in this example are for demonstration only. For more information about the actual prices and discounts, see the [Pricing](https://www.alibabacloud.com/product/ecs) tab of the Elastic Compute Service page and the[Discount Details](https://usercenter2-intl.aliyun.com/resource/spn/price) page.

For example, the regular pay-as-you-go unit price of ecs.g6.xlarge instances is `USD 0.155/instance/hour`, and a three-year savings plan provides savings of `54.5%` off the pay-as-you-go price for the ecs.g6 instance family in the China \(Shanghai\) region. The savings plan unit price of the ecs.g6.xlarge instances is calculated based on the following formula: `USD 0.155/instance/hour × 0.455 = USD 0.0705/instance/hour`.

If Alex makes a commitment of `USD 0.31/hour`, the savings plan can be applied to offset the hourly bills of 4.397 pay-as-you-go ecs.g6.xlarge instances, which is calculated based on the following formula: `0.31/0.0705 = 4.397`.

The following table compares the regular pay-as-you-go prices and the savings plan prices.

|Billing method|The first hour \(based on the assumption that six instances are running\)|The second hour \(based on the assumption that five instances are running\)|The third hour \(based on the assumption that four instances are running\)|
|--------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------|--------------------------------------------------------------------------|
|Total regular pay-as-you-go price without applying the savings plan|6 × 0.155 = 0.93 USD|5 × 0.155 = 0.775 USD|4 × 0.155 = 0.62 USD|
|Total price after the savings plan is applied|You are charged for the instances that exceed the maximum number of instances \(4.397 instances\) to which the savings plan can be applied on a pay-as-you-go basis. 0.31 + 0.155 × \(6 - 0.31/0.0705\) = 0.558 USD

|You are charged for the instances that exceed the maximum number of instances \(4.397 instances\) to which the savings plan can be applied on a pay-as-you-go basis.0.31 + 0.155 × \(5 - 0.31/0.0705\) = 0.403 USD

|The total price is calculated based on the commitment because the number of running instances is less than the maximum number of instances \(4.397 instances\) to which the savings plan can be applied. 0.31 USD |

## Select an hourly commitment

For each savings plan, you must select an hourly commitment. You are charged for resource usage within your commitment based on the savings plan unit price. You are charged for resource usage beyond your commitment at the regular pay-as-you-go unit price.

You can purchase a desired savings plan on the [Savings Plan](https://common-buy-intl.alibabacloud.com/?commodityCode=savingplan_common_public_intl#/buy) page or purchase a recommended savings plan on the [Recommended](https://usercenter2-intl.aliyun.com/resource/spn/recommend) page.

## Savings plan types

Savings plans are available in two types: general-purpose and Elastic Compute Service \(ECS\) compute. The following table compares the two types of savings plans. ECS compute savings plans are less flexible but offer higher discounts than general-purpose savings plans.

|Comparison item|General-purpose|ECS compute|
|---------------|---------------|-----------|
|Use across services|Can be used across services and supports the following services and resources:-   ECS: instance computing resources \(vCPUs and memory\), system disks, and public bandwidth
-   Elastic Container Instance: instance computing resources \(vCPUs and memory\)

|Can be used only for the following ECS resources: instance computing resources \(vCPUs and memory\), system disks, and public bandwidth.|
|Region limits|Has no limits on regions.|Can be applied only within a single region.|
|Instance limits|Has no limits on instance families, instance sizes, or operating systems.|Can be applied only to specific instance families. You can choose to place an order by instance family set. In this case, this savings plan type can be applied to all instance families in the set. You can also place an order by instance family. In this case, this savings plan type can be applied only to the specified instance family. Has no limits on instance sizes or operating systems. |

## Scenarios

Both savings plans and reserved instances can be applied to offset the bills of pay-as-you-go instances. The following table describes scenarios where a combination of savings plans and pay-as-you-go instances serves as an optimal billing solution.

|Scenario|Combination of savings plans and pay-as-you-go instances|Combination of reserved instances and pay-as-you-go instances|
|--------|--------------------------------------------------------|-------------------------------------------------------------|
|You want to change the instance family of your instances for business adjustment purposes, or you want to upgrade your instances to a next-generation instance family.|Has no limits on instance sizes or operating systems. General-purpose savings plans support more services and have no limits on regions or instance families.|Does not support changes of the instance family.|
|You want to deploy your instances in multiple regions.|A reserved instance can be used only within a single region.|
|You want to make it easy to select resources in the budgeting phase.|Requires an estimate of the approximate usage range but not details about the instance family or the operating system.|Requires details about the region, instance family, and operating system.|

For more information about instance billing, see [Instance types](/intl.en-US/Pricing/Billing items/Instance types.md).

## Billing

Savings plans support three payment options: All Upfront, Partial Upfront, and No Upfront. You can receive different discounts based on the selected payment option of your savings plan. Your savings plans are automatically applied to offset the bills of your pay-as-you-go instances based on specific rules within the terms of the plans. For more information, see [Savings plans](/intl.en-US/Pricing/Billing methods/Savings plans.md).

## Lifecycle management

The following rules apply to the lifecycle management of savings plans:

-   Management process from taking effect to expiration

    When a savings plan is purchased, the savings plan immediately takes effect at the hour of purchase. Savings plans take effect and expire on the hour.

    For example, you purchased a one-year savings plan at 13:45 of May 29, 2020. The savings plan takes effect at 13:00 of May 29, 2020 and expires at 24:00 of May 30, 2021. If you have eligible pay-as-you-go instances, the savings plan is applied to offset the bills of your pay-as-you-go instances starting from 13:00 of May 29, 2020 by hour until it expires.

    **Note:** Expired savings plans cannot continue to offset the bills of pay-as-you-go instances. However, the pay-as-you-go instances are not released, which ensures that your business can continue. Make sure that you have sufficient balance within your account to ensure that the services on your pay-as-you-go instances are available.

-   Overdue payment, suspension, payment, and resumption

    If you select the Partial Upfront or No Upfront payment option and you are unable to pay your hourly commitment because you have overdue payments within your account, the overdue payment management procedure is triggered. 72 hours after a payment within your account becomes overdue, your savings plans are suspended. The discounts of your savings plans are no longer applied starting from the next hour and cannot be resumed until the overdue bills are paid.

    **Note:**

    -   If your savings plans are suspended, you are still charged by hour based on the commitment.
    -   If your savings plans are suspended multiple times or for an extended period of time, you may not be able to use the No Upfront payment option for other Alibaba Cloud services. Make sure that you have sufficient balance within your account.

## Limits

The following table describes the limits of savings plans.

|Object|Item|Description|
|------|----|-----------|
|Savings plan|Maximum number|You can purchase up to 40 savings plans for each account.|
|Order of application|When multiple discount plans take effect, they are applied in the following order:1.  Reserved instances and resource plans
2.  Savings plans
3.  Coupons
4.  Vouchers |
|ECS instance|Billing method|-   Savings plans are applicable only to pay-as-you-go instances, excluding preemptible instances.
-   Savings plans are applicable to the following resources:
    -   ECS instance computing resources \(vCPUs and memory\)
    -   System disks
    -   Public bandwidth |
|Instance family|ECS compute savings plans can be applied only to pay-as-you-go instances of a specific instance family within a specific region.|

## Use across accounts

If you want to manage the financial relationships of multiple Alibaba Cloud accounts in a centralized manner, you can use the corporate finance feature in the User Center. The corporate finance feature allows you to establish trusteeship between multiple Alibaba Cloud accounts. You can use the main account to pay bills of linked accounts. After the trusteeship is established between multiple accounts, you can share savings plans within the main account to offset the bills of pay-as-you-go instances within the linked accounts.

**Note:** In corporate finance, the main account and linked accounts are independent Alibaba Cloud accounts that are used to grant financial management permissions. The relationships between these accounts are different from those between regular Alibaba Cloud accounts and Resource Access Management \(RAM\) users.

The following limits apply to the use of savings plans across accounts:

-   Savings plans within linked accounts cannot be shared.
-   If you want to use savings plans within a linked account, the original savings plans within the linked account take priority over shared ones.

## References

-   [Savings plans](/intl.en-US/Pricing/Billing methods/Savings plans.md)
-   [Purchase and apply savings plans](/intl.en-US/Instance/Instance purchasing options/Savings plans/Purchase and apply savings plans.md)
-   [Billing FAQ](/intl.en-US/Pricing/Billing FAQ.md)

