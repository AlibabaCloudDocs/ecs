---
keyword: [savings plans, pay-as-you-go, instance billing method, discount]
---

# Savings plans

A savings plan is a discount plan that allows you to receive pay-as-you-go billing discounts in exchange for a commitment to use a consistent amount of resources \(measured in dollars per hour\) over a one- or three-year period. After you purchase a savings plan, the hourly bills of your pay-as-you-go instances are covered up to the amount of the plan. This topic describes the billing methods and application rules of savings plans.

## Billing methods

When you purchase a savings plan, you make a commitment to use a consistent amount of resources \(measured in dollars per hour\) over a one- or three-year period. After you purchase the savings plan, hourly bills of your pay-as-you-go instances are covered up to the amount of the plan. Savings plans must be used in conjunction with pay-as-you-go instances. Savings plans cannot be used separately. For more information, see [Overview]().

Your usage commitment is made on an hourly basis. A one- or three-year commitment can be calculated based on the following formula: Hourly commitment × 24 hours × 365 days × Duration.

**Note:** When you select the hourly commitment, use the savings plan discount price for calculation. For more information about the hourly commitment, see [Purchase and apply savings plans]().

Savings plans support the following payment options:

-   All Upfront: Full payment is required upfront at purchase. No other fees are charged for the duration of the term.
-   Partial Upfront: Partial payment \(about 50% of the full amount\) is required upfront at purchase. The remainder is paid on an hourly basis for the duration of the term.
-   No Upfront: No upfront payment is required at purchase. The total fee is paid on an hourly basis for the duration of the term.

    **Note:** In different payment options, the total fee required is the same, but you can obtain different discounts. The more you pay upfront, the greater the discount you can obtain and the more pay-as-you-go bills your savings plan can offset. Whether you can use the No Upfront payment option is based on your ECS usage. If you want to use the No Upfront payment option, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).


For example, assume that you purchased a one-year savings plan with an hourly commitment of USD 0.1/hour, and the total fee is calculated based on the following formula: USD 0.1/hour × 24 hours × 365 days = USD 876. Payments based on the three payment options are made in the following ways:

-   All Upfront: The full amount of USD 876 is paid upfront at purchase.
-   Partial Upfront: 50% of the full amount, USD 438, is paid upfront at purchase. The remaining USD 438 is charged at a rate of USD 0.05/hour on an hourly basis for the duration of the term, which is one year in this case.
-   No Upfront: No upfront payment is made at purchase. The total fee is charged at a rate of USD 0.1/hour on an hourly basis for the duration of the term.

**Note:** A savings plan takes effect immediately after it is purchased. The savings plan takes effect and expires on the hour. For example, assume that you purchased a one-year savings plan at 13:45 of May 29, 2020. The savings plan takes effect at 13:00 of May 29, 2020 and expires at 24:00 of May 30, 2021. If you select the Partial Upfront or No Upfront payment option for your savings plan, the savings plan is applied to your resource usage starting on the next hour of purchase. If you select the All Upfront payment option, your resource usage on the day of purchase is free of charge. Therefore, the total fee payable when the Partial Upfront or No Upfront payment option is used is higher than that when the All Upfront payment option is used. The fee difference is the amount for the few hours from the hour of purchase till the end of the day. In addition, the All Upfront payment option provides a higher discount.

## Application rules

You can receive different discounts based on your selected payment option for your savings plans within the term. For more information, see the [Discount Details page](https://usercenter2-intl.aliyun.com/resource/spn/price).

The discount provided by a savings plan is based on the following factors:

-   The term of the savings plan

    A longer term of a savings plan provides a higher discount.

-   The payment option of the savings plan

    The discount provided by a savings plan decreases in the following order of payment options: All Upfront \> Partial Upfront \> No Upfront.

-   The instance family of the eligible instance
-   The region of the eligible instance
-   The operating system of the eligible instance

Savings plans can be applied to offset the bills of your pay-as-you-go instances based on the following rules:

-   If you have both general purpose and ECS compute savings plans, the ECS compute savings plan is applied first.
-   If your pay-as-you-go instances are billed based on a discount higher than that of your savings plans, the higher discount is applied first and the discounted charges are covered by your commitment of your savings plans.
-   If you have different types of savings plans with different discounts \(for example, you have a one-year plan and a three-year plan, or you have an All Upfront savings plan, a Partial Upfront savings plan, and a No Upfront savings plan\), the plans take effect in the order in which they were purchased.

## Examples

The following table provides examples of how savings plans apply in common scenarios. The unit prices and discounts listed in the table are only examples. For actual prices and discounts, see the ECS pricing and Discount Details pages.

|Pay-as-you-go instance|Savings plan|Hourly bill|
|----------------------|------------|-----------|
|-   Quantity: 15
-   Unit price: USD 1/hour

|-   Commitment: USD 5/hour
-   Savings plan price: USD 0.4/hour

|-   Number of eligible ECS instances: 5/0.4 = 12.5
-   Pay-as-you-go amount: \(15 - 12.5\) × 1 = USD 2.5
-   Total: 5 + 2.5 = USD 7.5 |
|-   ECS instance A
    -   Quantity: 15
    -   Unit price: USD 1/hour
-   ECS instance B
    -   Quantity: 10
    -   Unit price: USD 1.2/hour

|-   Commitment: USD 10/hour
-   Savings plan price of Instance A: USD 0.4/hour
-   Savings plan price of Instance B: USD 0.8/hour

|-   Amount applicable for Instances A: 15 × 0.4 = USD 6
-   Instances B to which the remainder of the savings plan applies: \(10 - 6\)/0.8 = 5
-   Pay-as-you-go amount: \(10 - 5\) × 1.2 = USD 6
-   Total: 10 + 6 = USD 16

**Note:** When multiple savings plans are applied to pay-as-you-go instances, the system automatically optimizes how the savings plans are applied to maximize the discount. |

## References

-   [Billing FAQ](/intl.en-US/Pricing/Billing FAQ.md)
-   [Overview]()
-   [Purchase and apply savings plans]()

