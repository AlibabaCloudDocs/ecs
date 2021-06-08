# ModifyInstanceNetworkSpec

Modifies the bandwidth configurations of an Elastic Compute Service \(ECS\) instance. You can modify the bandwidth configurations of an instance to improve network performance.

## Description

When you call this operation, take note of the following items:

-   As of November 27, 2020, the maximum bandwidth value available for you to create ECS instances or change the configurations of ECS instances is subject to the throttling policy of your account. To increase the maximum bandwidth value, submit a ticket. The following throttling policies apply:
    -   In a single region, the sum of actual maximum bandwidths of all ECS instances that use the pay-by-traffic billing method for network usage cannot exceed 5 Gbit/s.
    -   In a single region, the sum of actual maximum bandwidths of all ECS instances that use the pay-by-bandwidth billing method for network usage cannot exceed 50 Gbit/s.
-   If you upgrade the outbound public bandwidth \(InternetMaxBandwidthOut\) of a subscription \(PrePaid\) instance from 0 Mbit/s when you modify the bandwidth configurations of the instance, a public IP address is automatically assigned to the instance.
-   If you upgrade the outbound public bandwidth \(InternetMaxBandwidthOut\) of a pay-as-you-go \(PostPaid\) instance from 0 Mbit/s when you modify the bandwidth configurations of the instance, no public IP address is assigned to the instance. You must call the [AllocatePublicIpAddress](~~25544~~) operation to assign a public IP address to the instance.
-   An instance in the classic network must be in the Stopped state before you can upgrade its outbound public bandwidth \(InternetMaxBandwidthOut\) from 0 Mbit/s.
-   After the bandwidth is upgraded, AutoPay is set to true by default and the payment is automatically made. Make sure that you have sufficient balance in your account. Otherwise, your order becomes invalid and must be canceled. If your account balance is insufficient, you can set AutoPay to false. In this case, when you call the ModifyInstanceNetworkSpec operation, an unpaid order is generated. Then, you can log on to the ECS console to pay for the order.
-   The price difference is refunded to the payment account that you used. Used coupons cannot be refunded.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceNetworkSpec&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyInstanceNetworkSpec|The operation that you want to perform. Set the value to ModifyInstanceNetworkSpec. |
|InstanceId|String|Yes|i-bp67acfmxazb4\*\*\*\*|The ID of the instance for which you want to modify bandwidth configurations. |
|InternetMaxBandwidthOut|Integer|No|10|The maximum outbound public bandwidth. Unit: Mbit/s. Valid values: 0 to 100. |
|InternetMaxBandwidthIn|Integer|No|10|The maximum inbound public bandwidth. Unit: Mbit/s. Valid values:

 -   When the purchased outbound public bandwidth is less than or equal to 10 Mbit/s, the valid values of InternetMaxBandwidthIn are 1 to 10, and the default value is 10.
-   When the purchased outbound public bandwidth is greater than 10 Mbit/s, the valid values of InternetMaxBandwidthIn are 1 to the `InternetMaxBandwidthOut` value, and the default value is the `InternetMaxBandwidthOut` value. |
|NetworkChargeType|String|No|PayByTraffic|The billing method for network usage. Valid values:

 -   PayByBandwidth: pay-by-bandwidth
-   PayByTraffic: pay-by-traffic

 **Note:** When the **pay-by-traffic** billing method is used, the maximum inbound and outbound bandwidths are both the upper limits of bandwidths instead of guaranteed performance. When demands exceed resource supplies, these maximum bandwidths may be limited. If you want guaranteed bandwidths for your instances, use the **pay-by-bandwidth** billing method. |
|AllocatePublicIp|Boolean|No|false|Specifies whether to assign a public IP address.

 Default value: false. |
|StartTime|String|No|2017-12-05T22:40Z|The start time of the temporary bandwidth upgrade. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddThh:mmZ format. The time must be in UTC and accurate to the **minute** \(mm\). |
|EndTime|String|No|2017-12-06T22Z|The end time of the temporary bandwidth upgrade. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddThhZ format. The time must be in UTC and accurate to **hours** \(hh\).

 **Note:** The interval between the end time and the start time of the temporary bandwidth upgrade must be greater than or equal to 3 hours. |
|AutoPay|Boolean|No|true|Specifies whether to enable automatic payment. Valid values:

 -   true: enables automatic payment. After bandwidth configurations are upgraded, the payment is automatically made. Make sure that you have sufficient balance in your account when you set AutoPay to true. If your account balance is insufficient, your order cannot be paid in the ECS console and becomes invalid. You must cancel the order.
-   false: does not enable automatic payment. After bandwidth configurations are upgraded, an order is generated but is not paid. If your account balance is insufficient, you can set AutoPay to false. In this case, when you call the ModifyInstanceNetworkSpec operation, an unpaid order is generated. You can then log on to the [ECS console](https://ecs.console.aliyun.com) to pay for the order.

 Default value: true. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but make sure that it is unique among different requests. The **ClientToken** value can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OrderId|String|123457890|The ID of the generated order. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceNetworkSpec
&InstanceId=i-bp67acfmxazb4p****
&InternetMaxBandwidthOut=10
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyInstanceNetworkSpecResponse>
        <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
        <OrderId>123457890</OrderId>
</ModifyInstanceNetworkSpecResponse>
```

`JSON` format

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "OrderId": "123457890"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist.|
|400|InvalidInternetMaxBandwidthIn.ValueNotSupported|The specified InternetMaxBandwidthIn is beyond the permitted range.|The error message returned because the specified InternetMaxBandwidthIn parameter is not within the allowed range.|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified InternetMaxBandwidthOut is beyond the permitted range.|The error message returned because the specified InternetMaxBandwidthOut parameter is not within the allowed range.|
|403|IncorrectInstanceStatus|The current status of the instance does not support this operation.|The error message returned because the operation is not supported while the instance is in the current state.|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|The error message returned because the operation is not supported while the instance is locked for security reasons.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned because the subscription instance has expired. Renew the instance and try again.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|403|ChargeTypeViolation|The operation is not permitted due to billing method of the instance.|The error message returned because the billing method of the instance does not support the operation.|
|403|OperationDenied|The operation is denied due to the instance is PrePaid.|The error message returned because the instance is a subscription instance and does not support the operation.|
|400|OperationDenied|Specified instance is in VPC.|The error message returned because the instance resides in a virtual private cloud \(VPC\).|
|400|InvalidParameter.Bandwidth|%s|The error message returned because the specified bandwidth is invalid.|
|400|InvalidParameter.Conflict|%s|The error message returned because a specified parameter is invalid. Check whether parameter conflicts exist.|
|400|InvalidStartTime.ValueNotSupported|%s|The error message returned because the end time is earlier than the start time.|
|400|Account.Arrearage|Your account has an outstanding payment.|The error message returned because you have overdue payments within your account.|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is invalid.|The error message returned because the specified NetworkChargeType parameter is invalid.|
|400|DecreasedBandwidthNotAllowed|%s|The error message returned because the bandwidth cannot be downgraded.|
|400|BandwidthUpgradeDenied.EipBoundInstance|The specified VPC instance has bound EIP, temporary bandwidth upgrade is denied.|The error message returned because the instance is associated with an elastic IP address and cannot have its bandwidth temporarily upgraded.|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|The error message returned because the specified ClientToken parameter is invalid.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Add funds to your account and try again.|
|403|InvalidInstance.UnPaidOrder|The specified Instance has unpaid order.|The error message returned because you have unpaid orders for the specified instance. Pay for the orders and try again.|
|400|Throttling|Request was denied due to request throttling, please try again after 5 minutes.|The error message returned because your request is throttled. Try again 5 minutes later.|
|400|InvalidAction|Specified action is not valid.|The error message returned because the operation is invalid.|
|400|IpAllocationError|Allocate public ip failed.|The error message returned because a public IP address failed to be assigned.|
|400|InvalidParam.AllocatePublicIp|The specified param AllocatePublicIp is invalid.|The error message returned because the specified AllocatePublicIp parameter is invalid.|
|400|InstanceDowngrade.QuotaExceed|Quota of instance downgrade is exceed.|The error message returned because the maximum number of configuration downgrades allowed for the instance has been reached.|
|400|InvalidBandwidth.ValueNotSupported|Instance upgrade bandwidth of temporary not allow less then existed.|The error message returned because the new bandwidth specified for the temporary bandwidth upgrade is lower than the current bandwidth.|
|403|InvalidInstance.InstanceNotSupported|The special vpc instance with eip not need bandwidth.|The error message returned because the instance is located in a VPC and associated with an elastic IP address and you cannot specify a public bandwidth for the instance.|
|400|InvalidInstanceStatus|The specified instance status does not support this action.|The error message returned because the operation is not supported while the instance is in the current state.|
|403|InvalidInstanceStatus|The current status of the instance does not support this operation.|The error message returned because the operation is not supported while the instance is in the current state.|
|400|InvalidInstance.UnPaidOrder|Unpaid order exists in your account, please complete or cancel the payment in the expense center.|The error message returned because you have unpaid orders in your account. Pay for the orders and try again.|
|400|OperationDenied|After downgrade, you cannot upgrade or downgrade your instances again in the remaining time of the current billing cycle.|The error message returned because you have downgraded the configurations of the instance and cannot upgrade or downgrade the configurations again until a new billing cycle starts.|
|400|InvalidInternetChargeType.ValueNotSupported|%s|The error message returned because the specified InternetChargeType parameter is invalid.|
|400|LastOrderProcessing|The previous order is still processing, please try again later.|The error message returned because the order is being processed. Try again later.|
|400|OperationDenied|The current user does not support this operation.|The error message returned because your account does not support the operation.|
|403|NAT\_PUBLIC\_IP\_BINDING\_FAILED|Binding nat public ip failed|The error message returned because the public IP address failed to be associated with the gateway.|
|403|InvalidInstance.EipNotSupport|The specified instance with eip is not supported, please unassociate eip first.|The error message returned because the operation is not supported while an elastic IP address is associated with the instance. Disassociate the elastic IP address first.|
|403|OperationDenied.UnpaidOrder|The specified instance has unpaid order.|The error message returned because you have unpaid orders for the specified instance. You can log on to the ECS console to pay for the orders.|
|403|InvalidNetworkType.ValueNotSupported|The specified parameter NetworkType is not valid.|The error message returned because the specified network type is invalid.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

