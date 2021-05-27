# ModifyInstanceAttachmentAttributes

You can call this operation to modify the properties of the private pool for an instance.

## Description

A private pool is generated after an elasticity assurance or a capacity reservation is created. The private pool is associated with information about instances that are created by using the private pool. You can configure whether to use a private pool when you create an ECS instance, so that the instance can match the elasticity assurance or capacity reservation.

-   After you call this operation to modify the properties of the private pool for an instance, you do not need to restart the instance.
-   When you call the following operations, the system rematches the instance with private pools. If the instance already matches a specified private pool, the call to an operation may fail because the private pool capacity is used up or the private pool is invalid. If the call fails, call the ModifyInstanceAttachmentAttributes operation to change the match mode of the private pool to `Open`.
    -   StartInstance: Call this operation to restart an instance in the No Fees for Stopped Instances \(VPC-Connected\) state.
    -   ReActivateInstances
    -   ModifyInstanceChargeType
    -   ModifyPrepayInstanceSpec
    -   ReplaceSystemDisk

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceAttachmentAttributes&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyInstanceAttachmentAttributes|The operation that you want to perform. Set the value to ModifyInstanceAttachmentAttributes. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the private pool. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|PrivatePoolOptions.MatchCriteria|String|Yes|Open|The match mode of the private pool. Valid values:

-   Open: the open mode The system automatically matches the instance with open private pools.
-   Target: You must use `PrivatePoolOptions.Id` to specify the ID of a private pool.
-   None: The instance starts normally without using private pools. |
|InstanceId|String|Yes|i-bp67acfmxazb4\*\*\*\*|The ID of the instance for which you want to modify the properties of the private pool. |
|PrivatePoolOptions.Id|String|No|eap-bp67acfmxazb4\*\*\*\*|The ID of the private pool. Set the value to the ID of the elasticity assurance or capacity reservation that generates the private pool.

-   This parameter is required when the value of `PrivatePoolOptions.MatchCriteria` is set to `Target`.
-   This parameter must be empty when the value of `PrivatePoolOptions.MatchCriteria` is set to `Open` or `None`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceAttachmentAttributes
&RegionId=cn-hangzhou
&InstanceId=i-bp67acfmxazb4****
&PrivatePoolOptions.MatchCriteria=Open
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyInstanceAttachmentAttributesResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyInstanceAttachmentAttributesResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|The error message returned because the RegionId parameter is not specified.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

