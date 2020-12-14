# CreateDedicatedHostCluster

You can call this operation to create a dedicated host cluster.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateDedicatedHostCluster&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateDedicatedHostCluster|The operation that you want to perform. Set the value to CreateDedicatedHostCluster. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region in which to create the dedicated host cluster. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request without actually making the request. Valid values:

-   true: The validity of the request is checked but the request is not made. Check items include whether your AccessKey pair is valid, whether RAM users are authorized, and whether the required parameters are specified. If the check fails, the corresponding error is returned. If the check succeeds, the `DryRunOperation` error code is returned.
-   false: The validity of the request is checked. If the check succeeds, a 2XX HTTP status code is returned and the request is made.

Default value: false |
|Tag.N.Key|String|No|TestKey|The key of tag N of the dedicated host cluster. Valid values of N: 1 to 20. The tag key cannot be an empty string. It can be up to 64 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the dedicated host cluster. Valid values of N: 1 to 20. The tag value cannot be an empty string. It can be up to 64 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which to assign the dedicated host cluster. |
|ZoneId|String|No|cn-hangzhou-f|The ID of the zone in which to create the dedicated host cluster. You can call the [DescribeZones](~~25610~~) operation to query the most recent zone list. |
|DedicatedHostClusterName|String|No|myDDHCluster|The name of the dedicated host cluster. The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter. It cannot contain `http://` or `https://`.

This parameter is empty by default. |
|Description|String|No|This-is-my-DDHCluster|The description of the dedicated host cluster. The description must be 2 to 256 characters in length. It cannot start with `http://` or `https://`.

This parameter is empty by default. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DedicatedHostClusterId|String|dc-bp12wlf6bw0vz9v2\*\*\*\*|The ID of the dedicated host cluster. |
|RequestId|String|E2A664A6-2933-4C64-88AE-5033D003EADF|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateDedicatedHostCluster
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-f
&DedicatedHostClusterName=myDDHCluster
&Description=This-is-my-DDHCluster
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateDedicatedHostClusterResponse>
      <RequestId>214A2187-B06F-4E49-A081-4D053466A8C7</RequestId>
      <DedicatedHostClusterId>dc-bp12wlf6bw0vz9v2****</DedicatedHostClusterId>
</CreateDedicatedHostClusterResponse>
```

`JSON` format

```
{
    "RequestId": "214A2187-B06F-4E49-A081-4D053466A8C7",
    "DedicatedHostClusterId": "dc-bp12wlf6bw0vz9v2****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|The error message returned because the specified ResourceGroupId parameter does not exist.|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|The error message returned because the specified Tag.N.Key parameter is invalid.|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|The error message returned because the specified Tag.N.Value parameter is invalid.|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|The error message returned because the specified tag key already exists. Tag keys must be unique.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

