# DeleteAutoProvisioningGroup

You can call this operation to delete an auto provisioning group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DeleteAutoProvisioningGroup&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteAutoProvisioningGroup|The operation that you want to perform. Set the value to DeleteAutoProvisioningGroup. |
|AutoProvisioningGroupId|String|Yes|apg-bpuf6jel2bbl62wh13\*\*\*\*|The ID of the auto provisioning group to be deleted. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the auto provisioning group. |
|TerminateInstances|Boolean|Yes|true|Specifies whether to release instances in the auto provisioning group. Valid values:

-   true: releases instances in the auto provisioning group.
-   false: retains instances in the auto provisioning group. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|B48A12CD-1295-4A38-A8F0-0E92C937\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://ecs.aliyuncs.com/?Action=DeleteAutoProvisioningGroup
&AutoProvisioningGroupId=apg-bpuf6jel2bbl62wh13****
&RegionId=cn-hangzhou
&TerminateInstances=true
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteAutoProvisioningGroupResponse>
    <RequestId>928E2273-5715-46B9-A730-238DC996****</RequestId>
</DeleteAutoProvisioningGroupResponse>
```

`JSON` format

```
{
    "RequestId": "B48A12CD-1295-4A38-A8F0-0E92C937****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn't support RAM.|The error message returned because you are not authorized to manage this resource, or this API operation does not support RAM roles.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

