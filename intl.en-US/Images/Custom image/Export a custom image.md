# Export a custom image

You can export a new custom image to an OSS bucket and download the image to local computers. This topic describes how to export custom images and what precautions must be taken.

-   An OSS bucket is available within the same region as the custom image to be exported.

    If you have not created any OSS buckets, create one. For more information, see [Create buckets](/intl.en-US/Quick Start/Create buckets.md).

    **Note:** When you export a custom image, OSS storage and traffic fees are incurred for image download. For more information, see [Overview](/intl.en-US/Pricing/Billing items and methods/Overview.md).

-   The custom image to be exported meets the following requirements:
    -   It is not created based on an Alibaba Cloud Marketplace image.
    -   It does not contain a Windows Server operating system.
    -   It does not contain snapshots of more than four data disks. The size of each data disk does not exceed 500 GiB.

        **Note:** If the capacity of a data disk exceeds 500 GiB, you must distribute the data on the disk to multiple data disks that are smaller than 500 GiB in size and then create and export custom images from these smaller data disks.


Before you export a custom image, take note of the following points:

-   The amount of time it takes to export a custom image depends on the size of the image and the number of concurrent tasks in the queue.
-   If an exported custom image contains data disk snapshots, multiple objects appear in your OSS bucket.

    Objects whose names contain system are system disk snapshots. Objects whose names contain data are data disk snapshots. The identifier of a data disk snapshot is the mount point of the source data disk, such as xvdb and xvdc.

-   To use the exported image to create identical Linux instances, make sure that the storage location and storage space division of files recorded in /etc/fstab are consistent with the exported data disk snapshot information.
-   If the cloud disk does not contain any data when the custom image is created, the decompressed image file also does not contain any data.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.

3.  In the top navigation bar, select a region.

4.  Authorize ECS to access OSS.

    1.  Choose **More** \> **Export Image** in the **operation** column corresponding to an image.

    2.  In the Export Image dialog box, click **Verify** in the notes.

        ![Export an image](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4073559951/p4655.png)

    3.  In the Cloud Resource Access Authorization dialog box, click **Confirm Authorization Policy** to allow ECS to access your OSS resources.

5.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.

6.  On the **Custom Images** tab, find the image that you want to export and choose **More** \> **Export Image** in the **Actions** column.

7.  In the Export Image dialog box, configure the following parameters:

    -   Image Format: Select a format in which to export the custom image. Valid values: RAW, VHD, QCOW2, VDI, and VMDK.

        **Note:** The select image export format feature is currently available in some regions and will be made available in more regions in the future.

    -   OSS Bucket Address: Select an OSS bucket that belongs to the same region as the custom image.
    -   OSS Object Prefix: Set the prefix of the object name for the custom image. For example, if you set OSS Object Prefix to Demo, the exported image is named Demo-<Automatically generated object name\>.
8.  Click **OK** to export the custom image.

    You can cancel an image export task at any time before the task is complete. Go to the [Tasks](https://ecs.console.aliyun.com/#/task/region/cn-qingdao) page in the ECS console, find the corresponding task in the specified region, and cancel the task.


Download the custom image. For more information, see [Download objects](/intl.en-US/Console User Guide/Upload, download, and manage objects/Download objects.md).

**Note:** If you select the RAW image format, the default file name extension of the exported custom image is .raw.tar.gz, and the file name extension of the decompressed image is .raw. If your local computer runs a Mac OS X operating system, we recommend that you use GNU Tar to decompress the image.

**Related topics**  


[ExportImage](/intl.en-US/API Reference/Images/ExportImage.md)

[CancelTask](/intl.en-US/API Reference/Others/CancelTask.md)

