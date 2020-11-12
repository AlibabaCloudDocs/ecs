---
keyword: [custom Image, image, Alibaba Cloud]
---

# Overview

Custom images are created from instances or snapshots, or imported from your local device. You can create a custom image from an ECS instance that have applications deployed, and then use the custom image to create identical instances. This eliminates the need for repeated configurations.

## Lifecycle of a custom image

After you create or import a custom image, the image is in the **Available** state. You can use the image to create instances, share the image with other Alibaba Cloud accounts, copy the image to other regions, or export the image to an Object Storage Service \(OSS\) bucket. You can also delete the image if it is no longer needed.

**Note:** Only the creator of a custom image can use, share, copy, and delete the image.

The following figure shows the lifecycle of a custom image.

![Lifecycle of a custom image](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5863559951/p34490.png)

## Related operations

The following table lists operations that you can perform on custom images.

|Operation|Description|Reference|
|---------|-----------|---------|
|Create an image|You can create a custom image from an existing instance or a snapshot to copy the system environment without the need for repeated configurations. You can also use the custom image tool Packer to create a custom image.|-   [Create a custom image from an instance](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from an instance.md)
-   [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md)
-   [Create a custom image by using Packer](/intl.en-US/Images/Custom image/Create custom image/Create a custom image by using Packer.md)
-   [Create and import an on-premises image by using Packer](/intl.en-US/Images/Custom image/Create custom image/Create and import an on-premises image by using Packer.md) |
|Import an image|You can import a custom image from a local device.|[Image import procedure](/intl.en-US/Images/Custom image/Import images/Image import procedure.md)|
|Update an image|Operation Orchestration Service \(OOS\) provides public templates for automatic image updating. To create a random or scheduled O&M task, you only need to select a source image and specify required parameters such as the Cloud Assistant command in a public template. The O&M task is then automatically executed based on the definitions in the template.|[Update a custom image](/intl.en-US/Images/Custom image/Update a custom image.md)|
|Copy an image|If you want to use the image in another region, copy the image to that region. The image copy is assigned a unique ID. It is independent of the original image.

|[Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md)|
|Share an image|You can share a custom image that you created with other Alibaba Cloud accounts. The Alibaba Cloud accounts can create ECS instances from the shared image.|[Share a custom image](/intl.en-US/Images/Custom image/Share or unshare custom images.md)|
|Export an image|You can export a custom image that you created to an OSS bucket, and then download the image to local computers.|[Export a custom image](/intl.en-US/Images/Custom image/Export a custom image.md)|
|Modify image information|You can modify the name and description of a custom image.|[Modify custom images](/intl.en-US/Images/Custom image/Modify custom images.md)|
|Delete an image|You can delete a custom image that you no longer need.|[Delete a custom image](/intl.en-US/Images/Custom image/Delete a custom image.md)|

