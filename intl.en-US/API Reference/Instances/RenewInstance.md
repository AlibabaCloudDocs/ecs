# RenewInstance

You can call this operation to renew a subscription ECS instance.

## Description

Before you call this operation, make sure that you fully understand the billing methods and pricing schedule of [ECS](https://www.alibabacloud.com/product/ecs#pricing).

When you call this operation, take note of the following items:

-   This operation is applicable only to subscription ECS instances.
-   By default, the renewal operation first uses available coupons in your account. This does not apply to discount services.
-   Your account must support credit card payment.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=RenewInstance&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RenewInstance|The operation that you want to perform. Set the value to RenewInstance. |
|InstanceId|String|Yes|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance. |
|Period|Integer|Yes|1|The renewal period of the subscription instance. If the DedicatedHostId parameter is specified, the value of the Period parameter must be within the subscription period of the dedicated host. Valid values:

-   If `PeriodUnit` is set to `Month`, the valid values of `Period` are 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 24, 36, 48, and 60. |
|PeriodUnit|String|No|Month|The unit of the renewal period. Default value: Month. Set the value to Month.

-   Month |
|ClientToken|String|No|0c593ea1-3bea-11e9-b96b-88e9fe637760|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value must contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OrderId|String|1234567890|The ID of the order. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=RenewInstance
&InstanceId=i-bp67acfmxazb4p****
&Period=1
&PeriodUnit=Month
&ClientToken=0c593ea1-3bea-11e9-b96b-88e9fe637760
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RenewInstanceResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <OrderId>1234567890</OrderId>
</RenewInstanceResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "OrderId": "1234567890"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|The error message returned because the specified InternetChargeType parameter is invalid.|
|400|InvalidInstanceType.NotSupported|The specified InstanceType is not Supported.|The error message returned because the specified InstanceType parameter is invalid.|
|400|InvalidParameter|The specified parameter "InternetMaxBandwidthOut" is not valid.|The error message returned because the specified InternetMaxBandwidthOut parameter is invalid.|
|400|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records.|The error message returned because the specified InstanceChargeType parameter does not exist.|
|400|InvalidRebootTime.ValueNotSupported|The specified RebootTime is out of the permitted range.|The error message returned because the specified restart time is out of the permitted range.|
|400|IdempotenceParamNotMatch|Request uses a client token in a previous request but is not identical to that request.|The error message returned because the ClientToken value in this request is identical to that in the previous request but some other parameters in this request are different from those in the previous request.|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|The error message returned because the specified ClientToken parameter is invalid.|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|The error message returned because the operation is not supported while the instance uses the current billing method.|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned because the specified instance type does not exist or because you are not authorized to manage the instance type.|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|The error message returned because the specified DiskId parameter does not exist. Check whether the disk ID is correct.|
|403|Diskcategory.Mismatch|The disk specified to convert to portable is not allowed due to the disk category does not support.|The error message returned because the specified disk cannot be converted to a removable disk due to disk category restrictions.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified instance does not exist. Check whether the instance ID is correct.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|400|InvalidInstanceType.codeUnauthorized|The specified InstanceType is not authorized.|The error message returned because the specified InstanceType parameter is invalid.|
|400|InvalidInternetChargeType.InstanceNotSupported|The specified instance which is in vpc is not support the parameter InternetChargeType.|The error message returned because the specified billing method for network usage is not supported by the specified VPC-type instance.|
|400|InvalidPeriod|The specified period is not valid.|The error message returned because the specified Period parameter is invalid.|
|403|InstanceSpecModification.NotEffective|The specified instance has been reserved for making a spec modification and not taken effective in the current contract period.|The error message returned because the instance is reserved due to instance type changes. Changes made to it cannot take effect during the current contract period.|
|400|Upgrade.NotSupported|Upgrade operation is not supported.|The error message returned because the upgrade operation is invalid.|
|403|LastTokenProcessing|The last token request is processing.|The error message returned because the previous token request is being processed. Try again later.|
|403|Instance.UnPaidOrder|The specified instance has unpaid order.|The error message returned because you have overdue payments for the instance.|
|400|OperationDenied|Specified instance is in VPC.|The error message returned because the specified instance is in a VPC.|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|The error message returned because you are not authorized to use the specified instance type.|
|400|InvalidParameter|The specified parameter " InternetMaxBandwidthOut " is not valid.|The error message returned because the specified InternetMaxBandwidthOut parameter is invalid.|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|The error message returned because the operation is not supported while the instance is locked for security reasons.|
|403|InvalidDisk.NotAllowed|The specified disk is not allowed to be converted to portable.|The error message returned because the specified disk cannot be converted to a removable disk.|
|400|DependencyViolation.InstanceType|Current instancetype cannot be changed to the specified one.|The error message returned because the current instance type cannot be changed to the specified one.|
|403|InstanceTypeNotSupported|The specified zone does not offer the specified instancetype.|The error message returned because instances of the specified instance type cannot be created in the specified zone.|
|400|InvalidPeriodUnit.ValueNotSupported|The specified parameter PeriodUnit is not valid.|The error message returned because the specified PeriodUnit parameter is invalid.|
|400|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|The error message returned because the specified DedicatedHostId parameter does not exist.|
|400|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status.|The error message returned because the operation is not supported while the dedicated host is in the current state.|
|400|IncorrectDedicatedHostStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|The error message returned because the expiration date of the instance is later than that of the dedicated host.|
|400|InvalidStatus.Upgrading|The instance is upgrading; please try again later.|The error message returned because the specified instance is being upgraded. Try again later.|
|400|InvalidPeriod.ExceededMaximumExpirationDate|The specified renewal period cannot exceed the maximum expiration date. We recommend you try shortening the renewal period at next attempt.|The error message returned because the specified renewal period exceeds the maximum allowed value. We recommend that you shorten the renewal period on your next attempt.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|400|LastOrderProcessing|The previous order is still processing, please try again later.|The error message returned because the order is being processed. Try again later.|
|400|Idempotence.Processing|The previous request is still processing, please try again later.|The error message returned because the previous request is being processed. Try again later.|
|403|InvalidChargeType.NotSupported|The chargeType of the instance does not support this operation.|The error message returned because the operation is not supported while the instance uses the current billing method.|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone, try other types of resources or other regions and zones.|The error message returned because the requested resources are sold out in the specified zone. Try another instance type or zone.|
|403|OperationDenied.NoStock|The resource is out of usage.|The error message returned because the instance is not in the Running state. Start the instance or check whether the operation is valid.|
|400|OperationDenied|The current user does not support this operation.|The error message returned because your account does not support this operation.|
|403|InvalidPeriod.StarterPackage|This instance was created by using a Starter Package plan and can only be renewed monthly, not yearly.|The error message returned because the instance was created by using a Starter Package plan and can only be automatically renewed on a monthly basis.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

