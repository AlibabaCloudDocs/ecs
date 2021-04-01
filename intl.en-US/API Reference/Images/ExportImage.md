# ExportImage

You can call this operation to export a custom image to an OSS bucket in the same region.

## Description

-   If system disk snapshots have been taken for the instances created from Alibaba Cloud Marketplace images, you cannot call this operation to export the custom images created from these system disk snapshots.
-   A custom image cannot be exported if it contains more than four data disk snapshots or if one of the data disk snapshots exceeds 500 GiB in size.
-   Before you export a custom image, you must use Resource Access Management \(RAM\) to create a RAM role for ECS and authorize ECS to write data to Object Storage Service \(OSS\).

    1. Create a role named `AliyunECSImageExportDefaultRole`. Configure the following trust policy for the role:

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

    2. Attach the `AliyunECSImageExportRolePolicy` system policy to the `AliyunECSImageExportDefaultRole` role. This policy is the default policy used for ECS to export images. For more information, go to the [Cloud Resource Access Authorization](https://ram.console.aliyun.com/?spm=5176.2020520101.0.0.64c64df5dfpmdY#/role/authorize?request=%7B%22Requests%22:%20%7B%22request1%22:%20%7B%22RoleName%22:%20%22AliyunECSImageImportDefaultRole%22,%20%22TemplateId%22:%20%22ECSImportRole%22%7D,%20%22request2%22:%20%7B%22RoleName%22:%20%22AliyunECSImageExportDefaultRole%22,%20%22TemplateId%22:%20%22ECSExportRole%22%7D%7D,%20%22ReturnUrl%22:%20%22https:%2F%2Fecs.console.aliyun.com%2F%22,%20%22Service%22:%20%22ECS%22%7D) page. Alternatively, you can create a custom policy that contains the following content and attach the policy to the role:

    ```
    
             {
               "Version": "1",
               "Statement": [
                 {
                   "Action": [
                     "oss:GetObject",
                     "oss:PutObject",
                     "oss:DeleteObject",
                     "oss:GetBucketLocation",
                     "oss:GetBucketInfo",
                     "oss:AbortMultipartUpload",
                     "oss:ListMultipartUploads",
                     "oss:ListParts"
                   ],
                   "Resource": "*",
                   "Effect": "Allow"
                 }
               ]
             }
            
    ```


## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ExportImage&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ExportImage|The operation that you want to perform. Set the value to ExportImage. |
|ImageId|String|Yes|m-bp67acfmxazb4p\*\*\*\*|The ID of the custom image. |
|OSSBucket|String|Yes|testexportImage|The OSS bucket to which to export the custom image. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the custom image. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|OSSPrefix|String|No|EcsExport|The prefix of the OSS object. It must be 1 to 30 characters in length and can contain digits and letters. |
|ImageFormat|String|No|raw|The format in which to export the custom image. Valid values:

-   raw
-   vhd
-   qcow2
-   vmdk
-   vdi

Default value: raw. |
|RoleName|String|No|AliyunECSImageExportDefaultRole|The name of the RAM role used to export the custom image. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RegionId|String|cn-hangzhou|The region ID. |
|RequestId|String|C8B26B44-0189-443E-9816-D951F59623A9|The ID of the request. |
|TaskId|String|tsk-bp67acfmxazb4p\*\*\*\*|The ID of the image export task. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ExportImage
&ImageId=m-bp67acfmxazb4p****
&OSSBucket=testexportImage
&RegionId=cn-hangzhou
&OSSPrefix=EcsExport
&ImageFormat=raw
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ExportImageResponse>
      <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
      <ExportTaskId>tsk-bp67acfmxazb4p****</ExportTaskId>
      <RegionId>cn-hangzhou</RegionId>
</ExportImageResponse>
```

`JSON` format

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "ExportTaskId": "tsk-bp67acfmxazb4p****",
    "RegionId": "cn-hangzhou"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|The error message returned because the required RegionId parameter is not specified.|
|400|MissingParameter|An input parameter "ImageId" that is mandatory for processing the request is not supplied.|The error message returned because the required ImageId parameter is not specified.|
|400|MissingParameter|An input parameter "OSSBucket" that is mandatory for processing the request is not supplied.|The error message returned because the required OSSBucket parameter is not specified.|
|400|InvalidImageName.Malformed|The specified Image name is wrongly formed.|The error message returned because the specified DestinationImageName parameter is invalid. The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.|
|400|InvalidOSSPrefix.Malformed|The specified OSSPrefix format is wrongly formed.|The error message returned because the specified OSSPrefix parameter is invalid.|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned because the RegionId parameter does not exist.|
|400|InvalidRegion.NotSupport|The specified region does not support image import or export.|The error message returned because the specified region does not support this operation.|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned because the specified image does not exist within this account. Check whether the image ID is correct.|
|400|IncorrectImageStatus|The specified Image is not available.|The error message returned because the status of the specified image is invalid.|
|403|ImageNotSupported|The specified image from the image market, do not support export image.|The error message returned because the specified image is an Alibaba Cloud Marketplace image and cannot be exported.|
|400|InvalidImageFormat.Malformed|The specified Image Format is wrongly formed.|The error message returned because the specified ImageFormat parameter is invalid.|
|403|ImageIsExporting|The specified Image is exporting.|The error message returned because the specified image is being exported.|
|403|ExportImageFailed|Exporting image is failed, Please contact the administrator.|The error message returned because the image failed to be exported. Contact a system administrator.|
|403|UserNotInTheWhiteList|The user is not in the white list of exporting image.|The error message returned because you are not authorized to export images.|
|403|NoSetRoletoECSServiceAcount|ECS service account Have no right to access your OSS.please attach a role of access your oss to ECS service account.|The error message returned because ECS is not authorized to access the specified OSS bucket and object.|
|400|InvalidOSSBucket.NotFound|The specified OSS bucket does not exist in this region.|The error message returned because the specified OSS bucket does not exist.|
|400|OperationDenied|The specified image contains the snapshot of the data disk,does not support this operation.|The error message returned because the operation is not supported while the image contains data disk snapshots.|
|400|InvalidImage.DiskAmountOrSize|%s|The error message returned because the image contains more than four data disk snapshots or the size of one of the data disk snapshot exceeds 500 GiB.|
|400|ImageNotSupported|The specified Image contains encrypted snapshots, do not support export.|The error message returned because the specified image contains encrypted snapshots and cannot be exported.|
|400|ImageNotSupported|Image from image market does not support exporting.|The error message returned because the specified image is an Alibaba Cloud Marketplace image and cannot be exported.|
|400|InvalidOSSBucket.NotMatched|The specified OSS bucket is incorrect, %s.|The error message returned because the specified OSS bucket is invalid. For information about the details, see the response.|
|403|ConcurrentQuotaExceed.ExportImage|%s|The error message returned because the maximum number of concurrent ongoing tasks has been reached. Try again later.|
|403|WeeklyQuotaExceed.ExportImage|%s|The error message returned because the weekly quota for exported images of this week has been used up. Retry when the quota becomes available again.|
|403|InvalidImageLicense.NotSupported|%s|The error message returned because the specified image cannot be exported. For information about the details, see the response.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

