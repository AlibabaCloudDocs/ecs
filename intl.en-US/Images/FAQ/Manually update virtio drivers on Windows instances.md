# Manually update virtio drivers on Windows instances

This topic describes how to manually update virtio drivers on Windows instances.

Before you update virtio drivers on your Windows instances, we recommend that you create snapshots to back up instance data. For more information, see [Create a snapshot for a disk](/intl.en-US/Snapshots/Use snapshots/Create a snapshot for a disk.md).

You can use one of the following methods to manually update virtio drivers:

-   If your Windows instance has Internet access, we recommend that you use a script to update the virtio drivers on the instance. For more information, see [Method 1: Use a script](#section_dxx_gk9_ro8).
-   If your Windows instance does not have Internet access, we recommend that you upload an installation package to install more recent versions of virtio drivers on the instance. For more information, see [Method 2: Use an installation package](#section_1kb_hov_812).
-   If you want to update the virtio drivers on multiple Windows instances that have access to the Internet or the internal networks within virtual private clouds \(VPCs\), you can use Cloud Assistant provided by Alibaba Cloud to batch update the drivers on the instances. For more information, see [Method 3: Use Cloud Assistant to batch update virtio drivers on multiple instances](#section_u8c_blo_x3v).

## Method 1: Use a script

If your Windows instance has Internet access, you can use a script to update the virtio drivers on the instance.

1.  Connect to the Windows instance.

    For more information, see [Connection methods](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  On the Windows instance, download the script used to update the virtio drivers.

    Click [InstallVirtIo.ps1](https://windows-driver-cn-beijing.oss-cn-beijing.aliyuncs.com/virtio/InstallVirtIo.ps1) to download the InstallVirtIo.ps1 script.

3.  Run the InstallVirtIo.ps1 script to update the virtio drivers.

    In this example, InstallVirtIo.ps1 is downloaded to the C:\\test directory.

    1.  Access the C:\\test directory.

        In actual operations, access the directory to which InstallVirtIo.ps1 is downloaded.

    2.  Select and right-click InstallVirtIo.ps1 and then select **Run with PowerShell**.

        ![Run the script](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3479465261/p274473.png)

        Alternatively, you can press the Shift key and right-click a blank area in the folder window at the same time. Then, select **Open PowerShell window here**. Run the InstallVirtIo.ps1 script in Windows PowerShell.

        **Note:** If you are logged on to the Windows instance as a standard user, you must run this script as an administrator. If you are logged on as an administrator, you can run this script directly.

4.  After the script is run, restart the instance.

    For more information, see [Reboot the instance](/intl.en-US/Instance/Manage instance status/Restart an instance.md). The updated virtio drivers take effect after the instance is restarted.


## Method 2: Use an installation package

If your Windows instance does not have Internet access, you can use this method to update the virtio drivers.

1.  On your computer, download the virtio driver package provided by Alibaba Cloud.

    Click [Virtio Driver Package](https://windows-driver-cn-beijing.oss-cn-beijing.aliyuncs.com/virtio/210408.1454.1459_bin.zip) to download the package.

    The downloaded package is named 210408.1454.1459\_bin.zip.

2.  Upload 210408.1454.1459\_bin.zip to the Windows instance.

    You can use one of the following methods to upload the package:

    -   If your computer is running a Windows operating system, use the Windows Remote Desktop Connection tool to connect to the instance from your computer and then upload the package.
    -   Build an FTP site on the instance and then use an FTP client to upload the package. For more information, see [Manually build an FTP site on a Windows instance](/intl.en-US/Tutorials/Build an application/Build an FTP site on an ECS instance/Manually build an FTP site on a Windows instance.md).
3.  On the Windows instance, decompress 210408.1454.1459\_bin.zip and open the 210408.1454.1459\_bin folder.

    In the 210408.1454.1459\_bin folder, you can find the subfolders that correspond to different Windows versions.

    ![Windows versions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3479465261/p274528.png)

    These subfolders contain the virtio driver installation files for the corresponding Windows versions. Take note of the following subfolders:

    -   win10: contains the driver installation files for Windows Server 2016, Windows Server 2019, and Windows 10.
    -   Win8: contains the driver installation files for Windows Server 2012 R2 and Windows 8.1.
    -   win7: contains the drivers installation files for Windows Server 2008 R2 and Windows 7.
    In each of these subfolders, driver installation files are put into the x86 or amd64 subfolder based on the architectures on which the drivers can be installed. The installation files in the amd64 subfolders are applicable to 64-bit operating systems with an AMD64 architecture. The installation files in the x86 subfolders are applicable to 32-bit operating systems with an x86 architecture.

4.  Open an appropriate subfolder based on the operating system version of the Windows instance.

    In this example, open the amd64 subfolder in the C:\\test\\210408.1454.1459\_bin\\Win8\\amd64 directory because the Windows instance is running a Windows Server 2012 R2 64-bit operating system.

5.  After the amd64 subfolder is opened, press the Shift key and right-click a blank area at the same time. Then, select **Open PowerShell window here**.

    ![powershell](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8492565261/p274577.png)

6.  Run the following command in Windows PowerShell to install the new versions of virtio drivers.

    **Note:** If you are logged on to the Windows instance as a standard user, you must run this command as an administrator. If you are logged on as an administrator, you can run this command directly.

    ```
    pnputil -i -a *.inf
    ```

    A command output shown in the following figure indicates that the new versions of virtio drivers are installed.

    ![Run the command](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3479465261/p274580.png)

7.  Restart the Windows instance.

    For more information, see [Reboot the instance](/intl.en-US/Instance/Manage instance status/Restart an instance.md). The new versions of virtio drivers take effect after the instance is restarted.


## Method 3: Use Cloud Assistant to batch update virtio drivers on multiple instances

If you want to update the virtio drivers on multiple Windows instances that have access to the Internet or the internal networks within virtual private clouds \(VPCs\), you can use Cloud Assistant provided by Alibaba Cloud to batch update the drivers on the instances.

**Note:** To update virtio drivers by using Cloud Assistant, you must download the required installation package. The system preferentially downloads the package over the internal networks within VPCs. If the packages cannot be downloaded over the internal networks, the system downloads the package over the Internet.

1.  On your computer, download the InstallVirtIo.ps1 script.

    Click [InstallVirtIo.ps1](https://windows-driver-cn-beijing.oss-cn-beijing.aliyuncs.com/virtio/InstallVirtIo.ps1) to download the InstallVirtIo.ps1 script.

2.  Log on to the [ECS console](https://ecs.console.aliyun.com).

3.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **ECS Cloud Assistant**.

4.  In the top navigation bar, select a region.

    The selected region must be the region where your instances reside.

5.  On the **Cloud Assistant** page, click **Create or Run Command**.

6.  In the **Create Command** panel, configure parameters.

    -   In the **Command Information** section, configure the following required parameters and accept the default values for other parameters:
        -   **Command Source**: Select **Enter Command Content**.
        -   **Command Name**: Specify a name or accept the default name for the command.
        -   **Implementation plan**: Select **Immediate execution**.
        -   **Command Type**: Select **PowerShell**.
        -   **Command**: Enter the InstallVirtIo.ps1 script content in this field.

            You must open the InstallVirtIo.ps1 script and copy the entire script to the Command field.

    -   In the **Select Instances** section, select the IDs of the instances on which you want to update the virtio drivers.
7.  Click **Run**.

    You can view the execution results of the command on the **Command Execution Result** tab. For more information, see [View execution results in the console](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Query execution results and fix common problems.md). A command output shown in the following figure corresponds to one of the selected instances and indicates that the virtio drivers are updated on the instance.

    ![Execution results](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3479465261/p274637.png)

8.  Batch restart the instances.

    For more information, see [Reboot the instance](/intl.en-US/Instance/Manage instance status/Restart an instance.md). The updated virtio drivers take effect after the instances are restarted.


