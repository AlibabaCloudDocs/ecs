---
keyword: [UUID conflict, modify the UUID, mount error]
---

# Modify the UUID of a disk

If you create a disk from a snapshot of a disk on a Linux instance and attach the created disk to the Linux instance, the universally unique identifier \(UUID\) of the disk conflicts with that of the disk from which the snapshot is created. This topic describes how to modify the UUID of a disk.

After a disk is created from a snapshot of a disk on a Linux instance, the UUID of the created disk is the same as that of the disk from which the snapshot is created. If you attach the created disk to the Linux instance, the UUID of the disk conflicts with that of the disk from which the snapshot is created. The following issues may occur:

-   If you create a disk from a system disk snapshot of a Linux instance and attach the created disk to the Linux instance, Linux may be started from the newly attached data disk rather than the system disk.
-   If your disk uses the XFS file system, the mount operation is prohibited due to a UUID conflict. The `"mount: wrong fs type, bad option, bad superblock on /dev/vdd1,"` message appears.

Therefore, after you create a disk from a snapshot of a disk on a Linux instance and attach the created disk to the Linux instance in the console, you must log on to the instance to modify the UUID of the created disk before you perform the mount operation. To modify the UUID of your disk, you can run the `blkid` command to query its file system type and choose one of the following methods based on the command output:

-   If the command output is `TYPE="ext4"`, `TYPE="ext3"`, or `TYPE="ext2"`, see [Modify the UUID of an ext2, ext3, or ext4 file system](#section_gqh_rma_fsw).
-   If the command output is `TYPE="xfs"`, see [Modify the UUID of an XFS file system](#section_qw6_51s_l6y).

## Modify the UUID of an ext2, ext3, or ext4 file system

**Note:** In this example, /dev/vdb1 is used. You must modify the related commands based on your device name.

1.  Remotely connect to an ECS instance. For more information, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

2.  Run the following command to query the UUID of the created disk:

    ```
    blkid
    ```

    The following command output shows that the UUID of the disk created from a snapshot is the same as that of the disk from which the snapshot is created.

    ![The UUID information](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7139898161/p210223.png)

3.  Run the following command to check the file system:

    ```
    e2fsck -f /dev/vdb1
    ```

4.  Run the following command to generate a new UUID for the created disk:

    ```
    uuidgen | xargs tune2fs /dev/vdb1 -U
    ```

5.  Run the following command to check whether the UUID is modified:

    ```
    blkid
    ```

    The following command output shows that the UUID of /dev/vdb1 is modified.

    ![The UUID is changed](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7139898161/p210347.png)

6.  Run the following command to attach the created disk:

    ```
    mount /dev/vdb1 /mnt
    ```

7.  Configure the /etc/fstab file to automatically attach the created disk on startup.

    For information about how to configure the /etc/fstab file, see [t2000719.md\#]().


## Modify the UUID of an XFS file system

**Note:** In this example, /dev/vdd1 is used. You must modify the related commands based on your device name.

1.  Remotely connect to an ECS instance. For more information, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

2.  Run the following command to query the UUID of the created disk:

    ```
    blkid
    ```

    The following command output shows that the UUID of the disk created from a snapshot is the same as that of the disk from which the snapshot is created.

    ![xfs-uuid](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7139898161/p210365.png)

3.  Run the following command to generate a new UUID for the created disk:

    ```
    xfs_admin -U generate /dev/vdd1
    ```

4.  Run the following command to check whether the UUID is modified:

    ```
    blkid
    ```

    The following command output shows that the UUID of /dev/vdd1 is modified.

    ![The UUID result - XFS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7139898161/p210558.png)

5.  Run the following command to attach the created disk:

    ```
    mount /dev/vdd1 /mnt
    ```

6.  Configure the /etc/fstab file to automatically attach the created disk on startup.

    For information about how to configure the /etc/fstab file, see [t2000719.md\#]().


## References

-   [Create a disk from a snapshot](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk from a snapshot.md)
-   [t2000719.md\#]()

