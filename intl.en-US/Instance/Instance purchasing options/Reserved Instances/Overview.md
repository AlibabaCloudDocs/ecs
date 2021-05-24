# Overview

A reserved instance is a discount coupon that can be automatically applied to one or more pay-as-you-go instances, excluding preemptible instances. A reserved instance can also be used to reserve instance resources. A combination of reserved instances and pay-as-you-go instances provides similar cost-effectiveness to subscription instances but a higher degree of flexibility.



## Comparison between reserved instances, pay-as-you-go instances, and subscription instances

The following table describes the differences between reserved instances, pay-as-you-go instances, and subscription instances.

|Item|Reserved instance|Pay-as-you-go instance|Subscription instance|
|----|-----------------|----------------------|---------------------|
|Form|A discount coupon. Reserved instances are classified into regional and zonal reserved instances.|An instance that uses the pay-as-you-go billing method. A pay-as-you-go instance is equivalent to a virtual machine. For more information, see [Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md).|An instance that uses the subscription billing method. A subscription instance is equivalent to a virtual machine. For more information, see [Subscription](/intl.en-US/Pricing/Billing methods/Subscription.md).|
|Purpose|Reserved instances cannot be independently used. They must match pay-as-you-go instances to offset bills.|Pay-as-you-go instances can be independently used. They can be used as simple web servers, or used in combination with other Alibaba Cloud services to deliver powerful solutions.|Subscription instances can be independently used. They can be used as simple web servers, or used in combination with other Alibaba Cloud services to deliver powerful solutions.|

## Scenarios

The following table describes some scenarios where a combination of reserved instances and pay-as-you-go instances is the optimal solution.

|Scenario|Combination of reserved instances and pay-as-you-go instances|Pay-as-you-go instance|Subscription instance|
|--------|-------------------------------------------------------------|----------------------|---------------------|
|You may need to change the region for your business. You must release Elastic Compute Service \(ECS\) instances in the original zone and create ECS instances in the zones of the destination region.|A combination of reserved instances and pay-as-you-go instances has the following benefits: -   After you purchase reserved instances, you make commitments to using pay-as-you-go instances for a period of time. Reserved instances provide significant discounts compared with pay-as-you-go pricing.
-   Reserved instances that you purchase deliver computing power instead of instances. Reserved instances can match pay-as-you-go instances that meet the matching requirements, and are more flexible than subscription instances.
-   You can split or merge reserved instances to offset the bills of pay-as-you-go instances of different instance types.
-   You can modify the zone of a reserved instance anytime. A regional reserved instance can be used to offset the bills of pay-as-you-go instances across zones.
-   You can pay by hour by selecting the Partial Upfront or No Upfront payment option to avoid financial pressure caused by one-time payment.

|The unit prices of pay-as-you-go instances are higher than those of subscription instances. Pay-as-you-go instances may fail to be created if resources are insufficient. However, pay-as-you-go instances are easier to manage. For example, after you configure automated O&M, instances are automatically created and released. No manual refunds are involved after the instances are released. Pay-as-you-go instances can be used together with Auto Scaling.|Bills are associated with subscription instances. You may need to pay service fees when you apply for refunds.|
|During automated O&M, the number of subscription instances needs to be automatically adjusted.|Refunds must be manually implemented.|
|You use Auto Scaling to manage ECS instances and have a large number of pay-as-you-go instances. You want to lower your costs.|You must manually change pay-as-you instances to subscription instances. This process is inefficient and prone to errors.|
|You want to simplify the operations of managing the lifecycle of subscription instances, such as renewing, releasing, and synchronizing the expiration dates of subscription instances.|You must perform a large number of operations.|
|You want to pay for resources by installments to mitigate financial pressure.|The unit prices are lower. However, one-time payment is required.|

## Attributes

The following figure shows the key attributes of a reserved instance.

![Key attributes of a reserved instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7890359951/p112054.png)

The following table describes the key attributes of the preceding reserved instance.

|Section|Attribute|Description|
|-------|---------|-----------|
|①|Instance type|The following instance families support reserved instances: -   General purpose instance families: g7, g6e, g6, g5, g5ne, and sn2ne
-   Compute optimized instance families: c7, c6e, c6, c5, ic5, and sn1ne
-   Memory optimized instance families: r7, r6e, r6, r5, re6, re4, and se1ne
-   Big data instance family: d2s
-   Instance families with local SSDs: i2 and i2g
-   Instance families with high clock speeds: hfc6, hfc5, hfg6, hfg5, and hfr6
-   GPU-accelerated compute optimized instance families: gn6i, gn6e, and gn6v
-   ECS Bare Metal Instance families: ebmc6, ebmg6, ebmr6, ebmhfc6, ebmhfg6, and ebmhfr6
-   Burstable instance families: t6 and t5 |
|②|Region and zone|You need only to specify a region for a regional reserved instance. Regional reserved instances provide zone flexibility and instance size flexibility. You must specify a region and a zone for a zonal reserved instance. Resource reservation is supported. The matching conditions are determined by the type of a reserved instance. For more information, see [Match between reserved instances and pay-as-you-go instances](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Match between reserved instances and pay-as-you-go instances.md). You can modify the region and zone of a reserved instance after you purchase it. For more information, see [Modify a reserved instance](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Modify a reserved instance.md). |
|③|Operating system|Reserved instances are classified into Linux and Windows reserved instances. Windows reserved instances can be used to offset the image bills of Windows pay-as-you-go instances.|
|④|Normalization factor|A normalization factor indicates the performance level of an instance type and also the computing power. Normalization factors are determined by the number of vCPUs. For information about detailed specifications, see [View normalization factors](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/View normalization factors.md).|
|⑤|Instance quantity|The instance quantity is used for the following purposes: -   Calculates the computing power of reserved instances.
-   Specifies the number of reserved resources for zonal reserved instances. For example, in the preceding figure, the instance quantity is two and the instance type in use is ecs.r6e.xlarge. This indicates that two pay-as-you-go instances of the ecs.r6e.xlarge instance type are reserved. |
|⑥|Computing power|Reserved instances deliver computing power in advance. Pay-as-you-go instances consume the computing power. Computing power of a reserved instance = Normalization factor of an instance type × Instance quantity. The computing power is used for the following purposes:

-   Evaluates whether the computing power is the same before and after you split or merge reserved instances.
-   Evaluates the usage of a reserved instance when the size of a regional reserved instance is different from that of the matched pay-as-you-go instance. |
|⑦|Term|You must specify the term when you purchase a reserved instance. After you split, merge, and modify reserved instances, the terms of the original and new reserved instances are also changed. For more information, see [Split a reserved instance](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Split a reserved instance.md), [Merge reserved instances](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Merge reserved instances.md), and [Modify a reserved instance](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Modify a reserved instance.md). **Note:** You cannot shorten the term of a reserved instance to deliver more computing power.

A reserved instance takes effect and expires on the hour. For example, you purchased a reserved instance with a term of one year at 13:45 of May 29, 2020. The reserved instance takes effect at 13:00 of May 29, 2020 and expires at 24:00 of May 30, 2021. If you have pay-as-you-go instances that match the reserved instance, the reserved instance is applied to offset the bills of the matching pay-as-you-go instances from 13:00 of May 29, 2020 by hour until it expires.

Expired reserved instances cannot continue to offset the bills of pay-as-you-go instances. However, the pay-as-you-go instances are not released. This ensures continuity of your service.

**Note:** Make sure that your account balance is sufficient to ensure service availability of your pay-as-you-go instances. |

## Limits

|Limited object|Item|Description|
|--------------|----|-----------|
|Reserved instance|Maximum number of reserved instances|The maximum number of reserved instances is subject to the type of reserved instances. -   Maximum number of regional reserved instances: Each account can have up to 20 regional reserved instances across all regions.
-   Maximum number of zonal reserved instances: Each account can have up to 20 zonal reserved instances in each zone.

For example, you can purchase 10 regional reserved instances in the China \(Hangzhou\) region and 10 regional reserved instances in the China \(Qingdao\) region, but the total number of regional reserved instances cannot exceed 20. You can purchase 20 zonal reserved instances in Hangzhou Zone B and 20 zonal reserved instances in Hangzhou Zone H.

If you need more reserved instances, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm). |
|ECS instance|Billing method|-   Reserved instances can be used to match only pay-as-you-go instances. Reserved instances cannot be used to match preemptible instances.
-   Reserved instances can be used to offset the bills for compute resources of pay-as-you-go instances. They cannot be used to offset the bills for network and storage resources of pay-as-you-go instances. |
|Instance family|The gn6i and t5 instance families support only zonal reserved instances, not regional reserved instances. gn6i and t5 reserved instances cannot be split or merged.|

## Billing

Reserved instances support the All Upfront, Partial Upfront, and No Upfront payment options. Billing standards vary with payment options. For more information, see [Reserved instances](/intl.en-US/Pricing/Billing methods/Reserved instances.md).

**Note:** Your ECS usage determines whether you can use the No Upfront payment option. If you want to use the No Upfront payment option, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

## References

-   [Match between reserved instances and pay-as-you-go instances](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Match between reserved instances and pay-as-you-go instances.md)
-   [Purchase reserved instances](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Purchase reserved instances.md)
-   [Split a reserved instance](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Split a reserved instance.md)
-   [Merge reserved instances](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Merge reserved instances.md)
-   [Modify a reserved instance](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Modify a reserved instance.md)
-   [Instance FAQ](/intl.en-US/Instance/Instance FAQ.md)

