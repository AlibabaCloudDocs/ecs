# Roll back disks by using an instance snapshot

After an instance snapshot is created, you can use the instance snapshot to roll back one or more disks in the event of system failure or accidental changes.

Before you roll back a disk by using an instance snapshot, take note of the following items:

-   An instance snapshot is created. For more information, see [Create snapshots for multiple disks together by creating an instance snapshot](/intl.en-US/Snapshots/Use instance snapshots/Create snapshots for multiple disks together by creating an instance snapshot.md).

    **Note:** The rollback operation is irreversible. After a disk is rolled back, the data that you added, deleted, or changed from the time when the instance snapshot was created to the time when the disk is rolled back is lost. To avoid data loss caused by accidental changes, we recommend that you create an instance snapshot for the current disk before you roll back the disk.

-   The instance is in the **Stopped** state. For more information, see [Stop an instance](/intl.en-US/Instance/Manage instances/Stop an instance.md).

    **Note:** If the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled, a pay-as-you-go instance in a virtual private cloud \(VPC\) may not be restarted after the disk of the instance is rolled back. Select **Retain Instance and Continue Charging After Instance Is Stopped** when you stop the instance.

-   The disk is not released and remains attached to the instance.
-   The operating system of the system disk remains unchanged after the instance snapshot is created.
-   Snapshots of the disk are not deleted. If the snapshots of a disk are deleted after the instance snapshot is created, the disk cannot be rolled back. Only disks whose snapshots are not deleted can be rolled back.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Snapshots**.

3.  In the top navigation bar, select a region.

4.  Click the **Instance Snapshots** tab.

5.  Find the instance snapshot and click **Rollback instance** in the **Actions** column.

6.  In the **Rollback instance** dialog box, select the disks that you want to roll back and perform the rollback.

    1.  View the precautions about instance rollback.

    2.  If you want to start the instance after the rollback, select **Start Instance Immediately after Rollback**.

        If you select this option, the instance automatically starts after the rollback. If you do not select this option, you must manually start the instance after the rollback.

    3.  In the **Cloud disk snapshot** section, select the disks that you want to roll back.

    4.  Click **OK Rollback**.


After the rollback is complete, you can log on to the instance to check whether data on the disks is consistent with that of the snapshot.

