# Automatic snapshot policies {#concept_d35_r2w_wdb .concept}

Snapshots are the state of system data at a certain time point, and are used for data backup or image creation. You can create automatic snapshot policies to automatically take snapshots of disks. Alternatively, you can manually take snapshots of disks. The creation time of an automatic snapshot is determined by the automatic snapshot policies, whereas manually created snapshots are independent of any automatic snapshot policies you might have.

## Parameter settings {#section_yzd_gfw_wdb .section}

One account can create up to 100 automatic snapshot policies in one region. For more information about how to create automatic snapshot policies, see [create and delete an automatic snapshot policy](../../../../reseller.en-US/User Guide/Snapshots/Create and delete an automatic snapshot policy.md#). Parameters for creating automatic snapshot policies are described as follows:

-   Policy name: Name of an automatic snapshot policy, which is a string of 2−128 characters. The name must start with an uppercase or lowercase letter or a Chinese character, and can contain numbers and special characters, including periods \(.\), underscores \(\_\), and hyphens \(-\).
-   Creation time: You can create a snapshot at any of the 24 time points each day. The value ranges from 00:00 to 23:00.
-   Repeated day: You can set up to seven days of repetition day each week. The value ranges from Monday to Sunday.
-   Retention time: Number of days snapshots can be retained. The value can be 1−65,536 days or permanently, and the default value is 30 days.

## Snapshot creation time and repeated day {#section_vn5_nxz_jfb .section}

If you are an enterprise-level user, when setting the snapshot creation time and repeated day, avoid traffic peak periods based on characteristics of your own industry to avoid affecting normal service running.

**Note:** Creating snapshots may slightly degrade the disk performance and the disks may slow down temporarily.

## Snapshot retention time {#section_uxx_4xz_jfb .section}

You can set the snapshot retention time appropriately based on characteristics of your own industry and the data update cycle. The snapshot retention time is related to the number of snapshots. After the snapshot quota is reached, the earliest automatic snapshots are automatically deleted.

**Note:** Manually created snapshots are retained unless you delete them. If they are no longer needed, manually delete them.

## Costs {#section_c12_gfw_wdb .section}

Now, snapshots are free of charge.

