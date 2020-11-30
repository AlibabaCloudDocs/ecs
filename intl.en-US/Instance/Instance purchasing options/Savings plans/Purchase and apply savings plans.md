---
keyword: [hourly commitment, savings plans, purchase a savings plan, optimize instance costs]
---

# Purchase and apply savings plans

This topic describes how to calculate and select an hourly commitment so as to purchase appropriate savings plans, and how to view the results of applying savings plans.

## Purchase savings plans

You can purchase a savings plan recommended by the system or calculate a suitable savings plan on your own based on your past consumption habits.

-   Purchase a system-recommended savings plan

    If you want to optimize the costs of your pay-as-you-go instances, you can go to the [Recommend](https://usercenter2-intl.aliyun.com/resource/spn/recommend) page for system recommendations. You need only to configure the savings plan type, duration, and payment option, and the system recommends a savings plan with an appropriate hourly commitment based on your configurations. The recommendation feature is available for ECS and ECI instances.

-   Select and purchase a savings plan on your own

    If you have not created any pay-as-you-go instances, you can calculate an hourly commitment before you purchase a savings plan on the [Savings Plan](https://common-buy-intl.alibabacloud.com/?commodityCode=savingplan_common_public_intl#/buy) page.

    For more information about how to calculate and select an appropriate hourly commitment, see the following [Select an hourly commitment for ECS instances](#section_mk3_ije_9t8) and [Select an hourly commitment for ECI instances](#section_lhc_azk_pnx) sections in this topic. The prices used in this topic are merely examples. The prices displayed on the buy page prevail.


The following table describes the attributes of savings plans.

|Attribute|Description|
|---------|-----------|
|Plan type|Savings plans come in two types:-   General purpose savings plan: automatically applied to eligible pay-as-you-go instances without limitations on regions, instance families, instance sizes, or operating systems. General purpose savings plans provide the most flexibility and can provide discounts as great as 72% off the pay-as-you-go prices.
-   ECS compute savings plan: applied only to pay-as-you-go instances of a specified instance family within a specified region regardless of instance sizes or operating systems. ECS compute savings plans are more cost effective than general purpose savings plans and can provide discounts as great as 76% off the pay-as-you-go prices. |
|Region|When you select ECS compute savings plans, you must specify a region.|
|Instance family|When you select ECS compute savings plans, you must specify an instance family.|
|Hourly commitment|The hourly usage amount to which you commit. Minimum value: USD 0.01/hour. Resource usage up to your commitment is calculated and offset based on the savings plan price. Any resource usage beyond your commitment is charged at the regular pay-as-you-go price.**Note:** When you select the hourly commitment, use the savings plan discounted price for calculation. For specific discounts, see the [Discount Details page](https://usercenter2-intl.aliyun.com/resource/spn/price). |
|Payment option|Three payment options are provided: All Upfront, Partial Upfront, and No Upfront. The All Upfront payment option provides the largest discount.|
|Duration|You can choose a duration of one or three years. A duration of three years provides the largest discount.|

## Apply savings plans

After you purchase a savings plan, the savings plan is automatically applied to your pay-as-you-go instances. For information about the application rules, see [Billing of savings plans]().

You can go to the [Saving Plan](https://usercenter2-intl.aliyun.com/resource/spn/overview) page to view the information about how your savings plans are applied, including the saving amount, plan details, usage, and coverage.

## Select an hourly commitment for ECS instances

For example, assume that John plans to purchase a three-year general purpose savings plan with the All Upfront payment option and apply the plan to the following ECS instances.

**Note:** The calculation procedures described in this example merely show how to calculate the required hourly commitment consumption. It does not mean that subsequent resource usage is limited to the listed region and instance family.

|Instance|Region|Instance type|System disk|Bandwidth|Eligible quantity|
|--------|------|-------------|-----------|---------|-----------------|
|Instance A|China \(Shanghai\)|ecs.g6.xlarge|40 GiB ESSD PL0|3 Mbit/s|15|
|Instance B|China \(Beijing\)|ecs.c5.large|40 GiB ESSD PL0|1 Mbit/s|5|

Perform the following operations to calculate an appropriate hourly commitment:

1.  Go to the [ECS Pricing page](https://www.alibabacloud.com/product/ecs) and the [Discount Details page](https://usercenter2-intl.aliyun.com/resource/spn/price) to query the regular pay-as-you-go and savings plan prices of Instance A.

    The following table lists the prices of a single instance:

    |Billable item|Pay-as-you-go price \(USD/hour\)|Savings plan discount|Savings plan price \(USD/hour\)|
    |-------------|--------------------------------|---------------------|-------------------------------|
    |ECS instance type \(computing resources\)|0.155|54.5% off|0.0705|
    |System disk|0.0064|58.8% off|0.0026|
    |Network bandwidth|0.054|57.5% off|0.0229|

    After the savings plan is applied, the total cost of Instances A is calculated based on the following formula: \(0.0705 + 0.0026 + 0.0229\) × 15 = USD 1.44/hour.

2.  Query and calculate the prices of Instance B in the same way.

    The following table lists the prices of a single instance:

    |Billable item|Pay-as-you-go price \(USD/hour\)|Savings plan discount|Savings plan price \(USD/hour\)|
    |-------------|--------------------------------|---------------------|-------------------------------|
    |ECS instance type \(computing resources\)|0.1|72.7% off|0.0273|
    |System disk|0.0064|58.8% off|0.0026|
    |Network bandwidth|0.054|57.5% off|0.0229|

    After the savings plan is applied, the total cost of Instances B is calculated based on the following formula: \(0.0273 + 0.0026 + 0.0229\) × 5 = USD 0.264/hour.

3.  Calculate an appropriate hourly commitment, which is the sum of total costs of Instances A and Instances B.

    In this example, the recommended hourly commitment is calculated based on the following formula: 1.44 + 0.264 ≈ USD 1.70/hour.


## Select an hourly commitment for ECI instances

For example, assume that William wants to optimize the costs for his ECI instances. The hourly bill of the ECI instances is USD 8. William wants to purchase a three-year general purpose savings plan with the All Upfront payment option.

1.  Go to the [Discount Details page](https://usercenter2.aliyun.com/resource/spn/price) to query the pay-as-you-go price of the ECI instances.

    In this example, the savings plan discount is 54.5% off.

2.  Calculate an appropriate hourly commitment.

    In this example, after the savings plan is applied, the hourly cost for the ECI instances is calculated based on the following formula: 8 × 0.455 = USD 3.64/hour. Therefore, when William purchases a three-year general purpose savings plan with All Upfront payment, an hourly commitment of USD 3.64/hour is recommended to offset the existing hourly bills of the ECI instances.


## References

-   [Billing of savings plans]()
-   [Billing FAQ](/intl.en-US/Pricing/Billing FAQ.md)

