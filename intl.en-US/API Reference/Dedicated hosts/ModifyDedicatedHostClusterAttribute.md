# ModifyDedicatedHostClusterAttribute

You can call this operation to modify some attributes of a dedicated host cluster, such as its name and description.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyDedicatedHostClusterAttribute&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDedicatedHostClusterAttribute|The operation that you want to perform. Set the value to ModifyDedicatedHostClusterAttribute. |
|DedicatedHostClusterId|String|Yes|dc-bp12wlf6am0vz9v2\*\*\*\*|The ID of the dedicated host cluster. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the dedicated host cluster. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|DedicatedHostClusterName|String|No|newClusterName|The name of the dedicated host cluster. The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter. It cannot contain `http://` or `https://`. |
|Description|String|No|newClusterDescription|The description of the dedicated host cluster. The description must be 2 to 256 characters in length. It cannot start with `http://` or `https://`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|11B55F58-D3A4-4A9B-9596-342420D02FF8|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyDedicatedHostClusterAttribute
&RegionId=cn-hangzhou
&DedicatedHostClusterId=dc-bp12wlf6am0vz9v2****
&DedicatedHostClusterName=newClusterName
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDedicatedHostClusterAttributeResponse>
      <RequestId>11B55F58-D3A4-4A9B-9596-342420D02FF8</RequestId>
</ModifyDedicatedHostClusterAttributeResponse>
```

`JSON` format

```
{
    "RequestId": "11B55F58-D3A4-4A9B-9596-342420D02FF8"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidDescription.Malformed|The specified parameter Description is not valid.|The error message returned because the specified Description parameter is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|403|InvalidUser.Unauthorized|The user is not authorized|The error message returned because you are not authorized to perform this operation.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

