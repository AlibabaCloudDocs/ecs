# Common image formats

ECS allows you to import images in multiple formats. This topic compares the QCOW2, VHD, and RAW formats supported by ECS.

The following table describes the common image formats.

|Format|Description|Feature|
|------|-----------|-------|
|QCOW2|QCOW2 is a virtual machine image format implemented by QEMU, which can represent a fixed-size block device-type disk in the form of a file.

|-   Occupies a smaller amount of disk space.
-   Supports copy-on-write \(CoW\). Image files reflect only the underlying disk changes.
-   Supports snapshots and can contain multiple snapshots.
-   Supports compression and encryption. You can compress data by using zlib and encrypt data by using AES. |
|VHD|VHD is a virtual disk file format provided by Microsoft. Files in the VHD format can be compressed into a single file and stored on the file system of a physical host. It includes the file systems required to start ECS instances.

|-   Simple maintenance. You can partition, format, compress, and delete physical partitions without affecting them.
-   Easy backup. You can back up only the created VHD files. You can also use a backup tool to back up the entire physical partition where the VHD files reside.
-   Easy migration. If you want to use a VHD file on multiple computers, you can detach the VHD file, copy it to the destination computer, and then attach it.
-   Availability for system deployment. You can use the Imagex tool to release captured images to VHD virtual disks or use Windows Deployment Services \(WDS\) servers to deploy the system to VHD virtual disks. |
|RAW|RAW files can be directly read and written by ECS instances. RAW is a format that provides the optimal performance and does not allow the space to dynamically grow.

|-   Simple addressing and high access efficiency.
-   You can convert RAW to other formats by using format conversion tools.
-   RAW files can be mounted by physical hosts. You can perform data transfer between RAW files and hosts without the need to start virtual machines. |

