---
keyword: [backup, data backup, snapshot capacity, snapshot cost]
---

# Delete a snapshot

You can delete snapshots that are no longer needed to free up space or when the maximum number of snapshots has been reached. This topic describes the procedure to delete a snapshot in the ECS console. This procedure applies to both manual snapshots and automatic snapshots.

-   You have created a snapshot. For more information, see [Create a snapshot for a disk](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).
-   If a snapshot has been used to create custom images, you must delete those custom images before the snapshot can be deleted. For more information, see [Delete a custom image](/intl.en-US/Images/Custom image/Delete a custom image.md).

To delete a snapshot from which you have created disks, you can choose only **Force Delete**. After the snapshot is deleted, the disks cannot be re-initialized.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Snapshots**.

3.  In the top navigation bar, select a region.

4.  Select one or more snapshots to be deleted and click **Delete** at the bottom of the page.

    ![Delete a snapshot ](../images/p54074.png)

5.  In the Delete dialog box, select **Delete** or **Force Delete**.

    **Note:** To delete a snapshot from which you have created disks, you can choose only **Force Delete** and then click Proceed to Forcibly Delete. After a snapshot is deleted, you cannot perform operations that depend on the status of the original snapshot data, such as the operation to [reinitialize a cloud disk](/intl.en-US/Block Storage/Cloud disks/Reinitialize a cloud disk/Re-initialize a system disk.md).

    ![Active the ECS snapshot service](../images/p54077.png)

6.  Click **OK**.


**Related topics**  


[DeleteSnapshot](/intl.en-US/API Reference/Snapshots/DeleteSnapshot.md)

