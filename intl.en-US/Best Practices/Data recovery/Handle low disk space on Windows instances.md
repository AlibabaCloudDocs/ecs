---
keyword: [no disk space, low disk space]
---

# Handle low disk space on Windows instances

This topic describes how to handle low disk space on Windows instances and the best practices of daily disk management for Windows instances.

The methods described in this topic apply to Windows Server 2003 and later. In this topic, Windows Server 2012 R2 is used.

## Solutions and best practices

When you are running out of available disk space on a Windows instance, you can take one of the following measures:

-   [Release disk space](#section_o27_pqu_ih6)
-   [Resize the disk](#section_6e2_k66_nwk)

Develop good habits for using disk space with these best practices:

-   [Compress files for archiving](#section_d4u_a9n_c2y)
-   [Delete unneeded applications on a regular basis](#section_e2s_z1j_n21)
-   [Configure disk monitoring](#section_gwv_pwf_5bs)

## Release disk space

When you are running out of available disk space on a Windows instance, you can clear unnecessary files from the disk. Perform the following operations:

1.  Find the files that are taking up the most disk space.

    1.  Connect to the Windows instance. For more information, see [Connect to a Windows instance from a local client](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Windows instance from a local client.md).

    2.  Click **Start** and then click **This PC**.

    3.  Click the disk to be cleared, and press **Ctrl+F**.

    4.  In the top navigation bar, choose **Search** \> **Size**, and filter out large files on the specified disk.

        **Note:** You can also customize a file size range for retrieval. For example:

        -   Enter Size: \> 500 MB to search for files that are larger than 500 MB in size.
        -   Enter Size: \> 100 MB < 500 MB to search for files that are between 100 MB and 500 MB in size.
2.  Delete files that you no longer need.

    We recommend that you use the Windows Disk Cleanup utility to delete unneeded files such as log files, and empty the recycle bin. The Windows Disk Cleanup utility is not installed on the instance by default and must be installed manually. Perform the following operations to install the utility and use it to delete files:

    1.  In the taskbar, click the Server Manager icon.

    2.  In the upper-right corner, choose **Manage** \> **Add Roles and Features**.

    3.  In the Add Roles and Features Wizard dialog box, keep the default settings and click **Next** until the **Features** module is displayed. Select **Ink and Handwriting Services** and **Desktop Experience**, and click **Next**.

    4.  Click **Install**.

    5.  After the utility is installed, the system prompts you to restart the instance. You must restart the instance manually. After the instance restarts, verify that Desktop Experience has been installed.

    6.  Click **Start**. In the top search box, enter **Disk Cleanup**. In the dialog box that appears, select the disk that you want to delete and click **OK**.


## Resize the disk

When you are running out of available disk space on a Windows instance, you can resize the disks. For more information, see [Resize disks online for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Linux instances.md) or [Resize disks offline for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks offline for Linux instances.md).

## Compress files for archiving

For files that are generated on a regular basis, you can compress them for archiving to improve disk usage. We recommend that you use WinRAR to compress files. The following example describes how to configure a backup policy for compressing files:

1.  Download and install WinRAR. Download link: [WinRAR and RAR archiver downloads](https://www.rarlab.com/download.htm).

    WinRAR is used in this example.

2.  After WinRAR is installed, find the file to be compressed, right-click the file, and then select **Add to archive...**

3.  In the Settings dialog box, click the Backup tab and select **Generate archive name by mask**. Do not click **OK**.

4.  Click the General tab and then click **Browse** to specify the path in which to save the archive file. Click **Profiles...** and select **Save current settings to a new profile...**

5.  In the Profile parameters dialog box, set the **Profile name** parameter and select **Save archive name**, **Save selected file names**, and **Create shortcut on desktop**. Click **OK**.

6.  In the Archive name and parameters dialog box, click **OK**.

    A shortcut key to the archive file is generated on the desktop.

7.  Press **Win+R** to open the **Run** dialog box. Run the `control` command to open the **Control Panel** page. On the **Control Panel** page, click **System and Security** and then click **Scheduled tasks**. In the Task Scheduler dialog box, click **Create Basic Task...**

8.  In the Create Basic Task Wizard dialog box, enter a new task name and click **Next**.

9.  Select a trigger for the task and click **Next**. Select **Start a program** and click **Next**.

10. In the Start a Program step, set the **Program/script:** parameter. To set this parameter, find the previously generated shortcut key. Right-click the shortcut key and then select **Properties**. In the dialog box that appears, copy the value of the **Target:** field.

11. In the Create Basic Task Wizard dialog box, paste the copied value in the **Program/script:** field of the Start a Program step. Click **Finish**.


After you configure the backup policy, you can delete expired archive files on a regular basis to avoid taking up a large amount of disk space.

## Delete unneeded applications on a regular basis

You can delete unneeded applications on a regular basis by clicking Programs and Features on the Control Panel page.

## Configure disk monitoring

Monitoring plug-ins are pre-installed on ECS instances. You can log on to the [Cloud Monitor console](https://cms.console.aliyun.com/#/groups/) to create disk alert rules. In this way, you can receive alerts when disk usage exceeds a configured threshold and clean the disk in a timely manner. For more information, see [Manage alert rules](/intl.en-US/Alarm service/Alarm rules/Manage alert rules.md).

![Set alert rules](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4114488951/p12924.png)

