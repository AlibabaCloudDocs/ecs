# ImportImage

Imports an image to Elastic Compute Service \(ECS\). The imported image appears as a custom image in the destination region. You can use the imported image to create ECS instances \(RunInstances\) or replace system disks of ECS instances \(ReplaceSystemDisk\).

## Description

When you call this operation, take note of the following items:

-   You must upload an image to an Object Storage Service \(OSS\) bucket before you can import the image. For more information, see [Upload objects](~~31886~~).
-   The first time you import an image, you must use Resource Access Management \(RAM\) to authorize ECS to access your OSS buckets. If ECS is not authorized to access your OSS buckets, the `NoSetRoletoECSServiceAcount` error code is returned when you call the ImportImage operation. For more information, see [Account access control](~~25481~~). The following example shows the policies required for some operations:

    1. Create a role named `AliyunECSImageImportDefaultRole`. You must use this exact name. Otherwise, the image cannot be imported. Configure the following trust policy for the role:

    ```
    
            {
                "Statement": [
                {
                    "Action": "sts:AssumeRole",
                    "Effect": "Allow",
                    "Principal": {
                    "Service": [
                        "ecs.aliyuncs.com"
                    ]
                    }
                }
            ],
                "Version": "1"
            }
            
    ```

    2. Attach the `AliyunECSImageImportRolePolicy` system policy to the role. For more information, visit the [Cloud Resource Access Authorization](https://ram.console.aliyun.com/?spm=5176.2020520101.0.0.64c64df5dfpmdY#/role/authorize?request=%7B%22Requests%22:%20%7B%22request1%22:%20%7B%22RoleName%22:%20%22AliyunECSImageImportDefaultRole%22,%20%22TemplateId%22:%20%22ECSImportRole%22%7D,%20%22request2%22:%20%7B%22RoleName%22:%20%22AliyunECSImageExportDefaultRole%22,%20%22TemplateId%22:%20%22ECSExportRole%22%7D%7D,%20%22ReturnUrl%22:%20%22https:%2F%2Fecs.console.aliyun.com%2F%22,%20%22Service%22:%20%22ECS%22%7D) page of the RAM console. You can also create a custom policy that contains the following content and attach the policy to the role:

    ```
    
            {
                "Version": "1",
                "Statement": [
                {
                    "Action": [
                            "oss:GetObject",
                            "oss:GetBucketLocation",
                            "oss:GetBucketInfo"
                ],
                        "Resource": "*",
                        "Effect": "Allow"
                        }
                ]
            }
            
    ```

-   You cannot delete an image that is being imported. However, you can call the [CancelTask](~~25624~~) operation to cancel the image import task.
-   You can import an image only to the same region as the OSS bucket to which the image is uploaded.
-   The valid values of N in the `DiskDeviceMapping.N` parameter are 1 to 17. When N is 1, the disk is the system disk. When N ranges from 2 to 17, the disk is a data disk.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer.](https://api.aliyun.com/#product=Ecs&api=ImportImage&type=RPC&version=2014-05-26)OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ImportImage|The operation that you want to perform. Set the value to ImportImage. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the OSS bucket to which to upload the image.

You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|DiskDeviceMapping.N.Format|String|No|QCOW2|The format of the custom image. Valid values:

-   RAW
-   VHD
-   QCOW2

This parameter is empty by default, which indicates that the system checks the format of the custom image and uses the check result as the value of this parameter. |
|DiskDeviceMapping.N.OSSBucket|String|No|ecsimageos|The OSS bucket where the source image is stored.

**Note:** The first time you import an image, you must use RAM to authorize ECS to access your OSS buckets. If ECS is not authorized to access your OSS buckets, the `NoSetRoletoECSServiceAcount` error code is returned when you call the ImportImage operation. |
|DiskDeviceMapping.N.OSSObject|String|No|CentOS\_5.4\_32.raw|The name \(key\) of the image uploaded to and stored in the OSS bucket. |
|DiskDeviceMapping.N.DiskImSize|Integer|No|80|The size of the custom image.

**Note:** This parameter will be removed in the future. We recommend that you use the DiskDeviceMapping.N.DiskImageSize parameter to ensure future compatibility. |
|DiskDeviceMapping.N.DiskImageSize|Integer|No|80|The size of disk N in the custom image. The size of the system disk must be greater than or equal to the size of the imported image. Valid values:

-   When N is set to 1, the disk is the system disk and its size ranges from 5 GiB to 500 GiB.
-   When N is set to a value from 2 to 17, the disk is a data disk and its size ranges from 5 GiB to 1,000 GiB.

When you import an image, the system automatically checks the size of the disk contained in the image and uses the check result as the value of this parameter. |
|DiskDeviceMapping.N.Device|String|No|null|The device name of disk N in the custom image.

**Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|ImageName|String|No|ImageTestName|The name of the custom image. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`. It can contain letters, digits, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).

This parameter is empty by default. |
|Description|String|No|TestDescription|The description of the custom image. It must be 2 to 256 characters in length and cannot start with `http://` or `https://`.

This parameter is empty by default. |
|Architecture|String|No|x86\_64|The system architecture. Valid values:

-   i386
-   x86\_64

Default value: x86\_64. |
|OSType|String|No|linux|The type of the operating system. Valid values:

-   windows
-   linux

Default value: linux. |
|Platform|String|No|Aliyun|The distribution of the operating system. Valid values:

-   CentOS
-   Ubuntu
-   SUSE
-   OpenSUSE
-   Debian
-   CoreOS
-   Aliyun
-   Anolis
-   Windows Server 2003
-   Windows Server 2008
-   Windows Server 2012
-   Others Linux
-   Customized Linux

Default value: Others Linux. |
|BootMode|String|No|BIOS|The boot mode of the custom image. Valid values:

-   BIOS
-   UEFI

Default value: BIOS.

**Note:** You must know which boot modes the specified image supports. When you use this parameter to change the boot mode of the image, specify a boot mode supported by the image to ensure that instances created by using this image can be started normally. |
|RoleName|String|No|AliyunECSImageImportDefaultRole|The name of the RAM role used to import the source image. |
|LicenseType|String|No|Auto|The type of the license used to activate the operating system after the image is imported. Valid values:

-   Auto: ECS checks the operating system of the source image and allocates a license to the operating system. ECS first checks whether the operating system distribution specified by `Platform` has a license allocated by an official Alibaba Cloud channel. If yes, the allocated license is used. If no, bring your own license \(BYOL\) is used.
-   Aliyun: The license allocated by an official Alibaba Cloud channel is used for the operating system distribution specified by `Platform`.
-   BYOL: The license that comes with the source operating system is used. In this case, make sure that your license key can be used in Alibaba Cloud.

Default value: Auto. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the custom image. Valid values of N: 1 to 20. The tag key cannot be an empty string. It can be up to 128 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or`https://`. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the custom image. Valid values of N: 1 to 20. The tag value can be an empty string. It can be up to 128 characters in length. It cannot start with `acs:` or contain `http://` or `https://`. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which to assign the custom image. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ImageId|String|m-bp67acfmxazb4p\*\*\*\*|The ID of the image. |
|RegionId|String|cn-hangzhou|The region ID of the image. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TaskId|String|t-bp67acfmxazb4p\*\*\*\*|The ID of the image import task. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ImportImage
&RegionId=cn-hangzhou
&DiskDeviceMapping.1.Format=QCOW2
&DiskDeviceMapping.1.OSSBucket=ecsimageos
&DiskDeviceMapping.1.OSSObject=CentOS_5.4_32.raw
&DiskDeviceMapping.1.DiskImageSize=80
&ImageName=Test
&Description=Test
&Architecture=x86_64
&OSType=linux
&Platform=Aliyun
&LicenseType=Aliyun
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ImportImageResponse>
      <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
      <ImageId>m-bp67acfmxazb4p****</ImageId>
      <RegionId>cn-hangzhou</RegionId>
      <ImportTaskId>t-bp67acfmxazb4p****</ImportTaskId>
</ImportImageResponse>
```

`JSON` format

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "ImageId": "m-bp67acfmxazb4p****",
    "RegionId": "cn-hangzhou",
    "ImportTaskId": "t-bp67acfmxazb4p****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|The error message returned because the RegionId parameter is not specified.|
|400|MissingParameter|An input parameter "DiskDeviceMapping.1.OSSBucket" that is mandatory for processing the request is not supplied.|The error message returned because the DiskDeviceMapping.N.OSSBucket parameter is not specified.|
|400|MissingParameter|An input parameter "DiskDeviceMapping.1.OSSObject" that is mandatory for processing the request is not supplied.|The error message returned because the DiskDeviceMapping.N.OSSBucket parameter is not specified.|
|400|InvalidImageName.Malformed|The specified Image name is wrongly formed.|The error message returned because the specified ImageName parameter is invalid. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with acs: or aliyun. It cannot contain http:// or https://. It can contain letters, digits, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).|
|400|InvalidOSSObject.Malformed|The specified OSS object is wrongly formed.|The error message returned because the specified DiskDeviceMapping.N.OSSObject parameter is invalid.|
|400|InvalidDescription.Malformed|The specified Image description is wrongly formed.|The error message returned because the specified Description parameter is invalid.|
|400|InvalidArchitecture.Malformed|The specified Architecture is wrongly formed.|The error message returned because the specified Architecture parameter is invalid.|
|400|InvalidPlatform.Malformed|The specified Platform is wrongly formed.|The error message returned because the specified Platform parameter is invalid.|
|400|InvalidOSType.Malformed|The specified OSType is wrongly formed.|The error message returned because the specified OSType parameter is invalid.|
|400|InvalidImageName.Duplicated|The destination image is exist.|The error message returned because the specified image name already exists.|
|400|InvalidImageSize|%s|The error message returned because the specified image size is invalid.|
|400|InvalidDataDiskSize|The specified DiskDeviceMapping.N.DiskImSize should be in the specified range.|The error message returned because the specified DiskDeviceMapping.N.DiskImSize parameter is invalid.|
|400|InvalidImageFormat.Malformed|The specified Image Format is wrongly formed.|The error message returned because the specified ImageFormat parameter is invalid.|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned because the specified RegionId parameter does not exist.|
|400|InvalidRegion.NotSupport|The specified region does not support image import or export.|The error message returned because the specified region does not support the operation.|
|403|ImageIsImporting|The specified Image is importing.|The error message returned because the specified image is being imported and cannot be managed.|
|403|QuotaExceed.Image|The Image Quota exceeds.|The error message returned because the custom image quota has been used up.|
|403|ImportImageFailed|Importing image is failed, Please contact the administrator.|The error message returned because the image failed to be imported. Contact a system administrator.|
|403|UserNotInTheWhiteList|The user is not in the white list of importing image.|The error message returned because you are not authorized to import images.|
|403|NoSetRoletoECSServiceAcount|ECS service account Have no right to access your OSS.please attach a role of access your oss to ECS service account.|The error message returned because ECS is not authorized to access the specified OSS bucket or object.|
|400|InvalidOSSBucket.NotFound|The specified OSS bucket does not exist in this region.|The error message returned because the specified bucket does not exist.|
|403|InvalidParameter.Malformed|The specified parameter "DiskDeviceMapping.n.Device " is not valid.|The error message returned because the specified DiskDeviceMapping.N.Device parameter is invalid.|
|403|MissingParameter.DiskDeviceMapping|The specified parameter DiskDeviceMapping is not supplied.|The error message returned because a parameter that starts with DiskDeviceMapping is not specified.|
|400|InvalidOSSObject.NotFound|The specified OSS object does not exist in this region.|The error message returned because the specified OSS object does not exist.|
|400|InvalidOSSObject.NotFound|The specified OSS object cannot be retrieved.|The error message returned because the specified OSS object cannot be found.|
|400|InvalidOSSBucket.NotMatched|The specified OSS bucket is incorrect, %s.|The error message returned because the specified DiskDeviceMapping.N.OSSBucket parameter is invalid. For more information, see the return value of the %s placeholder in the error message.|
|400|InvalidLicenseType.NotSupported|The specified LicenseType is not supported|The error message returned because the specified LicenseType parameter is invalid.|
|400|InvalidLicenseType.BYOLOnly|Only BYOL LicenseType is supported for the current platform provided|The error message returned because the current platform supports only BYOL licenses.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

