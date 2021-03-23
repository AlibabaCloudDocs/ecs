---
keyword: [snapshot, storage plan, pay-as-you-go, snapshot fee, snapshot billing]
---

# Snapshots

This topic describes the billing methods and billing rules of ECS snapshots, and how to manage overdue payments. This topic also provides an example of how to calculate a snapshot fee.

## Billable items

A snapshot is a backup of data on a disk at a specific point in time. Typically, snapshots are used for disaster recovery and environment clone. The following table describes the billable items of snapshots.

|Billable item|Description|Billing method|
|-------------|-----------|--------------|
|Snapshot|Snapshots have disaster recovery capabilities and are stored in OSS buckets that are in the same region as the snapshots. However, an extended period of time is required to create a snapshot.|Pay-as-you-goThe pay-as-you-go bills of snapshots can be offset by storage capacity units \(SCUs\). |
|Snapshot replication|When a snapshot is copied from one region to another, a copy of the snapshot is created in the destination region.|Pay-as-you-go|
|Instant access|A snapshot becomes available for use within seconds after it is created. This feature is applicable only to enhanced SSDs \(ESSDs\).|Pay-as-you-go|

You are charged for the instant access feature on a pay-as-you-go basis. The billing is based on the number of times that the feature is enabled and the snapshot size. For more information, see the [Billing rules](#section_ah7_xox_o55) section in this topic.

## Billing methods

You are charged based on the snapshot size and storage duration. By default, the pay-as-you-go billing method is used. To reduce costs, you can use SCUs to offset the bills of snapshots. You are charged from the time when a snapshot is created to the time when the snapshot is released.

|Billing method|Description|Reference|
|--------------|-----------|---------|
|Pay-as-you-go|A billing method that allows you to pay for a resource after you use the resource. The snapshot fee is calculated based on the billing cycle of an hour. A bill is generated at the end of each billing cycle, and the fee is deducted from your account.|[Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md)|
|SCU|A subscription resource plan that can be used to offset the bills of multiple pay-as-you-go storage resources, such as disks, OSS buckets, NAS file systems, and snapshots. After you purchase an SCU, the SCU is automatically used to offset the subsequent bills generated for pay-as-you-go snapshots.|[Storage capacity units](/intl.en-US/Pricing/Billing methods/Storage capacity units.md)|

## Billing rules

|Billable item|Billing rule|
|-------------|------------|
|Storage fees for snapshots|Snapshots are billed every hour based on the storage capacity occupied by the snapshots.

Snapshot fees = Snapshot unit price × Snapshot size × Billing duration. The following section describes the billing rules of each item in the formula:

-   The snapshot unit price is measured in USD/GiB/month. You can calculate the hourly snapshot unit price based on this monthly unit price.
-   The snapshot size is measured in GiB. You have a free storage quota of 5 GiB each month.

The first snapshot of a disk is a full snapshot. Subsequent snapshots of the disk are incremental snapshots. Each incremental snapshot consists only of the data changes since the last snapshot. For more information, see [Incremental snapshots](/intl.en-US/Snapshots/Incremental snapshots.md).

-   The billing duration is measured in hours.

You are charged from the time when a snapshot is created to the time when the snapshot is released. A storage duration of less than one hour is calculated as one hour. |
|Service fees for snapshot replication|Service fees for snapshot replication = Service unit price for snapshot replication ② × Snapshot size**Note:** For information about the storage fees of snapshot copies, see the "Storage fees for snapshots" item in this table. |
|Service fees for instant access|Service fees for instant access include the feature usage fee and the storage fee of snapshots.

-   The feature usage fee is billed based on the number of times that the feature is enabled.
-   Storage fees for snapshots = Storage unit price for instant access × Snapshot size × Billing duration.
    -   The storage unit price for instant access is measured in USD/GiB/month. You can calculate the snapshot unit price per second based on this monthly unit price.
    -   The snapshot size is measured in GiB.
    -   The billing duration is measured in seconds. You are charged from the time when the instant access feature is enabled to the time when the feature is disabled.

**Note:** After instant access is disabled, you are still charged storage fees for snapshots. For more information, see the "Storage fees for snapshots" item in this table. |

② For information about the prices of snapshots, copying snapshots, and instant access, see the snapshot price list. To view snapshot prices in different regions, go to the [Elastic Compute Service](https://www.alibabacloud.com/product/ecs) page and click the **Pricing** tab. Then, select a region and click the **Snapshot** tab.

## Example of calculating snapshot fees

**Note:** The following example is for reference only. To check your actual snapshot bills, go to the Billing Management console.

For example, if you have three disks in the China \(Hangzhou\) region that belongs to your account. You created a snapshot for each disk at 10:20. The snapshots are 50 GiB, 220 GiB, and 40 GiB in size. If you do not delete these snapshots on the same day, the fees of the three snapshots are determined based on the following calculations:

-   Billing conditions
    -   Snapshot size: 50 GiB + 220 GiB + 40 GiB = 310 GiB.

        If you have not used the 5 GiB free storage quota of this month, the billed snapshot size is 305 GiB.

    -   Snapshot unit price: Assume that the pay-as-you-go price for snapshots in the China \(Hangzhou\) region is USD 0.0200/GiB/month, which is equivalent to USD 0.0000277778/GiB/hour.
    -   Billing duration: The period from 10:20 to 11:00 is calculated as an hour. A total of 13 hours is calculated until 23:00 when a bill is generated.
-   Billing calculation

    Snapshot fee = Snapshot unit price × Snapshot size × Billing duration. 305 GiB × USD 0.0000277778/GiB/hour × 13 = USD 0.008472.

    -   The actual payable amount shown on the billing page is USD 0.008.
    -   The generated bill shows the amount of USD 0.0085.

## Overdue payments

If your account balance in the current billing cycle is less than the payable amount of the previous billing cycle, the system sends you an SMS or email notification. The snapshot service is suspended 24 hours after payments become overdue within your account.

The following section describes how snapshots are retained from the day when the payment becomes overdue:

-   In the first 15 days, snapshots that exceed the retention periods are deleted, and other snapshots are retained.
-   After 15 days, all snapshots are deleted except for those that have been used to create disks or custom images. The automatic snapshot policy is also deleted.

## References

-   [Snapshot overview](/intl.en-US/Snapshots/Snapshot overview.md)
-   [Reduce snapshot fees](/intl.en-US/Snapshots/Use snapshots/Reduce snapshot fees.md)
-   [Snapshot FAQ](/intl.en-US/Snapshots/Snapshot FAQ.md)

