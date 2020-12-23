---
keyword: [re-initialize, re-install, master reset, system disk, reset system]
---

# Re-initialize a system disk

This topic describes how to re-initialize a system disk in the ECS console. After a system disk is re-initialized, it is restored to the status when it was created.

-   Data is lost after the disk is re-initialized. You must create snapshots for the disk to back up data. For more information, see [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).
-   The instance must be in the Stopped state before you re-initialize the disk. Your business is interrupted when you stop your instance. Proceed with caution. For more information, see [Stop an instance](/intl.en-US/Instance/Manage instances/Stop an instance.md).

    You must select **Retain Instance and Continue Charging After Instance Is Stopped** when you stop a pay-as-you-go instance.

    **Note:** If you select **No Charges After Instance Is Stopped**, you may not be able to start the instance after you re-initialize the disk. For more information, see [No Fees for Stopped Instances \(VPC-Connected\)](/intl.en-US/Pricing/Billing methods/No Fees for Stopped Instances (VPC-Connected).md).

    ![Retain Instance and Continue Charging After Instance Is Stopped](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4872909951/p5328.png)

-   You cannot re-initialize a disk that has local snapshots. You can create local snapshots only for enhanced SSDs \(ESSDs\). Therefore, if the disk is an ESSD, make sure that it does not have local snapshots.
-   \(Applicable only to Linux instances\) If you want to use an SSH key pair for authentication when you re-initialize a system disk, you must have created or imported an SSH key pair. For more information, see [Create an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Create an SSH key pair.md) and [Import an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Import an SSH key pair.md).

When a disk is attached to an ECS instance, you can re-initialize the disk to restore it to the status when it was created. The following list provides the changes of a system disk after you re-initialize it:

-   The system disk is restored to the status when it was created.

    For example, if you use a public image that runs Windows Server 2012 R2 to create an instance. After you re-initialize the system disk of the instance, the instance still runs Windows Server 2012 R2 but the applications that are installed and data generated after the instance was created are deleted.

    **Note:** If you re-initialize the system disk after you replace the system disk, the new system disk is re-initialized instead of the old one.

-   If an automatic snapshot policy is applied to the system disk, the policy remains valid after the system disk is re-initialized.
-   The IP address and system disk ID of the ECS instance are not changed.
-   The automatic and manual snapshots of the system disk remain available. You can use these snapshots to roll back the disk. For more information, see [Roll back a disk by using a snapshot](/intl.en-US/Snapshots/Use snapshots/Roll back a disk by using a snapshot.md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the ECS instance for which you want to re-initialize the system disk, and click the instance ID to go to the Instance Details page.

5.  Click the **Cloud Disk** tab.

6.  Find the system disk and click **Reinitialize Disk** in the **Actions** column.

7.  In the **Reinitialize Disk** dialog box, configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |Security|Windows instances: Select Set Password. You can use the old password or specify a new password.|
    |Linux instances: Select **Set SSH Key** or **Set Password**.    -   **Set SSH Key**: binds an SSH key pair to the instance. You can then log on the instance by using the SSH key pair.
    -   **Set Password**: specifies a logon password. You can use the old password or specify a new password. |
    |Security Hardening|After you select **Activate**, security components are loaded to the instance free of charge. These components provide services such as webshell detection, remote logon reminder, and protection against brute-force attacks.|
    |Instance Startup Policy|If you select **Start Instance after Resetting Disk**, the instance automatically starts after you re-initialize the system disk.|

8.  Click **Confirm**.


-   \(Applicable only to Linux instances\) If data disks have been attached to the ECS instance before you re-initialize its system disk, you must recreate the mount point information and mount file systems to the instance. For more information, see the [How do I reattach data disks after I re-initialize the system disk of a Linux instance?](/intl.en-US/Block Storage/Block Storage FAQ.md) section of the *Elastic Block Storage FAQ* topic.

    **Note:** After you re-initialize the system disk of a Linux instance, data within the data disks that are attached to the instance is not changed, but the mount point information is lost.

-   After the system disk is re-initialized, you must redeploy the applications and reconfigure the parameters on the disk to restore your business as soon as possible.
-   If you have created snapshots for the system disk, you can use the snapshots to create data disks and attach the data disks to the instance to obtain data in the original system disk. For more information, see [Create a disk from a snapshot](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk from a snapshot.md).

**Related topics**  


[ReInitDisk](/intl.en-US/API Reference/Disk/ReInitDisk.md)

[Re-initialize a data disk](/intl.en-US/Block Storage/Cloud disks/Reinitialize a cloud disk/Re-initialize a data disk.md)

