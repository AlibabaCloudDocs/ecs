---
keyword: [Alibaba Cloud, data encryption, security compliance, ECS]
---

# Encrypt a system disk

When you copy a custom image, you can encrypt the image copy. System disks and data disks created from the image copy are automatically encrypted. The encryption keys of the system disks and data disks are identical to the encryption key used by the image copy. Encryption keys can be customer master keys \(CMKs\) that are created by using Key Management Service \(KMS\) or custom keys that you import \(BYOK\).

You can have encrypted system disks only by creating them from encrypted custom images. You can encrypt custom images only by copying them. For more information, see [Encryption overview](/intl.en-US/Block Storage/Encrypt a disk/Encryption overview.md).

## Copy a custom image and encrypt the image copy in the ECS console

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.

3.  In the top navigation bar, select a region.

4.  On the **Images** page, click the **Custom Images** tab.

5.  Click **Copy Image** in the **Actions** column corresponding to the custom image that you want to copy.

    **Note:** If the size of the custom image is greater than 500 GiB, follow on-screen tips to submit a ticket when you click **Copy Image**.

6.  In the **Copy Image** dialog box, select **Encrypt** and then select a key from the drop-down list.

    By default, Alibaba Cloud uses the managed service key **Default Service CMK** when you select **Encrypt**. You can also specify a CMK that you created in KMS \(BYOK\) as the encryption key of the image copy. We recommend that you use a custom CMK \(BYOK\) as the encryption key.

    **Note:** The first time that you select Encrypt, click **Go to Authorize** and select AliyunECSDiskEncryptDefaultRole to allow ECS to access your KMS resources. This procedure describes how to configure the encryption setting when you copy a custom image. For more information about other configurations, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md).

    ![Copy Image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1073559951/p75715.png)

7.  Click **OK**.

    After the image copy is encrypted, the KMS key used to encrypt the image copy is automatically bound with a tag. The key of the tag is `acs:ecs:disk-encryption`, and the value of the tag is `true`. You can view the key tag in the [KMS console](https://kms.console.aliyun.com).


## Copy a custom image and encrypt the image copy by calling the CopyImage operation

In the following example, Alibaba Cloud CLI is used to call the [CopyImage](/intl.en-US/API Reference/Images/CopyImage.md) operation with KMSKeyId specified to copy a custom image and encrypt the image copy.

```
aliyun ecs CopyImage --RegionId cn-hongkong \
--ImageId m-bp155shrycg3s0****** --DestinationRegionId cn-shenzhen \
--Encrypted true --KMSKeyId e522b26d-abf6-4e0d-b5da-04b7******3c \
--Tag.N.Key EcsDocumentation
```

## Change of the encryption status

After a custom image is copied, the encryption status of the system disks created from the image copy is determined by whether a new CMY is selected during the image copy process.

-   If you do not select a CMK when you copy an unencrypted custom image, the system disk created from the image copy is unencrypted.

    ![Copy an unencrypted custom image as an unencrypted custom image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7972909951/p40819.png)

-   If you select a CMK when you copy an unencrypted custom image, the image copy is encrypted. To access instances created from the image copy, you must use this CMK.

    ![Copy an unencrypted custom image as an encrypted custom image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8972909951/p40820.png)

-   If you do not select a CMK when you copy an encrypted image, the image copy is encrypted with the encryption key of the original image. To access instances created from the image copy, you must use the encryption key of the original image.

    ![Copy an encrypted custom image as an encrypted custom image but do not change the encryption key](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8972909951/p40821.png)

-   If you select a new CMK when you copy an encrypted image, the image copy is encrypted with the new CMK. To access instances created from the image copy, you must use the new CMK.

    ![Copy an encrypted custom image as an encrypted custom image and change the encryption key](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8972909951/p40823.png)


You can use the copied image to create an instance or change the system disk:

-   [Create an ECS instance by using a custom image](/intl.en-US/Instance/Create an instance/Create an ECS instance by using a custom image.md)
-   [Replace a system disk \(non-public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace a system disk (non-public images).md)

**Related topics**  


[CopyImage](/intl.en-US/API Reference/Images/CopyImage.md)

[CancelCopyImage](/intl.en-US/API Reference/Images/CancelCopyImage.md)

[Copy a snapshot](/intl.en-US/Snapshots/Use snapshots/Copy a snapshot.md)

