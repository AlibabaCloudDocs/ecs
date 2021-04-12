# Delete a replication relationship to make a secondary disk available

After Asynchronous Block Storage Replication \(ABSR\) is enabled, a secondary disk can only synchronize data from its primary disk. You cannot perform the attach or read and write operations on the secondary disk. To use a secondary disk, you must stop and delete the replication relationship of the secondary disk.

After a replication relationship is stopped and deleted, the primary disk stops backing up data to the secondary disk. You must make appropriate planning to ensure data security of the primary disk.

## Step 1: Stop a replication relationship

When a replication relationship is in the **Active** \(`active`\) state, you can stop the relationship.

1.  Go to the Asynchronous Block Storage Replication page.

    1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

    2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Asynchronous Replication Relationship**.

2.  Find the replication relationship that you want to stop and click **Stop** in the Actions column.


## Step 2: Delete the replication relationship

After the replication relationship is stopped, it is in the **Paused** \(`paused`\) state. You can delete the replication relationship.

1.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Asynchronous Replication Relationship**.

2.  Find the replication relationship that is stopped and click **Delete** in the Actions column.

3.  In the message that appears, click **OK**.

    After the replication relationship is deleted, the secondary disk is automatically rolled back to the state that it was in when data was last synchronized. Data that is being synchronized is lost. Then, you can perform the attach or read and write operations on the secondary disk in the same way as you do on other cloud disks.


