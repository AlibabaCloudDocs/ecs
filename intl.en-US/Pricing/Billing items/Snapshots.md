---
keyword: [snapshot, storage plan, pay-as-you-go, snapshot fee, snapshot billing]
---

# Snapshots

This topic describes the billing methods and billing rules of ECS snapshots, and how to manage overdue payments. This topic also provides an example of how to calculate a snapshot fee.

## Billable items

A snapshot is a backup of data on a disk at a specific point in time. Snapshots are often used for disaster recovery and environment clone. The following table describes the billable items of snapshots.

|Billable item|Description|Billing method|
|-------------|-----------|--------------|
|Snapshot type|Normal snapshot|Normal snapshots have disaster recovery capabilities and are stored in OSS buckets that are in the same region as the snapshots. However, an extended period of time is required to create a normal snapshot.|Pay-as-you-goThe pay-as-you-go bills of normal snapshots can be offset by storage capacity units \(SCUs\). |
|Local snapshot|Local snapshots are stored in the same storage cluster as the disks for which the snapshots are created. Local snapshots can be used to back up data and roll back disks within seconds. Local snapshots can be created only for enhanced SSDs \(ESSDs\).|Pay-as-you-go|
|Snapshot service|Snapshot replication|When a normal snapshot is copied from one region to the destination, a copy of the normal snapshot is created in the destination region.|Pay-as-you-go|
|Instant access|A snapshot becomes available for use within seconds after it starts to be created. Then, you can use the snapshot to create disks or roll back the original disk when the snapshot is being created. This feature is applicable only to ESSDs.|Pay-as-you-go ①|

① You are charged for the instant access feature on a pay-as-you-go basis. The billable items are the number of times that the feature is enabled and the snapshot size. For more information, see the [Billing rules](#section_ah7_xox_o55) section in this topic.

## Billing methods

You are charged based on the snapshot size and storage duration. By default, the pay-as-you-go billing method is used for ECS snapshots. To reduce costs, you can use SCUs to offset bills of snapshots. You are charged from the time a snapshot is created until the time the snapshot is released.

|Billing method|Description|Reference|
|--------------|-----------|---------|
|Pay-as-you-go|A billing method that allows you to pay for a resource after you use the resource. The snapshot fee is calculated based on the billing cycle of an hour. A bill is generated at the end of each billing cycle, and the fee is deducted from your account.|[Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md)|
|SCU|A subscription resource plan that can be used to offset the bills of multiple pay-as-you-go storage resources, such as disks, OSS buckets, NAS file systems, and snapshots. After you purchase an SCU, the SCU is automatically used to offset the subsequent bills generated for pay-as-you-go snapshots.|[SCU billing methods](/intl.en-US/Pricing/Billing methods/SCU billing methods.md)|

## Billing rules

|Billable item|Billing rule|
|-------------|------------|
|Storage fees for normal and local snapshots|Snapshots are billed every hour based on the storage capacity occupied by the snapshots.

Snapshot fee = Snapshot unit price ② × Snapshot size × Billing duration. The following section describes the billing rules of each item in the formula:

-   Snapshot unit price is measured in USD/GiB/month. You can calculate the hourly snapshot unit price based on this monthly unit price.
-   Snapshot size is measured in GiB. You have a free storage quota of 5 GiB each month.

The first snapshot of a disk is a full snapshot. Subsequent snapshots of the disk are incremental snapshots. Each incremental snapshot consists only of the data changes since the last snapshot. For more information, see [Incremental snapshots](/intl.en-US/Snapshots/Incremental snapshots.md).

-   Billing duration is measured in hours.

You are charged from the time a snapshot is created until the time the snapshot is released. A storage duration of less than one hour is calculated as one hour. |
|Service fees for snapshots replication|Service fees for snapshots replication = Service unit price for snapshot replication ② × Snapshot size**Note:** For information about the storage fees of snapshot copies, see the "Storage fees for normal and local snapshots" item in this table. |
|Service fee for instant access|The service fee for instant access involves the feature usage fee and the storage fee of snapshots.

-   The feature usage fee is billed based on the number of times that the feature is enabled ②.
-   The storage fee of snapshots: Storage unit price for the instant access feature ② × Snapshot size × Billing duration
    -   Storage unit price for the instant access feature is measured in USD/GiB/month. You can calculate the snapshot unit price per second based on this monthly unit price.
    -   Snapshot size is measured in GiB.
    -   Billing duration is measured in seconds. You are charged from the time the instant access feature is enabled until the time the feature is disabled.

**Note:** After instant access is disabled, you are still charged storage fee for normal snapshots. For more information, see the "Storage fees for normal and local snapshots" item in this table. |

② For details about snapshot unit prices, see snapshot price list. To view snapshot prices in different regions, go to the [Elastic Compute Service](https://www.alibabacloud.com/product/ecs) page and click the **Pricing** tab. Then, select a region and click the **Snapshot** tab.

## Example of calculating normal snapshot fees

**Note:** The following example is for reference only. To check your snapshot bills, in the left-side navigation pane of the Billing Management console, click Spending Summary \> Spending Summary to go to the Bills page.

For example, assume that you have three disks in the China \(Hangzhou\) region in your account. You created a snapshot for each disk at 10:20 in a day. The snapshots are 50 GiB, 220 GiB, and 40 GiB in size. If you do not delete these snapshots on that day, the fees of the three snapshots are determined based on the following calculations:

-   Billing conditions
    -   Snapshot size: 50 GiB + 220 GiB + 40 GiB = 310 GiB.

        If you did not use the 5 GiB free storage quota of the current month, the billed snapshot size is 305 GiB.

    -   Snapshot unit price: Assume that the pay-as-you-go price for snapshots in the China \(Hangzhou\) region is USD 0.0200/GiB/month, which is equivalent to USD 0.0000277778/GiB/hour.
    -   Billing duration: The period from 10:20 to 11:00 is calculated as an hour. A total of 13 hours is calculated until 23:00 when a bill is generated.
-   Billing calculation

    Snapshot fee = Snapshot unit price × Snapshot size × Billing duration. That is, 305 GiB × USD 0.0000277778/GiB/hour × 13 = USD 0.008472.

    -   The actual payable amount shown on the billing page is USD 0.008.
    -   The generated bill records the amount of USD 0.0085.

## Overdue payments

If your account balance in the current billing cycle is less than the payable amount of the previous billing cycle, the system sends you an SMS or email notification.

The snapshot service is suspended 24 hours after your account payments become overdue. After your account has overdue payments:

-   In the first 15 days, snapshots that exceed the retention periods are deleted, and other snapshots are retained.
-   After 15 days, all snapshots are deleted except for those that have been used to create disks or custom images. The automatic snapshot policy is also deleted.

## References

-   [Snapshot overview](/intl.en-US/Snapshots/Snapshot overview.md)
-   [Reduce snapshot fees](/intl.en-US/Snapshots/Use snapshots/Reduce snapshot fees.md)
-   [Snapshot FAQ](/intl.en-US/Snapshots/Snapshot FAQ.md)

