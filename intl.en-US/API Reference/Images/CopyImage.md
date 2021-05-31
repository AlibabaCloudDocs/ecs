# CopyImage

Copies a custom image from one region to another. You can deploy or copy instances across regions by copying images.

## Description

After you copy a custom image, you can use the image copy to create Elastic Compute Service \(ECS\) instances \(RunInstances\) or replace system disks of instances \(ReplaceSystemDisk\) in the destination region.

When you call this operation, take note of the following items:

-   Only custom images that are in the Available \(`Available`\) state can be copied.
-   You can copy only the images within your Alibaba Cloud account. Images cannot be copied from one account to another.
-   When an image is being copied, you cannot delete the image copy by calling the [DeleteImage](~~25537~~) operation, but you can cancel the copy task by calling the [CancelCopyImage](~~25539~~) operation.
-   A single region can have only one image copy task running at a time. Other image copy tasks queue up for the current task to complete before they run in sequence.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CopyImage&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CopyImage|The operation that you want to perform. Set the value to CopyImage. |
|ImageId|String|Yes|m-bp1h46wfpjsjastc\*\*\*\*|The ID of the source custom image. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the source custom image. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|DestinationRegionId|String|No|cn-shanghai|The ID of the destination region to which to copy the source custom image. |
|DestinationImageName|String|No|YourImageName|The name of the image copy. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`. It can contain letters, digits, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).

This parameter is empty by default. |
|DestinationDescription|String|No|This is a description example.|The description of the image copy. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.

This parameter is empty by default. |
|Encrypted|Boolean|No|false|Specifies whether to encrypt the image copy.

Default value: false. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the image copy. Valid values of N: 1 to 20. The tag key cannot be an empty string. A tag key can be up to 128 characters in length. It cannot start with `acs:` or `aliyun`. It cannot contain `http://` or`https://`. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the image copy. Valid values of N: 1 to 20. The tag value can be an empty string. A tag value can be up to 128 characters in length. It cannot start with `acs:` and cannot contain `http://` or `https://`. |
|KMSKeyId|String|No|e522b26d-abf6-4e0d-b5da-04b7\*\*\*\*\*\*3c|The ID of the key used to encrypt the image copy. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which the image copy belongs. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ImageId|String|m-bp1h46wfpjsjastd\*\*\*\*|The ID of the image copy. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CopyImage
&ImageId=m-bp1h46wfpjsjastc****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CopyImageResponse>
      <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
      <ImageId>m-bp1h46wfpjsjastd****</ImageId>
</CopyImageResponse>
```

`JSON` format

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "ImageId": "m-bp1h46wfpjsjastd****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|401|InvalidAliUid.IsNull|The aliUid must not be null|The error message returned because the required aliUid parameter is not specified.|
|400|InvalidImageName.Malformed|The specified Image name is wrongly formed.|The error message returned because the specified ImageName parameter is invalid. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with acs: or aliyun. It cannot contain http:// or https://. It can contain letters, digits, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).|
|403|Forbbiden|User not authorized to operate on the specified resource.|The error message returned because you are not authorized to access the specified resource.|
|400|InvalidImageName.Malformed|The specified destination Image name is wrongly formed.|The error message returned because the specified DestinationImageName parameter is invalid. For more information, see the description of the DestinationImageName parameter.|
|400|InvalidDescription.Malformed|The specified destination description is wrongly formed.|The error message returned because the specified DestinationDescription parameter is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|400|InvalidDescription.Malformed|The specified description is wrongly formed.|The error message returned because the specified Description parameter is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|400|SourceRegion.NotFound|The source region not found|The error message returned because the specified RegionId parameter does not exist.|
|400|DestinationRegion.NotFound|The destination region not found|The error message returned because the specified DestinationRegionId parameter does not exist.|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned because the specified image does not exist within this account. Check whether the image ID is correct.|
|400|IncorrectImageStatus|The image not available.|The error message returned because the specified image is unavailable.|
|400|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|The error message returned because the specified snapshot ID does not exist. Check whether the snapshot ID is correct.|
|400|InvalidImageName.Duplicated|The destination image is exist.|The error message returned because the specified image name already exists.|
|403|QuotaExceed.Image|The Image Quota exceeds.|The error message returned because the custom image quota has been used up.|
|403|QuotaExceed.Snapshot|The snapshot quota exceeds.|The error message returned because the maximum number of snapshots has been reached. To store new snapshots, delete the snapshots that are no longer needed.|
|403|OperationDenied.ImageCopying|The Image are coping.|The error message returned because the source image is being copied. Try again later.|
|403|RegionNotSupportCopy|The region not support copy.|The error message returned because the specified source or destination region does not support image copying.|
|403|InvalidSnapshot.TooOld|This operation is denied because the specified snapshot is created before 2013-07-15.|The error message returned because the operation is rejected while the specified snapshot was created before July 15, 2013.|
|403|OperationDenied|The specified snapshot is not allowed to create image.|The error message returned because the specified snapshot cannot be used to create images.|
|403|IncorrectDestinationRegion|The destination region is not equal the target region.|The error message returned because the source region is the same as the destination region.|
|403|SizeExceed.Image|The image exceeds the maximum size. Please open a ticket to add the account to the white list.|The error message returned because the size of the image exceeds the upper limit.|
|403|OperationDeined.EncryptedSnapshot|The image contains encrypted snapshots, which do not support copying.|The error message returned because the specified image contains encrypted snapshots and cannot be copied.|
|403|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|403|OperationDenied.SameRegionOnly|The image shared from others can not be copied to another region directly.|The error message returned because you cannot copy images shared by other Alibaba Cloud accounts to another region.|
|403|OperationDenied.NotPublished|The operation is denied because corresponding marketplace image is not published in destination region.|The error message returned because the image type is not supported in the destination region and the operation is rejected.|
|403|InvalidParameter.KMSKeyId.CMKNotEnabled|The CMK needs to be enabled.|The error message returned because the customer master key \(CMK\) is not enabled when a KMS key ID is specified for a disk. You can call the DescribeKey operation of KMS to query information about the specified CMK.|
|404|InvalidParameter.KMSKeyId.NotFound|The specified KMSKeyId does not exist.|The error message returned because the specified N.KMSKeyId parameter does not exist.|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|The error message returned because ECS is not authorized to access your KMS resources.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|403|InvalidRegion.NotSupport|The specified region does not support byok.|The error message returned because the bring your own key \(BYOK\) feature is not supported in the region.|
|403|UserNotInTheWhiteList|The user is not in byok white list.|The error message returned because you are not in the BYOK whitelist. Try again when you are in the whitelist.|
|400|InvalidParameter.EncryptedIllegal|The specified parameter Encrypted must be true when kmsKeyId is not empty.|The error message returned because the encryption feature is not enabled after a KMS key ID is specified.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

