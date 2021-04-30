# ModifyInstanceChargeType

You can call this operation to change the billing method of one or more Elastic Compute Service \(ECS\) instances. You can change the billing methods of instances between pay-as-you-go and subscription, or change the billing method of all data disks attached to an instance from pay-as-you-go to subscription.

## Description

Before you call this operation, make sure that you fully understand the billing methods and pricing schedule of [Elastic Compute Service](https://www.alibabacloud.com/product/ecs#pricing).

When you call this operation, take note of the following items:

-   The instances must be in the **Running** \(`Running`\) or **Stopped** \(`Stopped`\) state, and you have no overdue payments for them.
-   After you change the billing method, automatic payment is enabled by default. Make sure that you have sufficient balance in your account. Otherwise, your order becomes invalid and must be canceled. If your account balance is insufficient, you can set `AutoPay` to `false`. Then an order is generated. You can log on to the [ECS console](https://ecs.console.aliyun.com/) to pay for the order.
-   **Change the billing method from subscription to pay-as-you-go**:
    -   Whether you can change the billing method depends on your ECS usage.
    -   After you change the billing method of an instance from subscription to pay-as-you-go, the new billing method remains in effect for the remaining lifecycle of the instance. The price difference is refunded to the payment account that you used. Vouchers that have been redeemed are not refundable.
    -   **Refund rule**: You have a quota for the total refund amount each month, and unused balance of this quota is not carried forward into the next month. After you use up the refund quota of the current month, you can change the billing method only when the next month arrives. The refund amount incurred when you change the billing method is calculated based on the following formula: **Number of vCPUs × \(Number of remaining days × 24 ± Number of remaining or elapsed hours\)**.
-   **Change the billing method from pay-as-you-go to subscription**:
    -   You can change the billing method of all data disks attached to an instance from pay-as-you-go to subscription.
    -   This operation cannot be called for a pay-as-you-go instance that has an automatic release time set.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceChargeType&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyInstanceChargeType|The operation that you want to perform. Set the value to ModifyInstanceChargeType. |
|InstanceIds|String|Yes|\["i-bp67acfmxazb4p\*\*\*\*","i-bp67acfmxazb4d\*\*\*\*"\]|The IDs of the instances. The value can be a JSON array that consists of up to 20 instance IDs. Separate multiple instance IDs with commas \(,\). |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Period|Integer|No|1|The renewal duration of the subscription instance. If the instance is hosted on a dedicated host, the renewal duration of the instance cannot exceed the subscription duration of the dedicated host. Valid values:

-   When the `PeriodUnit` parameter is set to Month, the valid values of the `Period` parameter are 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60. |
|PeriodUnit|String|No|Month|The unit of the renewal duration \(`Period`\). Default value: Month. Valid values:

-   Month |
|IncludeDataDisks|Boolean|No|false|Specifies whether to change the billing method of all data disks attached to the instance from pay-as-you-go to subscription.

Default value: false |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request without actually making the request. Default value: false. Valid values:

-   true: The validity of the request is checked but the request is not made. The system checks whether your AccessKey pair is valid, whether RAM users are authorized, and whether required parameters are specified. If the request fails the check, the corresponding error message is returned. If the request is determined as valid, the `DryRunOperation` error code is returned.
-   false: The validity of the request is checked. If the request is determined as valid, a 2XX HTTP status code is returned and the request is made. |
|AutoPay|Boolean|No|false|Specifies whether to enable automatic payment. Default value: true. Valid values:

-   true: enables automatic payment. Make sure that you have sufficient balance in your account. Otherwise, your order becomes invalid and must be canceled.
-   false: An order is generated but no payment is made.

**Note:** If your account balance is insufficient, you can set the AutoPay parameter to false to prevent your order from becoming invalid. Then, you can log on to the ECS console to pay for the order. |
|InstanceChargeType|String|No|PrePaid|The new billing method. Default value: PrePaid. Valid values:

-   PrePaid: subscription
-   PostPaid: pay-as-you-go |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value must contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|IsDetailFee|Boolean|No|false|Specifies whether to return cost details of the order when the billing method is changed from subscription to pay-as-you-go.

Default value: false |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|FeeOfInstances|Array of FeeOfInstance| |Cost details of the order. |
|FeeOfInstance| | | |
|Currency|String|CNY|The unit of currency for the bill. |
|Fee|String|0|The cost value. |
|InstanceId|String|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance. |
|OrderId|String|20413515388\*\*\*\*|The ID of the order. |
|RequestId|String|B61C08E5-403A-46A2-96C1-F7B1216DB10C|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceChargeType
&RegionId=cn-hangzhou
&InstanceIds=["i-bp67acfmxazb4p****","i-bp67acfmxazb4d****"]
&Period=1
&PeriodUnit=Month
&AutoPay=false
&IncludeDataDisks=false
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyInstanceChargeTypeResponse>
      <RequestId>B61C08E5-403A-46A2-96C1-F7B1216DB10C</RequestId>
      <OrderId>20413515388****</OrderId>
      <FeeOfInstances>
            <FeeOfInstance>
                  <Fee>0</Fee>
                  <InstanceId>i-bp67acfmxazb4p****</InstanceId>
                  <Currency>CNY</Currency>
            </FeeOfInstance>
            <FeeOfInstance>
                  <Fee>0</Fee>
                  <InstanceId>i-bp67acfmxazb4d****</InstanceId>
                  <Currency>CNY</Currency>
            </FeeOfInstance>
      </FeeOfInstances>
</ModifyInstanceChargeTypeResponse>
```

`JSON` format

```
{
    "RequestId":"B61C08E5-403A-46A2-96C1-F7B1216DB10C",
    "OrderId":"20413515388****",
    "FeeOfInstances":
    {
        "FeeOfInstance":[
            {
                "Fee":"0",
                "InstanceId":"i-bp67acfmxazb4p****",
                "Currency":"CNY"
            },
            {
                "Fee":"0",
                "InstanceId":"i-bp67acfmxazb4d****",
                "Currency":"CNY"
            }
        ]
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidParameter.InstanceIds|The specified InstanceIds are invalid.|The error message returned because the specified InstanceIds parameter is invalid.|
|400|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|400|InvalidStatus.ValueNotSupported|%s|The error message returned because the operation is not supported while the resource is in the current state.|
|400|InvalidInstanceChargeType.ValueNotSupported|%s|The error message returned because the specified InstanceChargeType parameter is not supported.|
|400|ExpiredInstance|The specified instance has expired.|The error message returned because the specified instance has expired.|
|403|InvalidInstance.TempBandwidthUpgrade|Cannot switch to Pay-As-You-Go during the period of temporary bandwidth upgrade.|The error message returned because you cannot change the billing method to pay-as-you-go when the bandwidth is being temporarily upgraded.|
|400|InstancesIdQuotaExceed|The maximum number of Instances is exceeded.|The error message returned because the maximum number of instances is exceeded.|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|The error message returned because the specified client token is invalid.|
|400|InvalidInternetChargeType.ValueNotSupported|%s|The error message returned because the specified billing method for network usage is not supported.|
|403|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned because the specified InstanceType parameter does not exist or because you are not authorized to manage instances of the specified instance type.|
|403|InstanceType.Offline|%s|The error message returned because the operation is not supported while the instance type is retired or resources of the instance type are insufficient.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|400|ReleaseTimeHaveBeenSet|The specified instance has been set released time.|The error message returned because an automatic release time has been set for the specified instance.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Add funds to your account and try again.|
|403|Account.Arrearage|Your account has an outstanding payment.|The error message returned because you have overdue payments within your account.|
|400|Throttling|Request was denied due to request throttling, please try again after 5 minutes.|The error message returned because the request is denied due to throttling. Try again 5 minutes later.|
|403|InvalidParameter.NotMatch|%s|The error message returned because a specified parameter is invalid. Check whether parameter conflicts exist.|
|403|InvalidAction|%s|The error message returned because this operation is invalid.|
|400|Throttling|%s|The error message returned because the request is denied due to throttling.|
|400|QuotaExceed.AfterpayInstance|The maximum number of Pay-As-You-Go instances is exceeded: %s|The error message returned because the pay-as-you-go instances of the specified instance type are insufficient. Reduce the number of instances to be created.|
|400|InvalidParameter.Bandwidth|%s|The error message returned because the specified bandwidth is invalid.|
|400|QuotaExceed.RufundVcpu|The maximum number of refund vcpu is exceeded: %s|The error message returned because the number of vCPUs that is used to calculate the refund amount exceeds the upper limit. For more information about the limit, see the return value of the %s placeholder in the error message.|
|400|InvalidPeriod.UnitMismatch|The specified Period must be correlated with the PeriodUnit.|The error message returned because the specified Period parameter is not associated with PeriodUnit.|
|400|InvalidImageType.NotSupported|%s|The error message returned because the specified image type is invalid. Check whether this image type is supported in the region.|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|The error message returned because the expiration date of the instance is later than that of the dedicated host.|
|400|InvalidMarketImageChargeType.NotSupport|The specified chargeType of marketImage is unsupported.|The error message returned because the billing method of the Alibaba Cloud Marketplace image is not supported.|
|403|QuotaExceed.PostPaidDisk|Living postPaid disks quota exceeded.|The error message returned because the maximum number of pay-as-you-go disks has been exceeded.|
|403|ImageNotSupportInstanceType|The specified instanceType is not supported by instance with marketplace image.|The error message returned because the specified Alibaba Cloud Marketplace image does not support the instance type.|
|403|InvalidInstanceType.PhasedOut|This instanceType is no longer offered.|The error message returned because the specified instance type is retired.|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|The error message returned because the operation is not supported by the specified system disk category.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|403|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|The error message returned because you have not completed real-name verification. Complete real-name verification and try again.|
|400|InvalidInstance.NotFoundSystemDisk|The specified instance has no system disk.|The error message returned because the specified instance does not have a system disk attached. Make sure that the specified instance has a system disk attached. You can call the DescribeInstances operation to query the most recent instance list.|
|403|QuotaExceed.ElasticQuota|No additional quota is available for the specified ECS instance type.|The error message returned because the maximum number of instances of the specified instance type in the current region has been reached. Try another region or instance type, or reduce the purchase quantity. You can also go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type.|The error message returned because the maximum number of instances of the specified instance type in the current region has been reached. Try another region or instance type, or reduce the purchase quantity. You can also go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|The error message returned because the maximum number of vCPUs for all instance types has been reached. You can go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type, or the number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|The error message returned because the maximum number of instances of the specified instance type that can be created in the current region has been reached, or because the maximum number of vCPUs for all instance types has been reached. Go to the ECS console or Quota Center to request a quota increase.|
|400|InvalidPeriod|The specified period is not valid.|The error message returned because the specified Period parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

