---
keyword: [Alibaba Cloud, ECS, resize a disk, resize, resize a disk on a Windows instance]
---

# Update Red Hat virtio drivers of Windows instances

You can resize the disks of Windows instances online without having to restart the instances. You can also query the serial numbers of disks from the operating systems. If you want to resize the disks of a Windows instance created before March 30, 2019 or query the serial numbers of the disks attached to an instance created before May 1, 2020, follow the procedure described in this topic to check whether Red Hat virtio drivers of the instances must be updated.

-   Red Hat virtio drivers are supported in only Windows Server 2008 and later.
-   If an ECS instance has multiple data disks attached, the driver update process may take one to two minutes to complete.

## Procedure

You can perform the following operations to update the Red Hat virtio drivers of a Windows instance:

1.  [Step 1: Check the version of the drivers](#section_mhl_nhy_dhb)
2.  [Step 2: Download the drivers](#section_93w_k6h_jgz)
3.  [Step 3. Update the Red Hat virtio drivers](#section_pvf_cr1_qgb)

## Step 1: Check the version of the drivers

You can use one of the following methods to check the version of the drivers:

-   Method 1: Use the PowerShell script to check the version of the drivers.
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
|Resize a disk online|58011 or later|Resize the disk online. For more information, see [Resize disks online for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Linux instances.md).|
|Earlier than 58011|Proceed to the next step.|
|Query the serial number of a disk|58015 or later|Query the serial number of the disk. For more information, see [Query the serial number of a disk](/intl.en-US/Block Storage/Cloud disks/Query the serial number of a disk.md).|
|Earlier than 58015|Proceed to the next step.|

## Step 2: Download the drivers

Click [here](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/169523/cn_zh/1590721781509/virtio_58015.zip) to download the virtio driver package and decompress it. The subsequent steps in this topic are based on the assumption that the decompressed driver package is located at C:\\Users\\Administrator\\Desktop\\virtioDriver. The following table lists the extracted folders corresponding to ECS instances of different operating system versions.

|Driver file \(folder\) name|Description|
|:--------------------------|:----------|
|win7|Windows Server 2008 R2 and Windows 7|
|Wlh|Windows Server 2008|
|Win8|Windows Server 2012 and Windows Server 2012 R2|
|win10|Windows 10, Windows Server 2016, Windows Server 2019, and Windows Server systems of later versions|
|amd64|64-bit|
|x86|32-bit|

## Step 3. Update the Red Hat virtio drivers

You can use one of the following methods to update the Red Hat virtio drivers:

-   Method 1: Use pnputil to add and install the drivers
    1.  Open Command Prompt.
    2.  Run the following command to add the driver package:

        ```
        pnputil -i -a <path to virtio driver inf\>
        ```

        Make sure that you have extracted the .inf file to the specified directory, which is <path to virtio driver inf\>. Example: C:\\Users\\Administrator\\Desktop\\virtioDriver\\win7\\amd64\\viostor.inf.

        -   To update only the disk driver, run the following command:

            ```
            pnputil -i -a C:\Users\Administrator\Desktop\virtioDriver\win7\amd64\viostor.inf
            ```

        -   To update all Red Hat virtio drivers, run the following command:

            ```
            pnputil -i -a C:\Users\Administrator\Desktop\virtioDriver\win7\amd64\*.inf
            ```

    3.  Restart the operating system of the ECS instance for the driver update to take effect.
-   Method 2: Manually add the drivers
    1.  Open Device Manager.
    2.  Right-click **Red Hat VirtIO SCSI controller** under **Storage controllers** and select **Update Driver Software...**

        **Note:** If multiple **Red Hat VirtIO SCSI controller** devices appear, you need to update only one of them.

        ![Update the drivers](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1182909951/p41810.png)

    3.  Select **Browse my computer for driver software**.
    4.  Select **Let me pick from a list of device drivers on my computer**.
    5.  Click **Have Disk**.
    6.  Select the viostor driver file in the corresponding folder, and follow the wizard to update the driver.
    7.  Restart the operating system of the ECS instance for the driver update to take effect.

-   For more information about how to resize a disk online, see [Resize a disk online](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Linux instances.md).
-   For more information about how to query the serial number of a disk, see [Query the serial number of a disk](/intl.en-US/Block Storage/Cloud disks/Query the serial number of a disk.md).

