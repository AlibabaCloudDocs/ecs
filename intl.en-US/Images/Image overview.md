# Image overview

An ECS image stores information that is required to create an ECS instance. You must select an image when you create an ECS instance. An image works as a copy that stores data from one or more disks. An ECS instance image may store data from a system disk or from both system and data disks.

## Image types

ECS images are classified into public images, custom images, shared images, and Alibaba Cloud Marketplace images based on image sources.

-   Public images

    Public images provided by Alibaba Cloud are licensed, secure, and stable. Public images include Windows Server system images and mainstream Linux system images. For more information, see [Public images](/intl.en-US/Images/Public image/Overview.md).

-   Custom images

    Custom images are created from instances or snapshots, or imported from your local device. For more information, see [Custom images](/intl.en-US/Images/Custom image/Overview.md).

-   Shared images

    Shared images are shared with you by other Alibaba Cloud accounts. For more information, see [Shared images](/intl.en-US/Images/Custom image/Share or unshare custom images.md).

-   Alibaba Cloud Marketplace images

    Alibaba Cloud Marketplace images are classified into the following types based on their providers:

    -   Images provided by Alibaba Cloud
    -   Images provided by independent software vendors \(ISVs\) that are licensed by Alibaba Cloud Marketplace
    An Alibaba Cloud Marketplace image contains an operating system and pre-installed software. The operating system and pre-installed software are tested and verified by the ISV and Alibaba Cloud to ensure that the image is safe to use. For more information, see [Alibaba Cloud Marketplace images](/intl.en-US/Images/Alibaba Cloud Marketplace images.md).


## Image prices

You may be charged for using images. The following table describes the billing methods of different types of images.

|Type|Price|
|:---|:----|
|Public image|Some public images are billed while others are free of charge.

-   Windows Server: The price is subject to the instance type that you choose. The price information is displayed on the buy page when you create an instance.
-   Red Hat Enterprise Linux: This image is a paid image. The price information is displayed on the buy page when you create an instance.
-   Public images that run other operating systems are free of charge.

**Note:** Public images that run Windows Server are licensed and maintained by Microsoft. Public images that run Red Hat Enterprise Linux are licensed and maintained by Red Hat. |
|Custom image|Custom images are billed differently in the following situations:

-   If a custom image is derived from a free image, you are charged for storage of the snapshots contained in the custom image.
-   If a custom image is derived from a payable image, you are charged for storage of the snapshots contained in the custom image. If you create an instance from the custom image, you are also charged for using the image.

**Note:** If a custom image is derived from an Alibaba Cloud Marketplace image, the custom image is billed based on the billing methods provided in Alibaba Cloud Marketplace. |
|Shared image|Shared images are billed differently in the following situations:

-   If an image shared with you by another Alibaba Cloud account is derived from a free image, you can use the shared image free of charge.
-   If an image shared with you by another Alibaba Cloud account is derived from a payable image and you create an ECS instance from the shared image, you are charged for using the payable image.

**Note:** If a shared image is derived from an Alibaba Cloud Marketplace image, the shared image is billed based on the billing methods provided in Alibaba Cloud Marketplace. |
|Alibaba Cloud Marketplace image|Alibaba Cloud Marketplace images are billed based on the billing methods provided in Alibaba Cloud Marketplace.|

For more information, see [Billing overview](/intl.en-US/Pricing/Billing overview.md) and the "FAQ about commercial availability of images" section in [Image FAQ](/intl.en-US/Images/Image FAQ.md).

## Select and find images

You can select an image based on the region, image type, image price, operating system, and built-in software. For more information, see [Select an image](/intl.en-US/Images/Select an image.md).

You can find an image based on its type, name, ID, or the ID of the snapshot from which the image is created. Then, you can use the image to create an instance or perform other operations. For more information, see [Find an image](/intl.en-US/Images/Find an image.md).

## Replace the image of an ECS instance

After you create an ECS instance, you can change its operating system by replacing the system disk of the instance.

-   You can replace the image with a public image by replacing the system disk of the instance. For more information, see [Replace the system disk \(public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace the system disk (public images).md).
-   You can also replace the image with a non-public image such as a custom, shared, or Alibaba Cloud Marketplace image by replacing the system disk of the instance. For more information, see [Replace a system disk \(non-public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace a system disk (non-public images).md).

## API operations

You can also call API operations to manage images. For more information, see the "Images" section in [List of API operations by functions](/intl.en-US/API Reference/List of operations by function.md).

