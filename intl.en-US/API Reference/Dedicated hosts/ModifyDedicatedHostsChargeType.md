# ModifyDedicatedHostsChargeType

You can call this operation to modify the billing method of dedicated hosts.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyDedicatedHostsChargeType&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDedicatedHostsChargeType|The operation that you want to perform. Set the value to ModifyDedicatedHostsChargeType. |
|DedicatedHostIds|String|Yes|\["dh-bp181e5064b5sotr\*\*\*\*","dh-bp18064b5sotrr9c\*\*\*\*"\]|The IDs of the dedicated hosts. The value can be a JSON array that consists of up to 20 dedicated host IDs. Separate multiple dedicated host IDs with commas \(,\). |
|RegionId|String|Yes|cn-hangzhou|The region ID of the dedicated host. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Period|Integer|No|1|The renewal period of the subscription instance. Valid values:

-   When `PeriodUnit` is set to Week, valid values of `Period` are 1, 2, 3, and 4.
-   When `PeriodUnit` is set to Month, valid values of `Period` are 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60. |
|PeriodUnit|String|No|Month|The unit of the renewal duration \(`Period`\). Valid values:

-   Week
-   Month

Default value: Month. |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request without actually making the request. Valid values:

-   true: The validity of the request is checked but resources are not queried. The system checks whether your AccessKey pair is valid, whether RAM users are authorized, and whether required parameters are specified. If the check fails, the corresponding error code is returned. If the check succeeds, the `DryRunOperation` error code is returned.
-   false: The validity of the request is checked. If the check succeeds, a 2XX HTTP status code is returned and the request is made.

Default value: false. |
|AutoPay|Boolean|No|false|Specifies whether to enable automatic payment. Valid values:

-   true: Automatic payment is enabled. Make sure that you have sufficient balance in your account. Otherwise, your order becomes invalid and must be canceled.
-   false: An order is generated but no payment is made.

Default value: true.

**Note:** If you do not have sufficient balance in your account, you can set the `AutoPay` parameter to `false` to generate an unpaid order. Then, you can manually complete the payment for the order. |
|DedicatedHostChargeType|String|No|PrePaid|The new billing method for the dedicated host. Valid values:

-   PrePaid: changes the billing method from pay-as-you-go to subscription.
-   PostPaid: changes the billing method from subscription to pay-as-you-go.

Default value: PrePaid. |
|ClientToken|String|No|e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The `ClientToken` value must contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|DetailFee|Boolean|No|false|Specifies whether to return the billing details of the order when the billing method is changed from subscription to pay-as-you-go.

Default value: false. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|FeeOfInstances|Array of FeeOfInstance| |Details about the charges for the order. |
|FeeOfInstance| | | |
|Currency|String|CNY|The unit of currency for the bill. |
|Fee|String|0|The cost value. |
|InstanceId|String|dh-bp181e5064b5sotrr\*\*\*\*|The ID of the dedicated host. |
|OrderId|String|20413515388\*\*\*\*|The ID of the generated order. |
|RequestId|String|B61C08E5-403A-46A2-96C1-F7B1216DB10C|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyDedicatedHostsChargeType
&RegionId=cn-hangzhou
&InstanceIds=["dh-bp181e5064b5sotr****","dh-bpe5064b5sotrr9c****"]
&Period=1
&PeriodUnit=Month
&AutoPay=false
&IncludeAllDisks=true
&ClientToken=e4567-e89b-12d3-a456-426655440000
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDedicatedHostsChargeTypeResponse>
      <RequestId>B61C08E5-403A-46A2-96C1-F7B1216DB10C</RequestId>
      <OrderId>20413515388****</OrderId>
      <FeeOfInstances>
            <FeeOfInstance>
                  <Fee>0</Fee>
                  <InstanceId>dh-bp181e5064b5sotr****</InstanceId>
                  <Currency>CNY</Currency>
            </FeeOfInstance>
            <FeeOfInstance>
                  <Fee>0</Fee>
                  <InstanceId>dh-bp181e5064b5sotr****</InstanceId>
                  <Currency>CNY</Currency>
            </FeeOfInstance>
      </FeeOfInstances>
</ModifyDedicatedHostsChargeTypeResponse>
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
                "InstanceId":"dh-bp181e5064b5sotr****",
                "Currency":"CNY"
            },
            {
                "Fee":"0",
                "InstanceId":"dh-bp181e5064b5sotr****",
                "Currency":"CNY"
            }
        ]
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidParameter.InstanceIds|The specified InstanceIds are invalid.|The error message returned because the specified DedicatedHostIds parameter is invalid.|
|400|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|400|InvalidStatus.ValueNotSupported|%s|The error message returned because the operation is not supported while the resource is in the current state.|
|400|InvalidInstanceChargeType.ValueNotSupported|%s|The error message returned because the specified DedicatedHostChargeType parameter is invalid. Check related information and try again.|
|400|ExpiredInstance|The specified instance has expired.|The error message returned because the specified instance has expired.|
|400|InstancesIdQuotaExceed|The maximum number of Instances is exceeded.|The error message returned because the maximum number of instances has been reached.|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|The error message returned because the specified ClientToken parameter is invalid.|
|403|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned because the specified instance type does not exist or you are not authorized to manage instances of this instance type.|
|403|InstanceType.Offline|%s|The error message returned because the instance type is retired or instances of this instance type are insufficient.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|400|ReleaseTimeHaveBeenSet|The specified instance has been set released time.|The error message returned because an automatic release time has been set for the specified instance.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Add funds to your account before you proceed.|
|403|Account.Arrearage|Your account has an outstanding payment.|The error message returned because you have overdue payments in your account.|
|400|Throttling|Request was denied due to request throttling, please try again after 5 minutes.|The error message returned because your request is denied due to throttling. Try again five minutes later.|
|403|InvalidParameter.NotMatch|%s|The error message returned because the specified parameter is invalid. Check whether the parameter conflicts with another parameter.|
|403|InvalidAction|%s|The error message returned because this operation is invalid.|
|400|Throttling|%s|The error message returned because the request is denied due to request throttling.|
|400|QuotaExceed.AfterpayInstance|The maximum number of Pay-As-You-Go instances is exceeded: %s|The error message returned because the pay-as-you-go instances of the specified instance type are insufficient. Reduce the number of instances to be created.|
|400|InvalidPeriod.UnitMismatch|The specified Period must be correlated with the PeriodUnit.|The error message returned because the specified Period parameter is not associated with PeriodUnit.|
|400|InvalidImageType.NotSupported|%s|The error message returned because the specified image type is invalid. Check whether this image type is supported in the region.|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|The error message returned because the expiration date of the instance is later than that of the dedicated host.|
|403|QuotaExceed.PostPaidDisk|Living postPaid disks quota exceeded.|The error message returned because the maximum number of pay-as-you-go disks has been reached.|
|403|ImageNotSupportInstanceType|The specified instanceType is not supported by instance with marketplace image.|The error message returned because the specified Alibaba Cloud Marketplace image does not support the specified instance type.|
|403|InvalidInstanceType.PhasedOut|This instanceType is no longer offered.|The error message returned because the specified instance type is no longer available.|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|The error message returned because the operation is not applicable to the specified system disk category.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|The error message returned because you have not completed real-name verification. Complete real-name verification and try again.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

