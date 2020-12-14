# ModifyPrepayInstanceSpec

You can call this operation to upgrade or downgrade the instance type of a subscription ECS instance. The new instance type takes effect for the remaining lifecycle of the instance.

## Description

Before you call this operation, make sure that you have fully understood the billing methods and pricing schedule of [ECS](https://www.alibabacloud.com/product/ecs#pricing).

Before you change the instance type of a subscription instance, you can call the [DescribeResourcesModification](~~66187~~) operation to query the instance types to which you can change. For more information, see the SDK for Python example in [Query available resources for configuration changes](~~109517~~).

When you call this operation, take note of the following items:

-   You cannot change the instance type of an expired instance. You can renew the instance and try again.
-   When you downgrade the instance type of an instance, take note of the following items:
    -   The instance must be in the **Stopped** \(`Stopped`\) state.
    -   You must specify the operation type by setting `OperatorType` to downgrade.
    -   You can downgrade the configurations of an instance a maximum of three times. Therefore, a maximum of three refunds for price difference can be made. Downgrade operations include instance type downgrades, bandwidth configuration downgrades, and the change of the disk billing method from subscription to pay-as-you-go.
    -   The price difference is refunded to the payment account you used. Vouchers that have been redeemed are not refundable.
-   This operation is asynchronous and you must wait for 5 to 10 seconds for the instance type change to complete. Then, you must restart the instance by calling the RebootInstance operation or by using the ECS console for the instance type change to take effect. If you restart only the operating system, the change does not take effect.
    -   If the instance is in the **Stopped** state, you need only to start the instance. You do not need to restart the instance after it enters the Running state.
    -   If `RebootWhenFinished` is set to true for the instance, you do not need to manually restart the instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyPrepayInstanceSpec&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyPrepayInstanceSpec|The operation that you want to perform. Set the value to ModifyPrepayInstanceSpec. |
|InstanceId|String|Yes|i-bp67acfmxazb4ph\*\*\*\*|The ID of the instance. |
|InstanceType|String|Yes|ecs.g5.xlarge|The new instance type. For information about available instance types, see [Instance families](~~25378~~) or call the [DescribeInstanceTypes](~~25620~~) operation. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|OperatorType|String|No|upgrade|The operation type. Default value: upgrade. Valid values:

-   upgrade: upgrades the instance type. Make sure that the balance in your account is sufficient.
-   downgrade: downgrades the instance type. When the new instance type specified by the `InstanceType` parameter has lower specifications than the current instance type, you must set `OperatorType` to downgrade.

**Note:** For more information about the precautions on upgrading or downgrading instance types, see the preceding "Description" section in this topic. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value must contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [Ensure idempotence](~~25693~~). |
|AutoPay|Boolean|No|true|Specifies whether to enable automatic payment when you upgrade the instance type. Default value: true. Valid values:

-   true: Automatic payment is enabled.

**Note:** Make sure that your account has sufficient balance. Otherwise, your order becomes invalid and you have to cancel the order. If you do not have sufficient balance in your account, you can set the `AutoPay` parameter to `false` to generate an unpaid order. Then, you can log on to the ECS console to pay for the order.

-   false: An order is generated but no payment is made.

When `OperatorType` is set to `downgrade`, `AutoPay` is ignored. |
|MigrateAcrossZone|Boolean|No|false|Specifies whether to support cross-cluster instance type upgrades.

Default value: false.

When the MigrateAcrossZone parameter is set to true and you upgrade the ECS instance based on the returned information, take note of the following items:

Classic network-type instances:

-   For retired instance types, when a non-I/O optimized instance is upgraded to an I/O optimized instance, the private IP address, disk device name, and software license codes of the instance are changed. For more information, see [Retired instance types](~~55263~~). For Linux instances, basic disks \(cloud\) are identified as xvd\* such as xvda and xvdb, and ultra disks \(cloud\_efficiency\) and standard SSDs \(cloud\_ssd\) are identified as vd\*, such as vda and vdb.
-   For available instance families, private IP addresses are changed after the instance types are upgraded. For more information, see [Instance families](~~25378~~).

VPC-type instances: For retired instance types, when a non-I/O optimized instance is upgraded to an I/O optimized instance, the disk device names and software license codes of the instance are changed. For Linux instances, basic disks \(cloud\) are identified as xvd\* such as xvda and xvdb, and ultra disks \(cloud\_efficiency\) and standard SSDs \(cloud\_ssd\) are identified as vd\*, such as vda and vdb. |
|SystemDisk.Category|String|No|cloud\_efficiency|The new category of the system disk. This parameter is valid only when you upgrade an instance from a retired instance type to an available instance type or upgrade a non-I/O optimized instance to an I/O optimized instance. For more information, see [Retired instance types](~~55263~~) and [Instance families](~~25378~~). Valid values:

-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD |
|RebootTime|String|No|2018-01-01T12:05Z|The restart time of the instance. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |
|EndTime|String|No|2018-01-01T12:05Z|The end time of the temporary change. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |
|RebootWhenFinished|Boolean|No|false|Specifies whether to restart the instance immediately after the instance type change is complete. Valid values:

-   true
-   false

Default value: false

**Note:** If the instance is in the **Stopping** state, even if you set `RebootWhenFinished` to true, the instance status remains unchanged and no operations are performed. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OrderId|String|1234567890|The ID of the generated order. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyPrepayInstanceSpec
&RegionId=cn-hangzhou
&InstanceId=i-bp67acfmxazb4ph****
&InstanceType=ecs.g5.xlarge
&AutoPay=true
&OperatorType=upgrade
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyPrepayInstanceSpecResponse>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
      <OrderId>1234567890</OrderId>
</ModifyPrepayInstanceSpecResponse>
```

`JSON` format

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "OrderId": "1234567890"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned because the specified RegionId parameter does not exist.|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|The error message returned because you are not authorized to use the specified instance type.|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned because the specified instance type does not exist or you are not authorized to manage instances of this instance type.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|404|BillingMethodNotFound|The account has not chosen any billing method.|The error message returned because no billing method is selected for this account.|
|403|OperationDenied.NoStock|The specified instance is out of usage.|The error message returned because the resource inventory of the specified instance type is insufficient.|
|400|InvalidBillingMethod.ValueNotSupported|The operation is not permitted due to an invalid billing method of the instance.|The error message returned because the operation is not supported due to the invalid billing method of the instance.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist.|
|400|InvalidInstance.PurchaseNotFound|The specified instance has no purchase history.|The error message returned because the order record for this instance does not exist.|
|400|InvalidInstanceType.NotSupported|The specified InstanceType is not Supported.|The error message returned because the specified InstanceType parameter is invalid.|
|400|OrderCreationFailed|Order creation failed, please check your params and try it again later.|The error message returned because the order fails to be created. Check your parameters and try again later.|
|400|Throttling|You have made too many requests within a short time; your request is denied due to request throttling.|The error message returned because your request is denied due to throttling. Try again later.|
|400|Account.Arrearage|Your account has an outstanding payment.|The error message returned because you have overdue payments in your account.|
|403|InvalidUser.PassRoleForbidden|The RAM user does not have privilege to pass a role.|The error message returned because RAM users are not authorized to assign RAM roles.|
|400|InvalidRebootTime.MalFormed|The specified rebootTime is not valid.|The error message returned because the specified RebootTime parameter is invalid.|
|400|InvalidRebootTime.ValueNotSupported|The specified RebootTime is not valid.|The error message returned because the specified RebootTime parameter is invalid.|
|403|ImageNotSupportInstanceType|The specified image does not support the specified InstanceType.|The error message returned because the specified image cannot be used on instances of the specified instance type.|
|403|InstanceType.Offline|%s|The error message returned because the instance type is retired or has insufficient resources.|
|400|IdempotenceParamNotMatch|Request uses a client token in a previous request but is not identical to that request.|The error message returned because the ClientToken value in this request is identical to that in the previous request but some other parameters in this request are different from those in the previous request.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|400|IdempotenceParamNotMatch|%s|The error message returned because the idempotent parameters do not match.|
|400|InvalidInstanceChargeType.ValueNotSupported|%s|The error message returned because the payment type is not supported. Check the related information and try again.|
|400|InvalidStatus.NotStopped|Instance status must be stopped.|The error message returned because the instance is not in the Stopped state. The operation can be performed only when the instance is in the Stopped state.|
|400|InvalidAction|%s|The error message returned because this operation is invalid.|
|400|InstanceDowngrade.QuotaExceed|Quota of instance downgrade is exceed.|The error message returned because the maximum number of configuration downgrades allowed for the instance has been reached.|
|400|InvalidInstanceType.ValueNotSupported|%s|The error message returned because the operation is not supported by the specified instance type.|
|403|InvalidParameter.InstanceId|%s|The error message returned because the specified InstanceId parameter is invalid.|
|400|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|403|OperationDenied|%s|The error message returned because the operation is denied.|
|403|ImageNotSupportInstanceType|The specified instanceType is not supported by instance with marketplace image.|The error message returned because the specified Alibaba Cloud Marketplace image does not support the instance type.|
|403|InvalidInstanceStatus|The current status of the instance does not support this operation.|The error message returned because the operation is not supported while the instance is in the current state.|
|403|InvalidInstance.PreInstanceExpired|Instance business status is not Expired|The error message returned because the current instance has expired.|
|403|InvalidInstance.EipNotSupport|The special instance with eip not support operate, please unassociate eip first.|The error message returned because the operation is not supported while an elastic IP address \(EIP\) is associated with this instance. Disassociate the EIP first.|
|400|OperationDenied|The current user does not support this operation.|The error message returned because the specified account does not support this operation.|
|403|OperationDenied.LocalDiskUnsupported|The configuration change is not allowed when the specified instance has local disks mounted.|The error message returned because the instance types of instances that have local disks attached cannot be changed.|
|403|OperationDenied.NoStock|The resource is out of stock in the specified zone. Please try other types, or choose other regions and zones.|The error message returned because the specified resource is unavailable in the specified zone. Try other resource types, or select other regions or zones.|
|400|LastOrderProcessing|The previous order is still processing, please try again later.|The error message returned because the order is being processed. Try again later.|
|403|InvalidOperation.Ipv4CountExceeded|%s|The error message returned because the maximum number of IPv4 addresses has been reached.|
|403|InvalidOperation.Ipv6CountExceeded|%s|The error message returned because the maximum number of IPv6 addresses has been reached.|
|403|InvalidOperation.Ipv6NotSupport|%s|The error message returned because IPv6 does not support the operation.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|QuotaExceed.ElasticQuota|No additional quota is available for the specified ECS instance type.|The error message returned because the maximum number of instances of the specified instance type in the current region has been reached. Try another region or instance type, or reduce the purchase quantity. You can also go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type.|The error message returned because the maximum number of instances of the specified instance type in the current region has been reached. Try another region or instance type, or reduce the purchase quantity. You can also go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|The error message returned because the maximum number of vCPUs for all instance types has been reached. Go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type, or the number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|The error message returned because the maximum number of instances of the specified instance type in the current region has been reached, or because the maximum number of vCPUs for all instance types has been reached. Go to the ECS console or Quota Center to request a quota increase.|
|400|InvalidOperation.VpcHasEnabledAdvancedNetworkFeature|The specified vpc has enabled advanced network feature.|The error message returned because the specified VPC has advanced features enabled. You cannot create instances that have low specifications in the VPC.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

