# ModifyImageAttribute

You can call this operation to modify the name, description, status, or image family of a custom image.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyImageAttribute&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyImageAttribute|The operation that you want to perform. Set the value to ModifyImageAttribute. |
|ImageId|String|Yes|m-bp18ygjuqnwhechc\*\*\*\*|The ID of the custom image. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the custom image. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ImageName|String|No|testImageName|The new name of the custom image. The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.

This parameter is empty by default, which indicates that the original name is retained. |
|Status|String|No|Deprecated|The new status of the custom image. Valid values:

-   Deprecated: puts the custom image into the Deprecated state. If the custom image is shared, you must unshare the image before you can put it into the Deprecated state. Images in the Deprecated state cannot be shared or copied, but can be used to create instances or replace system disks.
-   Available: puts the image into the Available state. You can restore an image from the Deprecated state to the Available state.

**Note:** If you want to roll back a custom image in the image family to a previous version, you can put the latest available custom image into the Deprecated state. You are unable to create instances if no custom images are in the Available state within the instance family. Proceed with caution if only one custom image is in the Available state within the image family. |
|ImageFamily|String|No|hangzhou-daily-update|The new image family name. The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.

This parameter is empty by default. |
|BootMode|String|No|BIOS|The new boot mode of the custom image. Valid values:

-   BIOS
-   UEFI

**Note:** You must know which boot modes the custom image supports. When you use this parameter to change the boot mode of the image, specify a boot mode supported by the image to ensure that instances based on this image can start normally. |
|Description|String|No|testDescription|The new description of the custom image. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.

This parameter is empty by default, which indicates that the original description is retained. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyImageAttribute
&ImageId=m-bp18ygjuqnwhechc****
&RegionId=cn-hangzhou
&ImageName=testImageName
&Description=testDescription
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyImageAttributeResponse>
      <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
</ModifyImageAttributeResponse>
```

`JSON` format

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidImageName.Malformed|The specified Image name is wrongly formed.|The error message returned because the specified ImageName parameter is invalid. The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start acs: or aliyun. It cannot contain http:// or https://.|
|400|MissingParameter|The input parameter "RegionId" that is mandatory for processing this request is not supplied.|The error message returned because the required RegionId parameter is not specified.|
|400|InvalidImageName.Duplicated|The specified Image name has already bean used.|The error message returned because the specified image name already exists.|
|400|InvalidDescription.Malformed|The specified description is wrongly formed.|The error message returned because the specified Description parameter is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned because the specified image does not exist within this account.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

