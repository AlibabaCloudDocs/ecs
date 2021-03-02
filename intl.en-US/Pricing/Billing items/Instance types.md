---
keyword: [ECS billing, instance billing, subscription, pay-as-you-go]
---

# Instance types

The billing of instance types refers to the billing of computing resources \(vCPUs and memory\). This topic describes the billing methods of instance types, comparison of these billing methods, and how to choose billing methods based on scenarios.

## Overview

Instance types are billed based on computing resources, including vCPUs and memory. Prices of an instance type may vary with regions. For more information, see the[Pricing](https://www.alibabacloud.com/product/ecs) tab on the Elastic Compute Service page.

**Note:** If you select an instance type that is equipped with local disks, the price of the instance type includes that of local disks.

## Billing methods

The following table describes the billing methods of instance types.

|Billing method|Description|Reference|
|--------------|-----------|---------|
|Subscription|A billing method that allows you to use instance types only after you pay for them. Price = Unit price of an instance type × Subscription duration.

|[Subscription](/intl.en-US/Pricing/Billing methods/Subscription.md)|
|Pay-as-you-go|A billing method that allows you to use instance types before you pay for them. Price = Unit price of an instance type × Billing duration. The billing cycle is accurate to seconds.

|[Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md)|
|Preemptible instance|Preemptible instances are on-demand instances that you can use before you pay. Compared with pay-as-you-go instances, preemptible instances offer more discounts. Preemptible instances are charged based on the actual usage duration, and their prices fluctuate based on the changes to supply and demand.|[Preemptible instances](/intl.en-US/Pricing/Billing methods/Preemptible instances.md)|
|Reserved instance|Reserved instances are coupons that must be used together with pay-as-you-go instances. Compared with pay-as-you-go instances, reserved instances offer some discounts. Prices of reserved instances are determined based on the region, instance type, operating system, payment option, term, and instance quantity. Reserved instances are used to offset bills of pay-as-you-go instances based on the resources that you specified when you purchased the reserved instances. Reserved instances are applied only when they match pay-as-you-go instances.

|[Reserved instances](/intl.en-US/Pricing/Billing methods/Reserved instances.md)|
|Savings plan|Savings plans are discount plans that are used together with pay-as-you-go instances and allow you to receive pay-as-you-go billing discounts in exchange for a committed consumption amount. Prices of savings plans are determined based on the committed hourly consumption, payment option, and subscription duration. After you purchase savings plans, the pay-as-you-go billing discounts that you can obtain are determined based on the selected savings plan type, payment option, subscription duration, and attributes of matched pay-as-you-go instances such as regions and instance types. Savings plans are used to offset bills of pay-as-you-go instances based on the committed consumption amount without limits on regions and instance families.|[Savings plans](/intl.en-US/Pricing/Billing methods/Savings plans.md)|

**Note:** You can purchase reserved instances and savings plans at the same time. Reserved instances are preferred to offset bills of pay-as-you-go instances over savings plans.

## Comparison of billing methods

The following table describes the comparison of billing methods.

|Comparison item|Subscription|Pay-as-you-go|Preemptible instance|Reserved instance|Savings plan|
|---------------|------------|-------------|--------------------|-----------------|------------|
|Usage|All operations are linked to the purchased instance.|All operations are linked to the purchased instance.|All operations are linked to the purchased instance.|Resources are decoupled from bills. Reserved instances must be used together with pay-as-you-go instances.|Resources are decoupled from bills. Savings plans must be used together with pay-as-you-go instances.|
|Payment option|You make a full payment for instance types before you use them.|You pay for instance types after you use them. The instance types are charged by second and billed by hour.|You pay for instance types after you use them. The instance types are charged by second and billed by hour.|You can choose All Upfront, Partial Upfront, or No Upfront.|You can choose All Upfront, Partial Upfront, or No Upfront.|
|Feature of price|Subscription instances are more cost-effective than pay-as-you-go instances.|Pay-as-you-go instances are the least cost-effective.|Prices of preemptible instances fluctuate based on the changes to supply and demand. The discounts can be up to 90% of pay-as-you-go prices.|Compared with pay-as-you-go instances, reserved instances offer some discounts. The discounted prices are close to those of subscription instances.|Compared with pay-as-you-go instances, savings plans are more flexible, but more expensive.|
|Instance release|You can manually release instances or they can be released by the system. If you want to release an instance before it expires, you must cancel the subscription of the instance or change its billing method to pay-as-you-go. If you do not renew an instance within the required period of time after it expires, the instance is automatically released.|You can release instances at any time.|You can manually release instances or they can be released by the system. Preemptible instances can be reclaimed and may be automatically released after the protection period ends.|Reserved instances must be used together with pay-as-you-go instances. Pay-as-you-go instances that match reserved instances can be released at any time. After the pay-as-you-go instances are released, the reserved instances can be used to match and offset bills of new pay-as-you-go instances.|Savings plans must be used together with pay-as-you-go instances. Pay-as-you-go instances that match savings plans can be released at any time. After the pay-as-you-go instances are released, the savings plans can be used to match and offset bills of new pay-as-you-go instances.|
|Scenario|Subscription instances are applicable to services that run for 24 hours a day and 7 days a week, such as web services and databases.|Pay-as-you-go instances are applicable to services that experience traffic spikes, such as temporary scaling, interim testing, and scientific computing.|Preemptible instances are applicable to services that experience traffic spikes, such as temporary scaling, interim testing, and scientific computing.|Reserved instances are used to match and offset bills of pay-as-you-go instances, and applicable to web services and databases.|Savings plans are used to match and offset bills of pay-as-you-go instances, and applicable to web services and databases.|

You can choose appropriate billing methods for ECS instances on which different applications are deployed to reduce costs. The following figure shows the recommended combinations of billing methods.

![Combination of billing methods](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8227393061/p167017.png)

For stable business loads, you can use the subscription billing method and reserved instances or savings plans to obtain some discounts. When ECS instances have the same subscription duration, savings plans are the most flexible, and reserved instances are more flexible than subscription. The following table describes the comparison between subscription, reserved instances, and savings plans.

|Feature|Subscription|Reserved instance|Savings plan|
|-------|------------|-----------------|------------|
|Discount limits|Discounts are offered only for a single instance.|A reserved instance can match a maximum of 100 pay-as-you-go instances to offer discounts.|Savings plans are used to offset bills without limits on the number of instances. Savings plans are flexible.|
|Resource reservation|Supported.|Supported. You must use zonal reserved instances.|Not supported.|
|Use across services|Not supported.|Supported. Reserved instances can be used in ECS and Elastic Container Instance \(ECI\).|Supported. Savings plans can be used in ECS and ECI.|
|Use across regions|Not supported.|Not supported.|Supported. General-purpose savings plans can be used across regions.|
|Use across zones in the same region|Not supported.|Supported. You must use regional reserved instances.|Supported.|
|Use across instance families|Not supported.|Not supported.|Supported. General-purpose savings plans can be used across instance families.|
|Use across instance types in the same instance family|Not supported.|Supported.|Supported.|
|Use across operating systems|Not supported.|Not supported.|Supported.|
|Use across accounts \(based on the established trusteeship\)|Not supported.|Supported.|Supported.|
|Installment|Not supported.|Supported. You can choose All Upfront, Partial Upfront, or No Upfront.|Supported. You can choose All Upfront, Partial Upfront, or No Upfront.|

## Examples of typical scenarios

The following figure shows some typical scenarios to which you can refer to choose appropriate billing methods.

![Scenarios of instance billing](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4227393061/p171036.png)

|Business type|Linked pattern|Stable pattern|Burstable pattern|Hybrid pattern|
|-------------|--------------|--------------|-----------------|--------------|
|Business characteristic|All businesses are closely linked. When traffic loads of one business increase, traffic loads of other businesses also increase.|Business loads are stable with no obvious peak hours or off-peak hours.|All businesses are loosely linked. Business loads may become burstable at some points in time.|Multiple businesses exist. Each business has a unique requirement for computing power during a specific time period. The businesses have different priorities.|
|Example scenario|Hot issues, e-commerce promotions, and traffic spikes of IoT|Stable online businesses, such as office automation \(OA\) systems|Event-based tasks, job tasks, and simulation tasks|Scenarios where online, offline, and job tasks are deployed in a hybrid manner and where multiple environments are used alternately, such as blue-green deployment|
|Recommended billing method|Pay-as-you-go and savings plans \(or reserved instances\).|-   Subscription.
-   Pay-as-you-go and savings plans \(or reserved instances\).

|Pay-as-you-go.You can combine the pay-as-you-go billing method with savings plans or reserved instances if traffic bursts frequently.

|Pay-as-you-go and savings plans \(or reserved instances\).|

## References

You can change the billing method of an instance from subscription to pay-as-you-go or from pay-as-you-go to subscription.

-   For information about how to change a billing method from subscription to pay-as-you-go, see [Change the billing method of an instance from subscription to pay-as-you-go](/intl.en-US/Pricing/Change the billing method/Change the billing method of an instance from subscription to pay-as-you-go.md).
-   For information about how to change a billing method from pay-as-you-go to subscription, see [Change the billing method of an instance from pay-as-you-go to subscription](/intl.en-US/Pricing/Change the billing method/Change the billing method of an instance from pay-as-you-go to subscription.md).

