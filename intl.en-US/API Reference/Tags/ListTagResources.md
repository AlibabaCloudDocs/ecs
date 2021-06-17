# ListTagResources

Queries the tags that are added to one or more Elastic Compute Service \(ECS\) resources.

## Description

Specify at least one of the following parameters or parameter pairs in the request to determine a query object:

-   `ResourceId.N`
-   `Tag.N` parameter pair \(`Tag.N.Key` and `Tag.N.Value`\)
-   `TagFilter.N`

If one of the following sets of request parameters is specified as filter conditions, the response contains only ECS resources that meet all these filter conditions:

-   Set 1: `Tag.N.Key, Tag.N.Value`, and `ResourceId.N`
-   Set 2: `TagFilter.N.TagValues.N, TagFilter.N.TagKey`, and `ResourceId.N`

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ListTagResources&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTagResources|The operation that you want to perform. Set the value to ListTagResources. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the resource. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
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
|TagFilter.N.TagKey|String|Yes|env|The key of tag N used for fuzzy search of ECS resources. The tag key must be 1 to 128 characters in length. Valid values of N: 1 to 5.

The `TagFilter.N` parameter pair \(TagFilter.N.TagKey and TagFilter.N.TagValues.N\) is used for fuzzy search of ECS resources that have specified tags added. In the specified tags, a tag key may correspond to one or more tag values. Fuzzy search may have a latency of 2 seconds. A fuzzy search can return a result set of up to 5,000 resources.

-   When you use `TagFilter.N.TagKey` for fuzzy search of ECS resources, you must leave `TagFilter.N.TagValues.N` empty. For example, to query ECS resources that have the `environment` tag key added, you can set `TagFilter.1.TagKey` to `env*` for prefix search, `*env*` for infix search, or `env` for exact search but you must leave `TagFilter.1.TagValues.1` empty.
-   When you use `TagFilter.N.TagValues.N` for fuzzy search of ECS resources, you must set `TagFilter.N.TagKey` to an exact value. For example, to query ECS resources that have a tag consisting of the `env` tag key and the `product` tag value, you must set `TagFilter.1.TagKey` to `env` and can set `TagFilter.1.TagValues.1` to `proc*` for prefix search, `*proc*` for infix search, or `proc` for exact search. Only one of the preceding search methods can be used for each tag key \(`TagFilter.N.TagKey`\). If multiple search methods are configured for a tag key, the first search method prevails.
-   If you specify multiple tag keys, only the ECS resources whose tags contain all the specified tag keys are returned.
-   If you specify a tag key that corresponds to multiple tag values, all the ECS resources that have one or more of these tag key-value pairs added are returned.

**Note:** The `TagFilter.N` parameter pair \(TagFilter.N.TagKey and TagFilter.N.TagValues.N\) cannot be used together with the `Tag.N` parameter pair \(Tag.N.Key and Tag.N.Value\). Otherwise, an error message is returned. |
|ResourceId.N|RepeatList|No|i-bp1j6qtvdm8w0z1o\*\*\*\*|The ID of resource N. Valid values of N: 1 to 50. |
|Tag.N.Key|String|No|TestKey|The key of tag N used for exact search of ECS resources. The tag key must be 1 to 128 characters in length. Valid values of N: 1 to 20.

The `Tag.N` parameter pair \(Tag.N.Key and Tag.N.Value\) is used for exact match of ECS resources that have specified tags added. Each tag is a key-value pair.

-   If you specify only `Tag.N.Key`, all ECS resources whose tags contain the specified tag key are returned.
-   If you specify only `Tag.N.Value`, the `InvalidParameter.TagValue` error is returned.
-   If you specify multiple tag key-value pairs, only the ECS resources that have all these tag key-value pairs added are returned. |
|Tag.N.Value|String|No|TestValue|The value of tag N used for exact search of ECS resources. The tag value must be 1 to 128 characters in length. Valid values of N: 1 to 20. |
|TagFilter.N.TagValues.N|RepeatList|No|TestTagFilter|The value of tag N used for fuzzy search of ECS resources. The tag value must be 1 to 128 characters in length. Valid values of N: 1 to 5. For more information, see the description of `TagFilter.N.TagKey`. |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0a4883|The token used to start the next query. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|The token used to start the next query. |
|RequestId|String|484256DA-D816-44D2-9D86-B6EE4D5BA78C|The ID of the request. |
|TagResources|Array of TagResource| |Details about resources and tags, including resource IDs, resource types, and tag key-value pairs. |
|TagResource| | | |
|ResourceId|String|i-bp1j6qtvdm8w0z1o\*\*\*\*|The ID of the resource. |
|ResourceType|String|instance|The type of the resource. Valid values:

-   instance: ECS instance
-   disk: disk
-   snapshot: snapshot
-   image: image
-   securitygroup: security group
-   volume: storage volume
-   eni: ENI
-   ddh: dedicated host
-   ddhcluster: dedicated host cluster
-   keypair: SSH key pair
-   launchtemplate: launch template
-   reservedinstance: reserved instance
-   snapshotpolicy: automatic snapshot policy
-   elasticityassurance: elasticity assurance
-   capacityreservation: capacity reservation |
|TagKey|String|TestKey|The tag key of the resource. |
|TagValue|String|TestValue|The tag value of the resource. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ListTagResources
&RegionId=cn-hangzhou
&ResourceType=instance
&ResourceId.1=i-bp1j6qtvdm8w0z1o****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListTagResourcesResponse>
      <TagResources>
            <TagResource>
                  <ResourceType>instance</ResourceType>
                  <TagValue>TestValue</TagValue>
                  <ResourceId>i-bp1j6qtvdm8w0z1o****</ResourceId>
                  <TagKey>TestKey</TagKey>
            </TagResource>
      </TagResources>
      <RequestId>DE65F6B7-7566-4802-9007-96F2494AC5XX</RequestId>
</ListTagResourcesResponse>
```

`JSON` format

```
{
    "TagResources": {
        "TagResource": [
            {
                "ResourceType": "instance",
                "TagValue": "TestValue",
                "ResourceId": "i-bp1j6qtvdm8w0z1o****",
                "TagKey": "TestKey"
            }
        ]
    },
    "RequestId": "DE65F6B7-7566-4802-9007-96F2494AC512"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
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

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

