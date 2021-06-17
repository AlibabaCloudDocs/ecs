# TagResources

Creates and adds tags to specified Elastic Compute Service \(ECS\) resources.

## Description

Before you add tags to a resource, Alibaba Cloud checks the number of existing tags of the resource. An error message is returned if the maximum number is reached. For more information, see the "Tag limits" section in [Limits](~~25412~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=TagResources&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|TagResources|The operation that you want to perform. Set the value to TagResources. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the resource. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ResourceId.N|RepeatList|Yes|i-bp67acfmxazb4ph\*\*\*\*|The ID of resource N. Valid values of N: 1 to 50. |
|ResourceType|String|Yes|instance|The type of the resource. Valid values:

 -   instance: ECS instance
-   disk: disk
-   snapshot: snapshot
-   image: image
-   securitygroup: security group
-   volume: storage volume
-   eni: elastic network interface \(ENI\)
-   ddh: dedicated host
-   ddhcluster: dedicated host cluster
-   keypair: SSH key pair
-   launchtemplate: launch template
-   reservedinstance: reserved instance
-   snapshotpolicy: automatic snapshot policy
-   elasticityassurance: elasticity assurance
-   capacityreservation: capacity reservation |
|Tag.N.Key|String|No|TestKey|The key of tag N. Valid values of N: 1 to 20. The tag key cannot be an empty string. The tag key can be up to 128 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`. |
|Tag.N.Value|String|No|TestValue|The value of tag N. Valid values of N: 1 to 20. The tag value can be an empty string. The tag value can be up to 128 characters in length and cannot start with `acs:`. It cannot contain `http://` or `https://`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=TagResources
&RegionId=cn-hangzhou
&ResourceId.1=i-bp1j6qtvdm8w0z1o0****
&ResourceId.2=i-bp1j6qtvdm8w0z1oP****
&ResourceType=instance
&Tag.1.Key=TestKey
&<Common request parameters>
```

Sample success responses

`XML` format

```
<TagResourcesResponse>
    <RequestId>C46FF5A8-C5F0-4024-8262-B16B639225A0</RequestId>
</TagResourcesResponse>
```

`JSON` format

```
{
	"RequestId":"C46FF5A8-C5F0-4024-8262-B16B639225A0"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|404|InvalidRegionId.NotFound|%s|The error message returned because the specified RegionId parameter does not exist.|
|404|MissingParameter.TagOwnerUid|The parameter - TagOwnerUid should not be null|The error message returned because the TagOwnerUid parameter is not specified.|
|404|MissingParameter.TagOwnerBid|The parameter - TagOwnerBid should not be null|The error message returned because the TagOwnerBid parameter is not specified.|
|404|MissingParameter.ResourceType|The parameter - ResourceType should not be null|The error message returned because the ResourceType parameter is not specified.|
|404|MissingParameter.Tags|The parameter - Tags should not be null|The error message returned because the tag-related parameters are not specified.|
|404|MissingParameter.RegionId|The parameter - RegionId should not be null|The error message returned because the RegionId parameter is not specified.|
|403|PermissionDenied.TagOwnerUid|The specified operator not have permission to set TagOwnerUid value.|The error message returned because you are not authorized to set the owner of the tag.|
|403|PermissionDenied.Scope|The specified operator not have permission to set Scope value.|The error message returned because you are not authorized to specify the Scope parameter.|
|400|NumberExceed.ResourceIds|The ResourceIds parameter's number is exceed , Valid : 50|The error message returned because more than 50 resource IDs are specified.|
|400|NumberExceed.Tags|The Tags parameter's number is exceed , Valid : 20|The error message returned because more than 20 tags are specified.|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|The error message returned because the specified tag key already exists. Tag keys must be unique.|
|404|InvalidResourceId.NotFound|The specified ResourceIds are not found in our records.|The error message returned because the specified resource does not exist. Check whether the resource ID is correct.|
|404|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|The error message returned because the specified ResourceType parameter does not exist.|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|The error message returned because the specified Tag.N.Key parameter is invalid.|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|The error message returned because the specified Tag.N.Value parameter is invalid.|
|400|OperationDenied.QuotaExceed|The quota of tags on resource is beyond permitted range.|The error message returned because the maximum number of tags that can be added to the resource has been reached.|
|403|InvalidResourceId.NotSupported|The specified ResourceId does not support tagging.|The error message returned because the specified resource does not support tagging.|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|The error message returned because the specified Tag.N.Key and Tag.N.Value parameters do not match.|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|The error message returned because the number of specified tags has reached the upper limit.|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned because the specified RegionId parameter does not exist.|
|400|Invalid.Scope|The specified scope is invalid.|The error message returned because the specified scope is invalid.|
|403|NoPermission.Tag|The operator is not permission for the tag.|The error message returned because you are not authorized to manage the tag.|
|403|QuotaExceed.Tags|%s|The error message returned because the maximum number of tags has been reached.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

