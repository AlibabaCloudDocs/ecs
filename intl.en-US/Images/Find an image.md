# Find an image

You can find an image based on its type, name, ID, or snapshot ID. After you find the image, you can use the image to create an instance or perform other operations. This topic describes how to find a specific image.

## Methods

You can use one of the following methods to find an image:

-   [Find an image by using the console](#section_3dr_thy_v7p)

    The following list provides three examples of this method:

    -   [Example 1](#section_bbf_onb_lzi): Find a Windows public image in the China \(Beijing\) region
    -   [Example 2](#section_g4o_i28_knb): Find a shared image whose name contains mysql in the China \(Hangzhou\) region
    -   [Example 3](#section_4k0_90k_qvn): Find a custom image whose snapshot ID is s-2xxxxxxxxxxxxxxxxxxx in the China \(Shenzhen\) region
-   [Find an image by calling an API operation](#section_wmv_5az_ujo)

## Find an image by using the console

You can find the image that you want to use on the Images page in the ECS console.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.

3.  In the top navigation bar, select a region.

4.  Select an image type.

5.  Select an image family.

    **Note:** You can select an image family only for custom images. By default, all images are displayed.

6.  Select a search item from the drop-down list.

    **Note:**

    You can select the image name, image ID, or snapshot ID as the search item.

7.  Enter the corresponding value in the search bar.

8.  Click Search to search for the image.


## Example 1

Example 1: Find a Windows public image in the China \(Beijing\) region

Perform the following operations on the Images page:

1.  In the upper-left corner, select **China \(Beijing\)** from the drop-down list.

2.  Click the **Public Image** tab.

3.  Select **Image Name** from the drop-down list in the search bar.

4.  Enter win in the search bar.

5.  Click Search to search for the image.


## Example 2

Example 2: Find a shared image whose name contains mysql in the China \(Hangzhou\) region

Perform the following operations on the Images page:

1.  In the upper-left corner, select **China \(Hangzhou\)** from the drop-down list.

2.  Click the **Shared Images** tab.

3.  Select **Image Name** from the drop-down list in the search bar.

4.  Enter mysql in the search bar.

5.  Click Search to search for the image.


## Example 3

Example 3: Find a custom image whose snapshot ID is s-2xxxxxxxxxxxxxxxxxxx in the China \(Shenzhen\) region

Perform the following operations on the Images page:

1.  In the upper-left corner, select **China \(Shenzhen\)** from the drop-down list.

2.  Click the **Custom Images** tab.

3.  Select **Snapshot ID** from the drop-down list in the search bar.

4.  Enter s-2xxxxxxxxxxxxxxxxxxx in the search bar.

5.  Click Search to search for the image.


## Find an image by calling an API operation

You can use OpenAPI Explorer or Alibaba Cloud CLI to call the DescribeImages operation to find a specific image. For more information about Alibaba Cloud CLI, see [What is Alibaba Cloud CLI?](). This section describes how to use OpenAPI Explorer to call the API operation to find a specific image.

1.  Go to [OpenAPI Explorer](https://api.aliyun.com/#/?product=Ecs&api=DescribeImages).

2.  Select a region from the **RegionId** drop-down list.

3.  Set other parameters such as ImageName and ImageId.

    **Note:** Image IDs are named in accordance with the following rules:

    -   IDs of public images are named after the operating system version numbers, architectures, languages, and release dates. For example, win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20190318.vhd indicates that the image runs Windows Server 2008 R2 Enterprise 64-bit \(English\).
    -   IDs of custom images and Alibaba Cloud Marketplace images start with m.
    -   IDs of shared images are the same as those of the source custom images.
4.  Click **Submit Request**.

5.  Click the **Debugging Result** tab.

    If the image is found, image information such as the image ID, description, and operating system is displayed on the **Debugging Result** tab. For more information, see [DescribeImages](/intl.en-US/API Reference/Images/DescribeImages.md).


After you find the image, you may want to perform the following operations:

-   Create an instance. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).
-   Share the image. For more information, see [Share or unshare custom images](/intl.en-US/Images/Custom image/Share or unshare custom images.md).
-   Copy the image. For more information, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md).
-   Export the image. For more information, see [Export a custom image](/intl.en-US/Images/Custom image/Export a custom image.md).
-   Delete the image. For more information, see [Delete a custom image](/intl.en-US/Images/Custom image/Delete a custom image.md)
-   Modify the description of the image. For more information, see [Modify custom images](/intl.en-US/Images/Custom image/Modify custom images.md).

**Related topics**  


[DescribeImages](/intl.en-US/API Reference/Images/DescribeImages.md)

