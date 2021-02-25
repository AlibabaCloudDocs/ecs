# Create a custom image from an instance

After you create an instance, you can perform operations to customize the instance such as installing software and deploying application environments and create a custom image for the updated instance. Instances created from the custom image contain all of the configured items, which saves you the trouble of configuring these items for each new instance.

Sensitive data is deleted from the instance to enhance data security.

Before you create a custom image from a Linux instance, take note of the following items:

-   Check the network configuration of the instance based on your Linux version. For more information, see [How to solve unreachable network errors when a VPC-type instance is created from a custom image](https://www.alibabacloud.com/help/en/doc-detail/140417.htm).
-   The system disk has a sufficient amount of free space.

When you create a custom image from an instance, a snapshot is generated for each disk in the instance. Together, all of the snapshots constitute a complete custom image, as shown in the following figure.

![custom_image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8863559951/p4599.png)

Before you create a custom image from an instance, take note of the following items:

-   When you create a custom image from an instance, you do not need to stop the instance.
-   When you create a custom image from an instance, the status of the instance cannot be changed. For example, if you stop, start, or restart an instance, the custom image fails to be created.
-   You cannot create images for subscription instances that have expired. You can create a snapshot for the system disk of an instance and then use the snapshot to create a custom image.
-   You cannot create images for released instances. If you have saved a system disk snapshot for an instance, you can use the snapshot to create a custom image.
-   Custom images are located within the same region as the instances from which the images are created. For example, if an instance is located in the China \(Hangzhou\) region, the image created from the instance is also located in the China \(Hangzhou\) region. For more information about how to use images across regions, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md).
-   The amount of time it takes to create an image depends on the size of the disk from which the image is created.

When you create a custom image from a Linux instance, take note of the following items:

-   Do not upload data disk information to the /etc/fstab file. Otherwise, instances created from the image cannot be started.
-   Do not update the kernel or operating system version.
-   Do not adjust the system disk partitions. Only disks with a single root partition are supported.
-   Do not modify critical system files such as /sbin, /bin, and /lib.
-   Do not modify the default logon username root.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance for which you want to create a custom image. In the **Actions** column, choose **More** \> **Disk and Image** \> **Create Custom Image**.

5.  Enter an image name and description.

6.  Click **Create**.

    **Note:** The image can be used only after snapshots of all disks are created. Image creation may take a while.


After you create a custom image, you can:

-   [Create an instance by using a custom image](/intl.en-US/Instance/Create an instance/Create an ECS instance by using a custom image.md)
-   [Share custom images](/intl.en-US/Images/Custom image/Share or unshare custom images.md)
-   [Export a custom image](/intl.en-US/Images/Custom image/Export a custom image.md)

**Related topics**  


[Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md)

[Modify custom images](/intl.en-US/Images/Custom image/Modify custom images.md)

[CreateImage](/intl.en-US/API Reference/Images/CreateImage.md)

