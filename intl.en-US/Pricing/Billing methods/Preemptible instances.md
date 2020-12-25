---
keyword: [preemptible instance, billing of ECS resources]
---

# Preemptible instances

Preemptible instances are a type of on-demand instances and are discounted compared to pay-as-you-go instances. After a preemptible instance is created, you are guaranteed a protection period to use the instance. After the period, if the market price is higher than your bid or if the resources of the instance type are insufficient, your instance is automatically released. This topic describes the billing methods and billing rules of preemptible instances.

## Billing methods

When you create a preemptible instance, you must specify a maximum price per hour to bid for a specific instance type. If your bid is higher than the current market price and the resources of the instance type are sufficient, your instance is created and charged at the current market price. Preemptible instances use the pay-as-you-go billing method. You pay for preemptible instances after you use them. Bills are calculated based on the market price and billing duration.

**Note:** The market price is only the price of the instance type. It does not include the prices of resources such as disks and public bandwidth.

-   The market price of a preemptible instance fluctuates based on changes to the supply and demand for its instance type.
-   The billing duration of a preemptible instance is the period when the instance is in service. This period lasts from the time when the instance is created to the time when the instance is released.

    You continue to be charged for a preemptible instance after it is stopped. When you no longer need a preemptible instance, we recommend that you create snapshots to back up your data and environment and then release the instance. You can purchase new preemptible instances at any time.

    When the market price exceeds your bid or when the resources of the instance are insufficient, your preemptible instance enters the To Be Recycled state. After five minutes, the instance is automatically released.


**Note:** Preemptible instances can reduce overall ECS instance costs, but have a risk of being reclaimed. You can use auto provisioning groups to alleviate the instability caused by preemptible instances being reclaimed. For more information, see [Auto Provisioning overview](/intl.en-US/Elasticity/Manage auto provisioning groups/Auto Provisioning overview.md).

## Billing rules

Preemptible instances are billed by second. The market price of a preemptible instance is an hourly price. To get the price per second, you can divide the hourly price by 3,600. During the protection period after a preemptible instance is created, the instance is billed at the market price at the time of purchase. After the protection period ends, the instance is billed based on the real-time market price.

## Billing example

Assume that you purchase a preemptible instance at 8:00 with a bid of USD 2 per hour. After the protection period ends, the instance is released at 10:00 because the market price is higher than your bid. The following table describes how to calculate the fee of the preemptible instance.

**Note:** The market price varies with changes to supply and demand of instance types. The following table is only for reference.

|Time|Market price \(USD/hour\)|Billing factor|Total fee \(USD\)|
|----|-------------------------|--------------|-----------------|
|8:00|1.5|/|/|
|8:30|2.5|-   Market price: USD 1.5/hour
-   Duration: 30 minutes

|1.5 / 60 × 30 = 0.75|
|9:00|1.8|-   Market price: USD 1.5/hour
-   Duration: 30 minutes

|0.75 + 1.5 / 60 × 30 = 1.5|
|9:30|1.6|-   Market price: USD 1.8/hour
-   Duration: 30 minutes

|1.5 + 1.8 / 60 × 30 = 2.4|
|10:00|3|-   Market price: USD 1.6/hour
-   Duration: 30 minutes

|2.4 + 1.6 / 60 × 30 =3.2|

## References

-   [Overview](/intl.en-US/Instance/Instance purchasing options/Preemptible instances/Overview.md)
-   [View bills of a preemptible instance](/intl.en-US/Instance/Instance purchasing options/Preemptible instances/View bills of a preemptible instance.md)

