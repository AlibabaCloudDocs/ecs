---
keyword: [format, Alibaba Cloud, ECS, partition a disk for a Linux instance]
---

# Format a data disk for a Linux instance

After you attach a new data disk to an ECS instance, you must create at least one file system on the data disk and mount the file system. In this example, an I/O optimized instance that runs the Alibaba Cloud Linux 2.1903 LTS 64-bit operating system is used. A new 20 GiB data disk is attached to the instance. The device name of the data disk is /dev/vdb. A single master boot record \(MBR\) partition is created on the data disk and an ext4 file system is mounted.

Data disks that you purchased separately are attached to ECS instances. If you purchased data disks with ECS instances, skip the attach operation. For more information, see [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md).

**Note:** The attach operation refers to attaching disks to ECS instances in the ECS console, instead of mounting file systems by running the mount command within the operating systems of ECS instances.

The following procedure applies only to data disks of up to 2 TiB in size. Data disks larger than 2 TiB must be partitioned in the GPT format. For more information, see [Partition and format a data disk larger than 2 TiB](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Partition and format a data disk larger than 2 TiB.md).

By default, the device names of data disks are assigned by the system based on the following naming conventions:

-   Device names of data disks for I/O optimized instances ascend from /dev/vdb to /dev/vdz.
-   Device names of data disks for non-I/O optimized instances ascend from /dev/xvdb to /dev/xvdz.

The following section describes the risks of formatting a data disk:

-   Disk partitioning and formatting are high-risk operations. Exercise caution when you partition and format disks. The procedure in this topic applies only to new data disks. If your data disk contains data, create a snapshot for the data disk to avoid data loss. For more information, see [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).
-   Only **data disks** can be partitioned. You cannot partition **system disks**. If you use a third-party tool to forcibly partition a system disk, unknown risks such as system failures and data loss may occur. You can extend partitions or add new partitions only for system disks that have been extended. For more information, see [Resize disks online for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Linux instances.md).

**Note:** The commands in the example also apply to CentOS 7.

## Step 1: Create MBR partitions for a data disk

1.  Connect to an ECS instance.

    For more information, see [Connect to a Linux instance by using VNC](/intl.en-US/Instance/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using VNC.md).

2.  View information about the data disks attached to the ECS instance.

    Run the following command:

    ```
    fdisk -l
    ```

    A command output similar to the following one is returned:

    ![Format disk_fdisk](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3233158061/p173584.png)

    **Note:** If /dev/vdb is not displayed in the command output, the ECS instance does not have data disks. Check whether data disks are attached to the instance. For information about how to attach a data disk, see [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md).

3.  Run the following commands in sequence to create a single partition for the data disk.

    1.  Run the following command to partition the data disk:

        ```
        fdisk -u /dev/vdb
        ```

    2.  Enter p to view the partition information of the data disk.

        In this example, the data disk is not partitioned.

    3.  Enter n to create a new partition.

    4.  Enter p to set the partition as a primary partition.

        **Note:** When you create a single partition for a data disk, the partition must be a primary partition. If you want to create four or more partitions, enter e \(extended\) at least once to create at least one extended partition.

    5.  Enter the partition number and press the Enter key.

        In this example, only one partition is created. Press the Enter key to use the default value 1.

    6.  Enter the number of the first available sector and press the Enter key.

        In this example, press the Enter key to use the default value 2048.

    7.  Enter the number of the last sector and press the Enter key.

        In this example, only one partition is created. Press the Enter key to use the default value.

    8.  Enter p to view the intended partitions of the data disk.

    9.  Enter w to start partitioning, and exit after partitioning is complete.

    The following figure shows the result of running the commands.

    ![Partition creation result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3233158061/p173593.png)

4.  View the information of the new partition.

    Run the following command:

    ```
    fdisk -lu /dev/vdb
    ```

    A command output similar to the following one is returned. If the information of /dev/vdb1 is displayed, the new partition is created.

    ![Partition result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4233158061/p173602.png)


## Step 2: Create a file system for the partition

Run one of the following commands to create a file system on the new partition.

-   Run the following command to create an ext4 file system:

    ```
    mkfs -t ext4 /dev/vdb1
    ```

-   Run the following command to create an xfs file system:

    ```
    mkfs -t xfs /dev/vdb1
    ```


In this example, an ext4 file system is created.

![Create a file system](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1749728061/p173624.png)

## Step 3: Configure the /etc/fstab file and mount the partition

Write the information of the new partition to /etc/fstab to enable this partition to be automatically mounted on instance startup.

**Note:** We recommend that you use a universally unique identifier \(UUID\) to reference the new partition in /etc/fstab.

1.  Back up /etc/fstab.

    Run the following command:

    ```
    cp /etc/fstab /etc/fstab.bak
    ```

2.  Write the information of the new partition to /etc/fstab.

    -   If you are a root user, you can run the following command to modify /etc/fstab:

        ```
        echo `blkid /dev/vdb1 | awk '{print $2}' | sed 's/\"//g'` /mnt ext4 defaults 0 0 >> /etc/fstab
        ```

        **Note:**

        -   The Ubuntu 12.04 operating system does not support barriers. You must run the `echo '`blkid /dev/vdb1 | awk '{print $3}' | sed 's/\"//g'` /mnt ext4 barrier=0 0 0' >> /etc/fstab` command to write the information of the new partition to /etc/fstab.
        -   You can separately mount the data disk as a folder to store web pages. In this case, the `/mnt` portion of the command must be replaced with the intended mount point folder path.
    -   If you are a common user, you can manually modify /etc/fstab.
        1.  Run the following command to query the UUID of the new partition:

            ```
            sudo blkid /dev/vdb1
            ```

            A command output similar to the following one is returned:

            ```
            /dev/vdb1: UUID="05779a4e-f04f-4eca-97ac-57fd1fda****" TYPE="ext4"
            ```

        2.  Run the following command to edit /etc/fstab:

            ```
            sudo vi /etc/fstab
            ```

        3.  Enter i to enter the editing mode:
        4.  Write the information of the new partition to /etc/fstab. Change the UUID value to the value you obtained in Step i.

            ```
            UUID=05779a4e-f04f-4eca-97ac-57fd1fda**** /mnt ext4 defaults 0 0
            ```

        5.  Press the Esc key, enter :wq, and then press the Enter key to save your changes and exit the editing mode.
3.  View the information of the new partition in /etc/fstab.

    Run the following command:

    ```
    cat /etc/fstab
    ```

    A command output similar to the following one is displayed:

    ![Query fstab](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4233158061/p173707.png)

4.  Mount the new partition.

    Run the following command:

    ```
    mount /dev/vdb1 /mnt
    ```

5.  Check the mount result.

    Run the following command:

    ```
    df -h
    ```

    A command output similar to the following one is returned. If the information of the new file system is displayed, the file system is mounted.

    ![Query the mount result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4233158061/p173729.png)


