# Delete a custom image

You can delete a custom image that you no longer need.

Take note of the following items before you delete a custom image:

-   After a custom image is deleted, you are no longer able to create instances from the image.
-   After a custom image is deleted:
    -   The ECS instances that were created from the image can still be used and you continue to be charged for the instances.
    -   The system disks of ECS instances that were created from the image cannot be re-initialized.
-   Before you delete a shared image, you must unshare the image. After a shared image is deleted:
    -   The accounts to which the image was shared are no longer able to query the image by using the ECS console or by calling an API operation.
    -   The accounts to which the image was shared are no longer able to create ECS instances or replace the system disks by using the image.
    -   The system disks of ECS instances that were created from the shared image cannot be re-initialized.
-   If you delete an image that has been copied, the image copies are not affected. If you delete the copies of an image, the image is not affected.
-   If you delete a custom image, snapshots contained in the image are not deleted. If you do not want to keep the snapshots, navigate to the Snapshots page and delete the snapshots.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.

3.  In the top navigation bar, select a region.

4.  On the **Images** page, click the **Custom Image** tab. Select one or more custom images that you want to delete and click **Delete Image** in the lower part of the page.

5.  In the Delete Image dialog box, select **Forcibly Delete**.

6.  Click **OK**.


**Related topics**  


[DeleteImage](/intl.en-US/API Reference/Images/DeleteImage.md)

