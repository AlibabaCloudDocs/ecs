# ModifyInstanceAutoRenewAttribute

You can call this operation to configure auto-renewal for one or more subscription instances. To reduce the maintenance workload when instances expire, you can configure auto-renewal for subscription instances.

## Description

Before you call this operation, make sure that you have fully understood the billing methods and pricing schedule of [ECS](https://www.alibabacloud.com/product/ecs#pricing).

-   The payment for auto-renewal is first made at 08:00:00 \(UTC+8\) nine days before the instance expires.
-   If the payment fails for the first time, this process repeats itself each day until the payment is made or the instance is locked after the nine-day period ends. You must confirm that your payment account has sufficient balance or credit.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates a sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceAutoRenewAttribute&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyInstanceAutoRenewAttribute|The operation that you want to perform. Set the value to ModifyInstanceAutoRenewAttribute. |
|InstanceId|String|Yes|i-bp67acfmxazb4ph\*\*\*\*,i-bp67acfmxazb4pi\*\*\*\*|The ID of the instance. A maximum of 100 instance IDs can be specified at a time. Separate multiple instance IDs with commas \(,\). |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Duration|Integer|No|1|The auto-renewal period.

-   When `PeriodUnit` is set to `Year`, valid values of `Duration` are 1, 2, and 3.
-   When `PeriodUnit` is set to `Month`, valid values of `Duration` are 1, 2, 3, 6, and 12. |
|AutoRenew|Boolean|No|true|Specifies whether to enable auto-renewal.

Default value: false. |
|RenewalStatus|String|No|AutoRenewal|The auto-renewal status of the instance. Valid values:

-   AutoRenewal: Auto-renewal is enabled for the instance.
-   Normal: Auto-renewal is disabled for the instance.
-   NotRenewal: The instance will not be renewed upon expiration. The system no longer sends an expiration reminder, but sends only a non-renewal reminder three days before the expiration date. You can change the value of this parameter from NotRenewal to `Normal` for an instance, and then manually renew the instance. Alternatively, you can set the RenewalStatus parameter to AutoRenewal.

**Note:** `RenewalStatus` takes precedence over `AutoRenew`. If you do not specify `RenewalStatus`, the `AutoRenew` parameter is used by default. |
|PeriodUnit|String|No|Month|The unit of the renewal duration \(`Period`\). Default value: month. Default value: Month. Valid values:

-   Month
-   Year |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceAutoRenewAttribute
&RegionId=cn-hangzhou
&InstanceId=i-bp67acfmxazb4ph****,i-bp67acfmxazb4pi****
&Duration=1
&PeriodUnit=Month
&AutoRenew=true
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyInstanceAutoRenewAttributeResponse>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceAutoRenewAttributeResponse>
```

`JSON` format

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|MissingParameter.InstanceId|InstanceId should not be null.|The error message returned because the InstanceId parameter is not specified.|
|403|InvalidParameter.ToManyInstanceIds|InstanceId should be less than 100.|The error message returned because the total number of instances has exceeded 100.|
|403|InvalidParameter.InvalidInstanceId|%s|The error message returned because the specified InstanceId parameter is invalid.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|ChargeTypeViolation|Pay-As-You-Go instances do not support this operation.|The error message returned because the pay-as-you-go billing method does not support this operation.|
|403|InvalidParameter.Duration|%s|The error message returned because the specified Duration parameter is invalid.|
|403|InvalidParameter.RenewalStatus|%s|The error message returned because the specified RenewalStatus parameter is invalid.|
|403|InvalidPeriodUnit.ValueNotSupported|The specified parameter PeriodUnit is not valid.|The error message returned because the specified PeriodUnit parameter is invalid.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|InvalidPeriod.StarterPackage|This instance was created by using a Starter Package plan and can only be renewed monthly, not yearly.|The error message returned because the instance was created by using a Starter Package plan and can only be automatically renewed on a monthly basis.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

