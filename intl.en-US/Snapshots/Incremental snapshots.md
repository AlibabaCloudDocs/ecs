---
keyword: [ecs, backup, Alibaba Cloud, data backup, disaster recovery]
---

# Incremental snapshots

Snapshots are used to back up the data of disks at one or more points in time. Snapshots ensure service security and make application deployment more efficient.

## Principles

After a disk is formatted, it is divided into multiple data blocks based on logical block addresses \(LBAs\). When new data is written to the data blocks, every modified data block is marked to be copied at the next snapshot. The first snapshot created for a disk is a full snapshot. A full snapshot does not include empty data blocks of the disk. For example, if the capacity of a disk is 200 GiB and 122 GiB is in use, the first snapshot of the disk is 122 GiB in size. All subsequent snapshots created for the disk are incremental snapshots. Each incremental snapshot includes only the business data that has changed since the last snapshot. Therefore, snapshots can contain the same data blocks, but the data on the data blocks may be different. The following figure illustrates how incremental snapshots work. Snapshots 1, 2, and 3 represent the first, second, and third snapshot of a disk.

![Principles](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8565319951/p5243.jpg)

Before a snapshot is created for a disk, the file system checks all the data blocks on the disk, and only data blocks whose data is modified are copied to the snapshot.

-   Snapshot 1 contains all the data on the disk at the point in time when the snapshot is created.
-   Snapshot 2 contains only Data Blocks B1 and C1, whose data has changed since Snapshot 1. Data Blocks A and D are referenced from Snapshot 1.
-   Snapshot 3 contains only Data Block B2 whose data has changed since Snapshot 2. Data Blocks A and D are referenced from Snapshot 1, and Data Block C1 is referenced from Snapshot 2.
-   When you roll the disk back to the status of Snapshot 3, the **Roll Back Disk** feature copies Data Blocks A, B2, C1, and D to the disk.
-   If you delete Snapshot 2, Data Block B1 is deleted, but Data Block C1 is retained because it is referenced by Snapshot 3. When you roll the disk back to the status of Snapshot 3, Data Block C1 can still be restored.

## Snapshot chain

A snapshot chain contains all of the snapshots of a specific disk. Each disk has a snapshot chain. A disk and its snapshot chain have the same ID.

A snapshot chain records the relationships between data blocks and contains the following information:

-   Snapshot size: the size of storage space occupied by all snapshots in the snapshot chain.

    **Note:** You are charged based on the snapshot size. You can use the snapshot chain to check the snapshot size of a disk.

-   Snapshot quota: Each disk can have up to 256 manual snapshots and 1,000 automatic snapshots. For more information, see the "Snapshot limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md).

    **Note:** When the snapshot quota is reached, you must free up storage space to create more snapshots. For automatic snapshots, the system automatically deletes the earliest automatic snapshot to free up storage space. For manual snapshots, you must manually delete snapshots to free up storage space. For more information, see [Apply or disable an automatic snapshot policy](/intl.en-US/Snapshots/Automatic snapshot policies/Apply or disable an automatic snapshot policy.md) and [Delete a snapshot](/intl.en-US/Snapshots/Use snapshots/Delete a snapshot.md).

-   Node: Each node in the snapshot chain represents a snapshot of the source disk. Each snapshot chain can have up to 1,256 nodes, which is equal to the sum of quotas of manual snapshots and automatic snapshots.

## Snapshot deletion

You can delete snapshots that are no longer needed. If the number of snapshots reaches the snapshot quota, you must delete some snapshots to free up storage space. The following figure shows the workflow and logic when you delete a snapshot from a snapshot chain. In this example, Snapshot S1 is deleted.

![Snapshot deletion](https://gw.alipayobjects.com/zos/onekb/GEmePRxTvdRaZPCgtUhF.png)

1.  Alibaba Cloud ECS analyzes all data blocks in Snapshot S1, and deletes the data blocks that are not referenced by other snapshots in the snapshot chain.
2.  Alibaba Cloud ECS adds the data blocks of Snapshot S1 that are referenced by other snapshots in the snapshot chain to Snapshot S2. The remaining snapshots in the snapshot chain record the information of 10 data blocks:
    -   Six data blocks from Snapshot S0
    -   Two data blocks from Snapshot S1
    -   Two data blocks from Snapshot S2

