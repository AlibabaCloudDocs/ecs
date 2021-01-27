# CreateDisk

You can call this operation to create a pay-as-you-go or subscription data disk. The disk can be a basic disk, ultra disk, standard SSD, or enhanced SSD \(ESSD\).

## Description

-   When you create disks, you may be charged for the resources used. We recommend that you fully understand the ECS billing methods before you create a disk. For more information, see [Billing overview](~~25398~~).
-   By default, the DeleteAutoSnapshot parameter is set to true when a disk is created. This indicates that when the disk is released, its automatic snapshots are deleted. You can call the [ModifyDiskAttribute](~~25517~~) operation to modify the parameter.
-   If you do not configure the performance level when you create an ESSD, the performance level for the ESSD is PL1 by default. You can call the [ModifyDiskSpec](~~123780~~) operation to modify the performance level of the ESSD.
-   By default, the Portable parameter of a disk created by calling this operation is set to true, and the billing method of the disk is pay-as-you-go.
-   You must specify one of the Size and SnapshotId parameters. The Size parameter specifies the size of the disk and the SnapshotId parameter specifies the snapshot that is used to create the disk.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateDisk&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateDisk|The operation that you want to perform. Set the value to CreateDisk. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the disk. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ZoneId|String|No|cn-hangzhou-g|The ID of the zone in which a pay-as-you-go disk is to be created.

-   If the InstanceId parameter is not specified, the ZoneId parameter is required.
-   You cannot specify both the ZoneId and InstanceId parameters. |
|SnapshotId|String|No|s-bp67acfmxazb4p\*\*\*\*|The ID of the snapshot used to create the disk. If this parameter is specified, the Size parameter is ignored, and the disk is created with the size of the specified snapshot. The snapshots that were created on or before July 15, 2013 cannot be used to create disks. |
|DiskName|String|No|testDiskName|The name of the disk. The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter but cannot start with http:// or https://.

This parameter is empty by default. |
|Size|Integer|No|2000|The size of the disk. Unit: GiB. The value of this parameter must be greater than or equal to the size of the specified snapshot. Valid values:

-   Valid values when DiskCategory is set to cloud: 5 to 2000
-   Valid values when DiskCategory is set to cloud\_efficiency: 20 to 32768
-   Valid values when DiskCategory is set to cloud\_ssd: 20 to 32768
-   Valid values when DiskCategory is set to cloud\_essd: 20 to 32768 |
|DiskCategory|String|No|cloud\_ssd|The category of the data disk. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: ESSD

Default value: cloud. |
|Description|String|No|testDescription|The description of the disk. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

This parameter is empty by default. |
|Encrypted|Boolean|No|false|Specifies whether to encrypt the disk. Default value: false. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value must contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|InstanceId|String|No|i-bp18pnlg1ds9rky4\*\*\*\*|The ID of the instance to which the created subscription disk is automatically attached.

-   After you specify the instance ID, the specified ResourceGroupId, Tag.N.Key, Tag.N.Value, ClientToken, and KMSKeyId parameters are ignored.
-   You cannot specify both the ZoneId and InstanceId parameters.

This parameter is empty by default. This indicates that a pay-as-you-go disk is created and the RegionId and ZoneId parameters determine where the disk resides. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the disk. Valid values of N: 1 to 20. The tag key cannot be an empty string. The tag key can be up to 128 characters in length. It cannot start with aliyun or acs:, or contain http:// or https://. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the disk. Valid values of N: 1 to 20. This parameter can be an empty string. It can be up to 128 characters in length and cannot start with acs: or contain http:// or https://. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which the disk belongs. |
|KMSKeyId|String|No|0e478b7a-4262-4802-b8cb-00d3fb40826X|The ID of the KMS key corresponding to the disk. |
|PerformanceLevel|String|No|PL1|Specifies the performance level of an ESSD when you create the ESSD. Valid values:

-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS.

For more information about ESSD performance levels, see [ESSD](~~122389~~). |
|StorageSetId|String|No|ss-bp67acfmxazb4p\*\*\*\*|The ID of the storage set. |
|StorageSetPartitionNumber|Integer|No|3|The number of partitions in the storage set. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DiskId|String|d-bp131n0q38u3a4zi\*\*\*\*|The ID of the disk. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateDisk
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-g
&SnapshotId=s-bp67acfmxazb4p****
&DiskName=testDiskName
&Size=2000
&DiskCategory=cloud_ssd
&Description=testDescription
&Encrypted=false
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&Tag.1.Key=TestKey
&Tag.1.Value=TestValue
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateDiskResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <DiskId>d-bp131n0q38u3a4zi****</DiskId>
</CreateDiskResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "DiskId": "d-bp131n0q38u3a4zi****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidSize.ValueNotSupported|The specified parameter Size is not valid.|The error message returned because the specified Size parameter is invalid.|
|403|InvalidDataDiskCategory.NotSupported|Specified disk category is not supported.|The error message returned because the specified DiskCategory parameter is not supported.|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned because the specified RegionId parameter does not exist.|
|404|InvalidZoneId.NotFound|The specified zone does not exist.|The error message returned because the specified ZoneId parameter does not exist.|
|404|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|The error message returned because the specified snapshot does not exist. Check whether the snapshot ID is correct.|
|400|InvalidDiskName.Malformed|The specified disk name is wrongly formed.|The error message returned because the specified DiskName parameter is invalid. The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.|
|400|InvalidDescription.Malformed|The specified description is wrongly formed.|The error message returned because the specified description is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|403|InstanceDiskCategoryLimitExceed|The total size of specified disk category in an instance exceeds.|The error message returned because the total size of the specified disks exceeds the maximum capacity that is allowed for the disk category.|
|403|InvalidSnapshot.NotReady|The specified snapshot creation is not completed yet.|The error message returned because the specified snapshot is no created.|
|403|InvalidSnapshot.TooOld|This operation is forbidden because the specified snapshot is created before 2013-07-15.|The error message returned because the specified snapshot created on or before July 15, 2013 cannot be used to create disks.|
|403|InvalidSnapshot.TooLarge|The capacity of snapshot exceeds 2000GB.|The error message returned because the size of the specified snapshot exceeds 2,000 GB.|
|403|OperationDenied|The specified snapshot is not allowed to create disk.|The error message returned because the specified snapshot cannot be used to create disks.|
|403|QuotaExceed.PortableCloudDisk|The quota of portable cloud disk exceeds.|The error message returned because the maximum number of removable disks has been reached.|
|400|MissingParameter|The input parameter either "SnapshotId" or "Size" should be specified.|The error message returned because neither the SnapshotId parameter nor the Size parameter is specified.|
|403|InvalidDiskCategory.ValueUnauthorized|The disk category is not authorized.|The error message returned because you are not authorized to manage the specified disk category.|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|The error message returned because the specified snapshot is being created.|
|403|InvalidSnapshotId.NotDataDiskSnapshot|The specified snapshot is system disk snapshot.|The error message returned because the specified snapshot is a system disk snapshot.|
|403|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot.|The error message returned because the capacity of the specified disk is smaller than that of the snapshot.|
|403|OperationDenied|The type of the disk does not support the operation.|The error message returned because the specified disk category does not support this operation.|
|403|InvalidDataDiskCategory.NotSupported|%s|The error message returned because the specified DiskCategory parameter is invalid.|
|403|InvalidDiskSize.NotSupported|disk size is not supported.|The error message returned because the specified Size parameter is invalid.|
|400|InvalidDiskCategory.NotSupported|The specified disk category is not support.|The error message returned because the specified DiskCategory parameter is not supported.|
|400|Account.Arrearage|Your account has an outstanding payment.|The error message returned because you have overdue payments in your account.|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Add funds to your account and try again.|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|The error message returned because the operation is not supported while the snapshot service is not activated.|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|The error message returned because the specified DiskCategory parameter is invalid.|
|400|InvalidParameter.Conflict|%s|The error message returned because a specified parameter is invalid. Check whether the parameter conflicts with another parameter.|
|400|RegionUnauthorized|%s|The error message returned because you are not authorized to perform the operation in the specified region.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|400|Zone.NotOnSale|%s|The error message returned because the requested resources are unavailable in the specified zone.|
|400|InvalidDataDiskSize.ValueNotSupported|%s|The error message returned because the specified Size parameter is invalid.|
|403|InvalidPayMethod|The specified pay method is not valid.|The error message returned because the specified payment method is invalid.|
|400|OperationDenied|The specified Zone is not available or not authorized.|The error message returned because the specified zone is unavailable or you are not authorized to access it.|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|The error message returned because the specified ResourceGroupId parameter does not exist.|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not supported.|The error message returned because the specified disk category does not support the current operation.|
|403|InvalidDiskSize.NotSupported|The specified disk size is not supported.|The error message returned because the specified Size parameter is invalid.|
|400|InvalidDiskSize.NotSupported|The specified parameter size is not valid.|The error message returned because the specified Size parameter is invalid.|
|403|UserNotInTheWhiteList|The user is not in disk white list.|The error message returned because you are not in the whitelist to manage the disk. Try again when you are in the whitelist.|
|400|InvalidDiskSizeOrCategory|The specified disk category or size is invalid.|The error message returned because the specified disk category or size is invalid.|
|400|InvalidParameter.EncryptedIllegal|%s|The error message returned because the specified parameter is invalid. Check whether the encryption is valid.|
|400|InvalidParameter.EncryptedNotSupported|%s|The error message returned because the specified parameter is invalid and your encryption operation is not supported.|
|400|EncryptedOption.Conflict|%s|The error message returned because the parameter does not support encrypted disks.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|QuotaExceed.PostPaidDisk|Living postPaid disks quota exceeded.|The error message returned because the maximum number of pay-as-you-go disks has been reached.|
|403|InvalidRegion.NotSupport|The specified region does not support byok.|The error message returned because the bring your own key \(BYOK\) feature is not supported in this region.|
|403|UserNotInTheWhiteList|The user is not in byok white list.|The error message returned because you are not in the BYOK whitelist. Try again when you are in the whitelist.|
|400|InvalidParameter.EncryptedIllegal|The specified parameter Encrypted must be true when kmsKeyId is not empty.|The error message returned because the encryption feature is not enabled after the KMSKeyId parameter is specified.|
|404|InvalidParameter.KMSKeyId.NotFound|The specified KMSKeyId does not exist.|The error message returned because the specified KMSKeyId parameter does not exist.|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|The error message returned because ECS is not authorized to access your KMS resources.|
|403|SecurityRisk.3DVerification|We have detected a security risk with your default credit or debit card. Please proceed with verification via the link in your email.|The error message returned because your default credit card or debit card is exposed to security risks. Click the link in the email for verification.|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|The error message returned because a tag with the identical key already exists.|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|The error message returned because the specified Tag.N.Key parameter is invalid.|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|The error message returned because the specified Tag.N.Value parameter is invalid.|
|404|InvalidInstanceId.NotFound|The InstanceId provided does not exist in our records.|The error message returned because the specified InstanceId parameter does not exist. Check whether the instance ID is correct.|
|403|InvalidStatus.Upgrading|The instance is upgrading; please try again later.|The error message returned because the specified instance is being upgraded. Try again later.|
|400|InvalidPerformanceLevel.Malformed|The specified parameter PerformanceLevel is not valid.|The error message returned because the specified PerformanceLevel parameter is invalid.|
|403|QuotaExceed.Tags|%s|The error message returned because the maximum number of tags has been reached.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist. Check whether the instance ID is correct.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

