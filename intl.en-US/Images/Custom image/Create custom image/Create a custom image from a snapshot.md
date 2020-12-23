---
keyword: [custom image, replication environment, preparation, deployment with source code, ECS]
---

# Create a custom image from a snapshot

You can create a custom image from a snapshot that contains the operating system and data of an ECS instance. Then, you can use the custom image to create multiple identical instances.

A system disk snapshot is created. For more information, see [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).

![demo](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6863559951/p4584.png)

Before you create custom images from snapshots, take note of the following points:

-   Notes on snapshots used to create custom images:
    -   A custom image can be created from a system disk snapshot or from a system disk snapshot and one or more data disk snapshots. Data disk snapshots alone cannot be used to create custom images.
    -   Both encrypted and unencrypted snapshots can be used to create custom images.
    -   If the ECS instance from which a snapshot was created expires or is released, the custom image created from the snapshot and the ECS instance created from the image are not affected.
-   Notes on custom images:
    -   Custom images cannot be used across regions. However, you can copy custom images from one region to another for later use. For more information, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md).
    -   Custom images are independent of the billing methods of the ECS instances from which the custom images were created. For example, custom images created from subscription ECS instances can be used to create pay-as-you-go instances.
-   Notes on ECS instances created from custom images:
    -   You can upgrade the configurations of ECS instances created from custom images, such as vCPUs, memory, bandwidth, and disks.
    -   You can replace the operating systems of ECS instances created from custom images, and the custom image remains usable. For more information, see [Replace the system disk \(non-public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace a system disk (non-public images).md).
    -   Unreachable network errors may occur after you use a custom image to create VPC-type ECS instances that run the Linux operating system. The errors may be caused by the configurations in /etc/sysconfig/network. For more information, see [How to solve unreachable network errors when a VPC-type instance is created from a custom image](https://www.alibabacloud.com/help/en/doc-detail/140417.htm).
-   Recommendations for data security:
    -   For information about how to enhance the security of custom images, see [Security suggestions for Alibaba Cloud custom images](https://www.alibabacloud.com/help/zh/faq-detail/54903.htm?spm=a2c63.q38357.a3.3.3a4b61feRLos9d).
    -   Delete sensitive data from a snapshot in advance to enhance data security.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  Use one of the following methods to find the system disk snapshot from which you want to create a custom image:

    -   On the Instances page
        1.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
        2.  In the top navigation bar, select a region.
        3.  Find the instance. Click the instance ID or click **Manage** in the **Actions** column. The Instance Details tab appears.
        4.  Click the **Snapshot** tab. Find the snapshot whose **Disk Type\(All\)** is **System Disk**. Click **Create Custom Image** in the **Actions** column.
    -   On the Snapshots page
        1.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Snapshots**.
        2.  In the top navigation bar, select a region.
        3.  Find the snapshot whose **Disk Type\(All\)** is **System Disk**. Click **Create Custom Image** in the Actions column.

            ![snapshot_systemdisk](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6067934061/p4593.png)

3.  In the **Create Custom Image** dialog box, configure the following parameters.

    |Parameter|Description|Reference|
    |---------|-----------|---------|
    |**System Snapshot ID**|The snapshot must be a system disk snapshot.|N/A|
    |Custom Image Name and Custom Image Description|Enter a name and description for the custom image to be created.|N/A|
    |**Add Data Disk Snapshot**|Optional. Select **Add Data Disk Snapshot**, click **Add**, and then select the ID of a data disk snapshot.     -   If you do not select the ID of any data disk snapshot, an empty data disk is created with a default capacity of 5 GiB.
    -   If you select the ID of a data disk snapshot, the resulting disk capacity is the same as the snapshot size.
|[Snapshot overview](/intl.en-US/Snapshots/Snapshot overview.md)|
    |**Tag**|Select a tag.     -   Optional: In most scenarios, the tag is optional.
    -   Required: When you log on as a RAM user bound with an authorization policy that requires tags, you must specify a tag. Otherwise, an error is reported, indicating insufficient permissions.
|[Create a resource with a specific tag](/intl.en-US/Tag & Resource/Tags/Create a resource with a specific tag.md)|

    ![create_custom_image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7863559951/p41259.png)

4.  Click **Create**.


After the custom image is created, you can perform the following operations:

-   [Create an ECS instance by using a custom image](/intl.en-US/Instance/Create an instance/Create an ECS instance by using a custom image.md)
-   [Replace a system disk \(non-public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace a system disk (non-public images).md)

**Related topics**  


[CreateImage](/intl.en-US/API Reference/Images/CreateImage.md)

