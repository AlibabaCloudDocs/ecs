---
keyword: [share images, unshare images, share images across regions]
---

# Share or unshare custom images

This topic describes how to share or unshare custom images. Shared images can be used to deploy ECS instances across accounts. After you create a custom image, you can share it with other Alibaba Cloud accounts. The other Alibaba Cloud accounts can create ECS instances from the shared image. You can also unshare custom images from Alibaba Cloud accounts.

Before you share an image, ensure that all sensitive data and files have been removed from the image.

Images shared with an account do not count towards the image quota for the account. The account is not charged for these shared images.

When the account uses an image shared by you to create ECS instances, you are not charged for but the account is charged for the created instances. For more information about the billing of shared images, see the "Image types" section in [Image Overview](/intl.en-US/Images/Image overview.md).

The account can use the images shared with it but cannot delete these shared images directly. You must unshare an image before you can delete it. For more information, see [Delete a custom image](/intl.en-US/Images/Custom image/Delete a custom image.md).

Before you share an image, take note of the following items:

-   You can share only the custom images that are created in your account. You cannot share custom images that are created and shared by other accounts.
-   Each custom image can be shared with up to 50 accounts.
-   You can share images between the accounts on the China \(aliyun.com\), International \(alibabacloud.com\), and Japan \(jp.alibabacloud.com\) sites. However, the custom images that are created based on Alibaba Cloud Marketplace images cannot be shared.
-   Custom images cannot be shared across regions. If you want to share a custom image across regions, you must copy the image to the destination region first. For more information, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md).
-   ECS does not guarantee the integrity and security of shared images. Before you use shared images, ensure that the images come from trusted accounts. You must assume all risks.

## Share a custom image

You can perform the following operations to share your custom image with an Alibaba Cloud account.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.

3.  In the top navigation bar, select a region.

4.  On the **Custom Images** tab, select the custom image that you want to share. Click **Share Image** in the **Actions** Column.

5.  In the **Share Image** dialog box, enter the ID of the account with which you want to share the image, and select the option under the Account field. Then, click **Share Image**.

    To obtain the account ID, move the pointer over the Avatar in the upper-right corner of the Alibaba Cloud Management console. Click **Security Settings** tab. The account ID is displayed on the **Security Settings** page.

    After you share a custom image with an account, the account can view the shared image in the ECS console by choosing **Instances & Images** \> **Images** and then clicking **Shared Images** tab in the same region as that you previously selected. The account can perform the following operations:

    -   Create one or more ECS instances from the shared image.

        When the account creates an ECS instance, it can select Share Image and then select the shared image in the Image section. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

    -   Replace the system disk of an ECS instance with the shared image.

        For more information, see [Replace a system disk \(non-public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace a system disk (non-public images).md).


## Unshare custom images

You can perform the following operations to unshare your custom image from an Alibaba Cloud account.

**Note:** After you unshare a custom image from an account:

-   The account is no longer able to query the image by using the ECS console or by calling the API operation.
-   The account is no longer able to create ECS instances or replace the system disk by using the image.
-   The system disks of ECS instances that were created from the shared image cannot be re-initialized.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.

3.  In the top navigation bar, select a region.

4.  On the **Custom Images** tab, select the custom image that you want to unshare. Choose **More \> Share Image** in the **Actions** column.

5.  In the **Share Image** dialog box, find the ID of the account from which you want to unshare the image and click **Cancel Sharing** in the Actions column.


**Related topics**  


[ModifyImageSharePermission](/intl.en-US/API Reference/Images/ModifyImageSharePermission.md)

[DescribeImageSharePermission](/intl.en-US/API Reference/Images/DescribeImageSharePermission.md)

