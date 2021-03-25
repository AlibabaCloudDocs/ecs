# Enable the application-consistent snapshot feature

The Alibaba Cloud snapshot service works with Cloud Assistant to provide the application-consistent snapshot feature. Application-consistent snapshots can be used for rollbacks to avoid log rollbacks when applications such as databases start. This ensures that the applications start in a consistent state.

-   The instance allows access to the Internet. A public IP address is configured or an elastic IP address \(EIP\) is associated.
-   The instance runs one of the following operating systems:
    -   Windows: Windows Server 2019, Windows Server 2016, and Windows Server 2012.
    -   Linux: CentOS 7.6 or later, Ubuntu 18.04 or later, and Alibaba Cloud Linux 2 \(2.1903 LTS 64-bit\).
-   The disks of the instance are enhanced SSDs \(ESSDs\) and the file system is EXT3, EXT4, XFS, or NTFS.

By default, created snapshots are crash-consistent. If you enable the application-consistent snapshot feature when you create a snapshot, the system creates an application-consistent snapshot or a file-system consistent snapshot based on your requirements.

|Type|Description|Implementation|
|----|-----------|--------------|
|Application-consistent snapshot|Application-consistent snapshots back up the data in memory and the database transactions in progress when the snapshots are created. This ensures consistency of the application data and database transactions. When application-consistent snapshots are used for rollbacks, no data corruption or loss occurs, logs are not rolled back when databases start, and applications start in a consistent state.Application-consistent snapshots are identified by the `APPConsistent:True` tag.

|The application-consistent snapshot feature is implemented in different manners based on the operating system:-   Windows: The feature is implemented by using Volume Shadow Copy Service \(VSS\).
-   Linux: The feature is implemented by using custom shell scripts. You must write your own scripts based on the application. When you use custom scripts, Alibaba Cloud does not take responsibility for application consistency issues. |
|File-system consistent snapshot|If the application-consistent snapshot feature is enabled but relevant conditions are not met, file-system consistent snapshots are created.File-system consistent snapshots synchronize the file system memory and disk information when the snapshots are created and freezes write operations on the file system to ensure consistency of the file system. File-system consistent snapshots can be used to prevent the operating system from performing disk check and fix operations by using check disk \(chkdsk\) or file system consistency check \(fsck\).

File-system consistent snapshots are identified by the `FsConsistent:True` tag.

|The file-system consistent snapshot feature is implemented based on the operating system:-   Windows: If no VSS writers are available, file-system consistent snapshots are created by default.
-   Linux: If no application scripts are available, file-system consistent snapshots are created by default. |

## Procedure

1.  [Step 1: Configure a RAM role for the ECS instance](#section_qez_tzh_rwa)

    Before you enable the application-consistent snapshot feature, you must configure a RAM role for the ECS instance.

2.  Step 2: Enable the application-consistent snapshot feature based on the operating system of the instance.
    -   [Step 2: Enable the application-consistent snapshot feature for Windows instances](#section_kqu_a40_ztc)

        For Windows instances, you can use VSS to implement application consistency.

    -   [Step 2: Enable the application-consistent snapshot feature for Linux instances](#section_xp0_bto_m3n)

        For Linux instances, you must configure shell scripts \(application pre-freeze and post-thaw scripts\) based on the applications in the instance to implement application consistency.


## Step 1: Configure a RAM role for the ECS instance

1.  Log on to the [Resource Access Management \(RAM\) console](https://ram.console.aliyun.com/) by using your Alibaba Cloud account.

2.  Create a RAM role for the application-consistent snapshot feature. For more information about how to create a RAM role, see [Create a RAM role for a trusted Alibaba Cloud service](/intl.en-US/RAM Role Management/Create a RAM role/Create a RAM role for a trusted Alibaba Cloud service.md).

    The following figure shows an example on how to create the AppSnapshotRoleName RAM role.

    ![RAM role for the application-consistent snapshot feature](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6800666161/p250036.png)

3.  Create a permission policy for the application-consistent snapshot feature. For more information about how to create a policy, see [Create a custom policy](/intl.en-US/Policy Management/Custom policies/Create a custom policy.md).

    ![Snapshot policy](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6800666161/p249921.png)

    Create the AppSnapshotPolicy policy to grant the permissions to query snapshot details, create snapshots, configure tags, and query disk details. You can use the following policy:

    ```
    {
        "Version": "1",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "ecs:DescribeSnapshot*",
                    "ecs:CreateSnapshot*",
                    "ecs:TagResources",
                    "ecs:DescribeDisks"
                ],
                "Resource": [
                    "*"
                ],
                "Condition": {}
            }
        ]
    }
    ```

4.  Attach the AppSnapshotPolicy policy to the AppSnapshotRoleName RAM role. For more information about how to attach a policy to a RAM role, see [Grant permissions to a RAM role](/intl.en-US/RAM Role Management/Grant permissions to a RAM role.md).

    ![Attach policy](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6800666161/p250505.png)

5.  Bind the AppSnapshotRoleName RAM role to the ECS instance. For more information about how to bind a RAM role to an ECS instance, see [Bind an instance RAM role](/intl.en-US/Security/Instance RAM roles/Bind an instance RAM role.md).


## Step 2: Enable the application-consistent snapshot feature for Windows instances

For Windows instances, you can use VSS to implement application consistency. This section describes how to enable the application-consistent snapshot feature for a Windows instance.

1.  Go to the Instances page.

    1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

    2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

    3.  In the top navigation bar, select the region where the ECS instance on which you want to perform operations is located.

2.  Find the instance for which you want to enable the application-consistent snapshot feature and choose **More** \> **Disk and Image** \> **Create Instance Snapshot** in the Actions column.

3.  In the **Create Instance Snapshot** dialog box, configure the parameters for the instance snapshot and enable the instant access feature.

    -   For more information about the parameters of the instance snapshot, see [Create snapshots for multiple disks together by creating an instance snapshot](/intl.en-US/Snapshots/Use instance snapshots/Create snapshots for multiple disks together by creating an instance snapshot.md).
    -   For more information about the instant access feature, see [Enable or disable the instant access feature](/intl.en-US/Snapshots/Use snapshots/Enable or disable the instant access feature.md).
4.  In the **Create Instance Snapshot** dialog box, specify Application-consistent Snapshot.

    -   If you select **Enable Application-consistent Snapshot** and **Whether Writer is included by default**, an application-consistent snapshot is created.
    -   If you select only **Enable Application-consistent Snapshot**, a file-system consistent snapshot is created.
    **Note:** If the Cloud Assistant client is not installed on your instance, the client is automatically installed when the instance snapshot is created after you select **Enable Application-consistent Snapshot**.

5.  Click **OK**.

    After the instance snapshot is created, you can choose **Storage & Snapshots** \> **Snapshots** in the left-side navigation pane and click the **Instance Snapshots** tab to view the snapshot.

    You can also click the **Snapshots** tab to check whether the created snapshot is an application-consistent snapshot or a file-system consistent snapshot based on the tag. Application-consistent snapshots have the `APPConsistent:True` tag. File-system consistent snapshots have the `FsConsistent: True` tag.


## Step 2: Enable the application-consistent snapshot feature for Linux instances

For Linux instances, you must configure shell scripts \(application pre-freeze and post-thaw scripts\) based on the applications in the instance to implement application consistency. This section describes how to enable the application-consistent snapshot feature for a Linux instance.

1.  Write the application pre-freeze and post-thaw scripts based on the applications in the instance and upload the scripts to the instance.

    You can use the FTP service or Cloud Assistant to upload the application pre-freeze and post-thaw scripts to the instance.

    -   Application pre-freeze script: Configure the script to allow only the root user to have the read, write, and execute permissions on the script. Set the save path to /tmp/prescript.sh.
    -   Application post-thaw script: Configure the script to allow only the root user to have the read, write, and execute permissions on the script. Set the save path to /tmp/postscript.sh.
    **Note:** If the script configurations such as permissions, save path, or file name are invalid, a file-system consistent snapshot is created.

2.  Go to the Instances page.

    1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

    2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

    3.  In the top navigation bar, select the region where the ECS instance on which you want to perform operations is located.

3.  Find the instance for which you want to enable the application-consistent snapshot feature and choose **More** \> **Disk and Image** \> **Create Instance Snapshot** in the Actions column.

4.  In the **Create Instance Snapshot** dialog box, configure the parameters for the instance snapshot and enable the instant access feature.

    -   For more information about the parameters of the instance snapshot, see [Create snapshots for multiple disks together by creating an instance snapshot](/intl.en-US/Snapshots/Use instance snapshots/Create snapshots for multiple disks together by creating an instance snapshot.md).
    -   For more information about the instant access feature, see [Enable or disable the instant access feature](/intl.en-US/Snapshots/Use snapshots/Enable or disable the instant access feature.md).
5.  In the **Create Instance Snapshot** dialog box, specify Application-consistent Snapshot.

    -   If you select **Enable Application-consistent Snapshot** and **Enable File System Freeze and Thaw** and configure valid scripts, an application-consistent snapshot is created.
    -   If you select **Enable Application-consistent Snapshot** and **Enable File System Freeze and Thaw** but do not configure valid scripts, a file-system consistent snapshot is created.
    **Note:** If the Cloud Assistant client is not installed on your instance, the client is automatically installed when the instance snapshot is created after you select **Enable Application-consistent Snapshot**.

6.  Click **OK**.

    After the instance snapshot is created, you can choose **Storage & Snapshots** \> **Snapshots** in the left-side navigation pane and click the **Instance Snapshots** tab to view the snapshot.

    You can also click the **Snapshots** tab to check whether the created snapshot is an application-consistent snapshot or a file-system consistent snapshot based on the tag. Application-consistent snapshots have the `APPConsistent:True` tag. File-system consistent snapshots have the `FsConsistent: True` tag.


