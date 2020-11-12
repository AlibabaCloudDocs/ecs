# Create a hard link across project quotas

By default, the ext4 file system has constraints, and you are not allowed to create hard links across project quotas. However, in practice, some scenarios require hard links to be created. Alibaba Cloud Linux 2 provides a custom interface that can bypass the constraints of the ext4 file system to create hard links across project quotas. This topic describes the interface and provides an example of how to use the interface.

Linux distributions support the following disk quota modes: user quota, group quota, and project quota. Project quotas provide more fine-grained disk quotas than user or group quotas. Project quotas identify directories and files within file systems by project ID. This topic describes how to create a hard link across project ID directories in an ext4 file system.

## Interface description

The default value of the /proc/sys/fs/hardlink\_cross\_projid interface is 0. In this case, hard links cannot be created across project quotas. If the /proc/sys/fs/hardlink\_cross\_projid interface is set to 1, you can bypass the constraints of the ext4 file system to create hard links across project quotas.

For more information about the interface, see `Documentation/sysctl/fs.txt`. You can obtain the kernel document from the Debuginfo package and the source code package of Alibaba Cloud Linux 2. For more information, see [Use Alibaba Cloud Linux 2](/intl.en-US/Images/Alibaba Cloud Linux 2/Overview.md).

## Example

You can run the following command to query the value of the /proc/sys/fs/hardlink\_cross\_projid interface:

```
cat /proc/sys/fs/hardlink_cross_projid
```

A value of `0` is returned, indicating that hard links cannot be created across project quotas.

You can change the value from 0 to 1 so that you can create hard link across project quotas.

```
echo 1 > /proc/sys/fs/hardlink_cross_projid
```

