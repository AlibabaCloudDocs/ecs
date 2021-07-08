---
keyword: [Alibaba Cloud, ECS, resize a disk, resize, resize a disk on a Windows instance]
---

# Update Red Hat virtio drivers of Windows instances

You can resize the disks of Windows instances online without the need to restart the instances. You can also query the serial numbers of disks from the operating systems. If you want to resize the disks of a Windows instance created before March 30, 2019 or query the serial numbers of the disks attached to an instance created before May 1, 2020, perform the operations described in this topic to check whether Red Hat virtio drivers of the instances must be updated.

-   Red Hat virtio drivers are supported in only Windows Server 2008 and later.
-   If an Elastic Compute Service \(ECS\) instance has multiple data disks attached, the driver update process may take 1 to 2 minutes.

## Procedure

You can perform the following operations to update the Red Hat virtio drivers of a Windows instance:

1.  [Step 1: Check the version of the drivers](#section_mhl_nhy_dhb)
2.  [Step 2: Download the drivers](#section_93w_k6h_jgz)

## Step 1: Check the version of the drivers

You can use one of the following methods to check the version of the drivers:

-   Method 1: Use the PowerShell script to check the version of the drivers
    1.  Connect to the Windows instance. For more information, see [Connect to a Windows instance from a local client](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Windows instance from a local client.md).
    2.  Open Command Prompt.
    3.  Enter powershell to access the PowerShell interactive interface.
    4.  Enter and run the following command to check the version and determine whether the ECS instance supports resizing disks online based on the command output:

        ```
        [System.Diagnostics.FileVersionInfo]::GetVersionInfo("C:\Windows\System32\drivers\viostor.sys")
        ```

        ![Check the version of the drivers](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1182909951/p41813.png)

-   Method 2: Manually check the version of the drivers
    1.  Connect to the Windows instance.
    2.  Go to the C:\\Windows\\System32\\drivers system directory.
    3.  Right-click the viostor.sys file, select **Properties**, and then view the file version on the **Details** tab.

        ![File version](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1182909951/p41818.png)


Determine whether the requirements of the file version are met based on the query results, and perform corresponding operations.

|Scenario|Version of the Red Hat virtio-scsi driver|Operation|
|--------|-----------------------------------------|---------|
|Resize a disk online|58011 or later|Resize the disk online. For more information, see [Resize disks online for Windows instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Windows instances.md).|
|Earlier than 58011|Proceed to the next step.|
|Query the serial number of a disk|58015 or later|Query the serial number of the disk. For more information, see [Query the serial number of a disk](/intl.en-US/Block Storage/Cloud disks/Query the serial number of a disk.md).|
|Earlier than 58015|Proceed to the next step.|

## Step 2: Download the drivers

If your Windows instance can access the Internet, you can use a script to update the virtio driver on the instance.

Before you update the virtio drivers on your Windows instances, we recommend that you create snapshots to back up instance data. For more information, see [Create a snapshot for a disk](/intl.en-US/Snapshots/Use snapshots/Create a snapshot for a disk.md).

1.  Connect to the Windows instance.

    For more information, see [Connection methods](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  On the Windows instance, download the script used to update the virtio driver.

    Click [InstallVirtIo.ps1](https://windows-driver-cn-beijing.oss-cn-beijing.aliyuncs.com/virtio/InstallVirtIo.ps1) to download the InstallVirtIo.ps1 script.

3.  Run the InstallVirtIo.ps1 script to update the virtio driver.

    In this example, InstallVirtIo.ps1 is downloaded to the C:\\test directory.

    1.  Open the C:\\test folder.

        In actual operations, access the directory to which InstallVirtIo.ps1 is downloaded.

    2.  Select and right-click InstallVirtIo.ps1 and then select **Run with PowerShell**.

        ![Run the script](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3479465261/p274473.png)

        Alternatively, you can press the Shift key and right-click a blank area in the folder at the same time. Then, select **Open PowerShell window here**. Run the InstallVirtIo.ps1 script in Windows PowerShell.

        **Note:** If you are logged on to the Windows instance as a standard user, you must run this script as an administrator. If you are logged on as an administrator, you can directly run this script.

4.  After the script is run, restart the instance.

    For more information, see [Reboot the instance](/intl.en-US/Instance/Manage instance status/Restart an instance.md). After the instance is restarted, the updated virtio driver takes effect.


-   For information about how to resize a disk online, see [Resize a disk online](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Linux instances.md).
-   For information about how to query the serial number of a disk, see [Query the serial number of a disk](/intl.en-US/Block Storage/Cloud disks/Query the serial number of a disk.md).
-   For more information about how to manually update virtio drivers on Windows instances, see [Manually update virtio drivers on Windows instances](/intl.en-US/Images/FAQ/Manually update virtio drivers on Windows instances.md).

