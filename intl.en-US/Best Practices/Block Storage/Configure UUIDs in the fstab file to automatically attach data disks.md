# Configure UUIDs in the fstab file to automatically attach data disks

In Linux, you can configure the fstab file to automatically attach data disks on the startup of an ECS instance. If the fstab file is inappropriately configured and the attach sequence of your disks is changed, the ECS instance may not run properly after it is restarted. This topic describes how to configure universally unique identifiers \(UUIDs\) in the fstab file to automatically attach data disks. This can handle the preceding restart exception.

The disks to be attached to the instance are partitioned and formatted. For more information, see [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md).

fstab allows you to identify a file system by using a disk partition name such as/dev/vdb1 or by using a UUID. The following section describes the differences between the two methods:

-   When you use disk partition names to identify file systems in the fstab file, the disk partitions may not be mounted to the original mount points if the attach sequence of the disks is changed. In this case, applications that run on your ECS instance may be affected.
-   When you use UUIDs to identify file systems in the fstab file, the disk partitions can still be mounted to the original mount points if the attach sequence of the disks is changed. Therefore, we recommend that you use UUIDs to identify file systems.

## Procedure

1.  Connect to the instance.

    For information about how to connect to an ECS instance, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

2.  Run the following command to view information of the disks to be attached to the instance:

    ```
     fdisk -lu
    ```

    A command output similar to the following one is displayed.

    ![Query the disks](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4020998161/p187006.png)

3.  Run the following command to query the UUIDs of the disks:

    ```
    blkid
    ```

    A command output similar to the following one is displayed.

    ![Query the UUIDs](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4020998161/p187034.png)

4.  Run the following commands to create the mount points for the data disks:

    -   Create the /test01 mount point for /dev/vdb1:

        ```
        mkdir /test01
        ```

    -   Create the /test02 mount point for /dev/vdc1:

        ```
        mkdir /test02
        ```

5.  Add the mount information to the fstab file.

    1.  Run the following command to edit the fstab file:

        ```
        vi /etc/fstab
        ```

    2.  Press the `I` key to enter the edit mode.

    3.  Add the following mount information:

        ```
        UUID=59f23670-94c1-42d1-8bb0-209d7854****   /test01     ext4    defaults     0   0
        UUID=88619b1a-d971-41c2-91d0-3a440fc0****   /test02     xfs     defaults     0   0
        ```

        A command output similar to the following one is displayed.

        ![Description of the fstab file](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3736915161/p187115.png)

        |No.|Section|Description|
        |---|-------|-----------|
        |1|<file system\>|The partitions to be mounted.We recommend that you use the UUIDs of the file systems. You can run the `blkid` command to query the UUIDs of the file systems. |
        |2|<dir\>|The mount points of the partitions.You can create mount points. In this topic, the /test01 and /test02 mount points are created. |
        |3|<type\>|The types of file systems to be mounted to the partitions.You can run the `blkid` command to query the types of the file systems. |
        |4|<options\>|The parameters used for mounting. Typically, the defaults parameter is used. If you want to use multiple parameters, separate them with commas \(,\). Example: `defaults,noatime`.For more information about the <options\> parameters, visit [fstab](https://wiki.debian.org/fstab). |
        |5|<dump\>|Indicates whether the dump tool backs up the file systems.        -   0: The dump tool does not back up the file systems.
        -   1: The dump tool backs up the file systems.
Typically, the dump tool is not used. In this case, this parameter is set to 0. |
        |6|<pass\>|The priority in which fsck checks the file systems.        -   0: The file systems are not checked.
        -   1: The root file system is checked.
        -   2: All file systems except the root one are checked.
Typically, this parameter is set to 0. |

    4.  Press the `Esc` key to exit the edit mode after the preceding information is configured.

    5.  Enter `:wq` and press the `Enter` key to save and exit the file.

6.  Run the following command to view the fstab file:

    ```
    cat /etc/fstab
    ```

    A command output similar to the following one is displayed.

    ![Query fstab](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3736915161/p187136.png)

7.  Run the following commands to attach the data disks:

    -   To attach /dev/vdb1, run the following command:

        ```
        mount /dev/vdb1 /test01
        ```

    -   To attach /dev/vdc1, run the following command:

        ```
        mount /dev/vdc1 /test02
        ```

8.  Run the following command to check whether the data disks are attached:

    ```
    df -h
    ```

    A command output similar to the following one is displayed.

    ![Command output](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4020998161/p187224.png)


After the fstab file is configured, the system automatically attaches the data disks after you restart the ECS instance.

## FAQ

[System startup exceptions due to the configuration error of the /etc/fstab file on Linux instances](https://help.aliyun.com/knowledge_detail/41460.html)

