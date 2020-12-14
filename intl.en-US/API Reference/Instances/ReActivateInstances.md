# ReActivateInstances

You can call this operation to reactivate a pay-as-you-go instance that has expired or for which you have overdue payments.

## Description

When you call this operation, take note of the following items:

-   The instance must be in the **Expired** \(`Stopped`\) state.
-   You must pay the bills and reactivate the instance within 15 days after the instance is stopped due to overdue payments. If you fail to reactivate the instance within the preceding period, the instance is released and data on the instance cannot be recovered. If you cannot reactivate a VPC-type instance, try again later or [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).
-   After the operation is called, the instance enters the **Starting** \(`Starting`\) state.
-   You cannot call this operation on ECS instances that are locked for security reasons. An instance is locked for security reasons if `OperationLocks` in the response returned when you query information of the instance contains `"LockReason": "security"`. For more information, see [API behavior when an instance is locked for security reasons](~~25695~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ReActivateInstances&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ReActivateInstances|The operation that you want to perform. Set the value to ReActivateInstances. |
|InstanceId|String|Yes|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance that you want to reactivate. |
|RegionId|String|No|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|51AB7717-6E1A-4D1D-A44D-54CB123ABC|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ReActivateInstances
&RegionId=cn-hangzhou
&InstanceId=i-bp67acfmxazb4p****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ReActivateInstancesResponse>
      <RequestId>51AB7717-6E1A-4D1D-A44D-54CB123ABC</RequestId>
</ReActivateInstancesResponse>
```

`JSON` format

```
{
    "RequestId": "51AB7717-6E1A-4D1D-A44D-54CB123ABC"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist.|
|404|InvalidPayType.NotSupport|The specified pre pay instance not support.|The error message returned because subscription instances do not support this operation.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|The error message returned because the operation is not supported while the instance is locked for security reasons.|
|403|InsufficientBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Add funds to your account and try again.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|400|ReopenInstance.InstanceStatusNotValid|Instance status is not Expired, ImageExpired or EcsAndImageExpired.|The error message returned because the instance fails to be reactivated. A possible cause is that the instance or the image has expired.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

