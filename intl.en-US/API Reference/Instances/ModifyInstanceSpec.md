# ModifyInstanceSpec

You can call this operation to change the instance type and public bandwidth of a pay-as-you-go instance.

## Description

For information about SDK for Python used to change resource configurations, see [Query available resources for configuration changes](~~109517~~).

When you call this operation, take note of the following items:

-   You must have no overdue payments in your account.
-   You can change the public bandwidth of an instance only when the instance is in the **Running** \(`Running`\) or **Stopped** \(`Stopped`\) state.
-   Before you change the instance type of a pay-as-you-go instance, you can call the [DescribeResourcesModification](~~66187~~) operation to query the instance types to which you can change.
-   You can change the instance type of an instance only when the instance is in the **Stopped** \(`Stopped`\) state.
-   You can change only the instance type or the public bandwidth each time.
-   After you change the instance type or the public bandwidth of an instance, you cannot initiate another change for this instance within five minutes.
-   As of November 27, 2020, the peak bandwidth available for you to create ECS instances or change the configurations of ECS instances is subject to throttling policies in your account. To increase the peak bandwidth, submit a ticket. The following throttling policies apply:
    -   In a single region, the sum of actual peak bandwidths of all ECS instances that use the pay-by-traffic billing method for network usage cannot exceed 5 Gbit/s.
    -   In a single region, the sum of actual peak bandwidths of all ECS instances that use the pay-by-bandwidth billing method for network usage cannot exceed 50 Gbit/s.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceSpec&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyInstanceSpec|The operation that you want to perform. Set the value to ModifyInstanceSpec. |
|InstanceId|String|Yes|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance. |
|InstanceType|String|No|ecs.g6.large|The new instance type. For more information, see [Instance families](~~25378~~) or call the [DescribeInstanceTypes](~~25620~~) operation to query the most recent instance type list. |
|InternetMaxBandwidthOut|Integer|No|10|The maximum outbound public bandwidth. Unit: Mbit/s. Valid values: 0 to 100.

**Note:** When the **pay-by-traffic** billing method is used, the peak inbound and outbound bandwidths indicate the upper limits for bandwidths and are used only for reference. In the event of resource contention, the peak bandwidths cannot be guaranteed. If you want guaranteed bandwidths for your instance, use the **pay-by-bandwidth** billing method. |
|InternetMaxBandwidthIn|Integer|No|10|The maximum inbound public bandwidth. Unit: Mbit/s. Valid values:

-   When the purchased outbound public bandwidth is less than or equal to 10 Mbit/s, the valid values of InternetMaxBandwidthIn are 1 to 10 and the default value is 10.
-   When the purchased outbound public bandwidth is greater than 10 Mbit/s, the valid values of InternetMaxBandwidthIn are 1 to the `InternetMaxBandwidthOut` value and the default value is the `InternetMaxBandwidthOut` value.

**Note:** When the **pay-by-traffic** billing method is used, the peak inbound and outbound bandwidths indicate the upper limits for bandwidths and are used only for reference. In the event of resource contention, the peak bandwidths cannot be guaranteed. If you want guaranteed bandwidths for your instance, use the **pay-by-bandwidth** billing method. |
|Temporary.StartTime|String|No|2017-12-05T22:40:00Z|The start time of the temporary bandwidth upgrade. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |
|Temporary.EndTime|String|No|2017-12-05T22:40:00Z|The end time of the temporary bandwidth upgrade. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |
|Temporary.InternetMaxBandwidthOut|Integer|No|50|The maximum outbound public bandwidth after the temporary bandwidth upgrade. Valid values: 1 to 100.

**Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|Async|Boolean|No|false|Specifies whether to submit an asynchronous request.

Default value: false. |
|AllowMigrateAcrossZone|Boolean|No|false|Specifies whether to enable cross-cluster instance type upgrade.

Default value: false.

When `AllowMigrateAcrossZone` is set to true and you upgrade the instance configurations based on the returned information, take note of the following items:

Instances in the classic network:

-   For retired instance types, when a non-I/O optimized instance is upgraded to an I/O optimized instance, the private IP address, disk device names, and software license code of the instance are changed. For information about retired instance types, see [Retired instance types](~~55263~~). For Linux instances, basic disks \(`cloud`\) are identified as xvd\*, such as **xvda** and **xvdb**. Ultra disks \(`cloud_efficiency`\) and standard SSDs \(`cloud_ssd`\) are identified as vd\*, such as **vda** and **vdb**.
-   For instance families available for purchase, when the instance type of an instance is changed, the private IP address of the instance is also changed. For information about instance families available for purchase, see [Instance families](~~25378~~).

Instances in VPCs: For retired instance types, when a non-I/O optimized instance is upgraded to an I/O optimized instance, the disk device names and software license codes of the instance are changed. For information about retired instance types, see [Retired instance types](~~55263~~). For Linux instances, basic disks \(`cloud`\) are identified as xvd\*, such as **xvda** and **xvdb**. Ultra disks \(`cloud_efficiency`\) and standard SSDs \(`cloud_ssd`\) are identified as vd\*, such as **vda** and **vdb**. |
|SystemDisk.Category|String|No|cloud\_ssd|The category of the system disk. This parameter is valid only when you upgrade an instance of a retired instance type to an instance type of an available instance family and upgrade a non-I/O optimized instance to an I/O optimized instance. For more information, see [Retired instance types](~~55263~~) and [Instance families](~~25378~~). Valid values:

-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD |
|ClientToken|String|No|0c593ea1-3bea-11e9-b96b-88e9fe637760|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How can I ensure idempotence?](~~25693~~) |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceSpec
&InstanceId=i-bp67acfmxazb4p****
&InstanceType=ecs.g6.large
&InternetMaxBandwidthOut=10
&ClientToken=0c593ea1-3bea-11e9-b96b-88e9fe637760
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyInstanceSpecResponse>
     <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceSpecResponse>
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
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|The error message returned because the specified InternetChargeType parameter is invalid.|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType does not exist or beyond the permitted range.|The error message returned because the specified InstanceType parameter does not exist or you are not authorized to manage instances of this instance type.|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|The error message returned because you are not authorized to use the specified instance type.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist. Check whether the instance ID is correct.|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned because the specified InstanceType parameter does not exist or you are not authorized to manage instances of this instance type.|
|400|InvalidParameter|The specified parameter "InternetMaxBandwidthOut" is not valid.|The error message returned because the specified InternetMaxBandwidthOut parameter is invalid.|
|400|InvalidParameter.Mismatch|Too many parameters in one request.|The error message returned because the request contains invalid parameters.|
|403|CategoryViolation|The specified instance does not support this operation because of its disk category.|The error message returned because the configurations of instances that are attached with local disks cannot be upgraded or downgraded.|
|403|InvalidStatus.ValueNotSupported|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|The error message returned because the operation is not supported while the instance is locked for security reasons.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Add funds to your account and try again.|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|The error message returned because the billing method of the instance does not support this operation.|
|403|OperationDenied|The specified instance is out of usage.|The error message returned because the resource inventory of the specified instance type is insufficient.|
|400|BandwidthUpgradeDenied.EipBoundInstance|The specified VPC instance has bound EIP, temporary bandwidth upgrade is denied.|The error message returned because the instance is associated with an elastic IP address \(EIP\) and cannot have its bandwidth temporarily upgraded.|
|404|MissingTemporary.StartTime|Temporary.StartTime is not specified.|The error message returned because the Temporary.StartTime parameter is not specified.|
|404|MissingTemporary.EndTime|Temporary.EndTime is not specified.|The error message returned because the Temporary.EndTime parameter is not specified.|
|400|InvalidTemporary.StartTime|The specifed Temporary.StartTime is not valid.|The error message because the specified Temporary.StartTime parameter is invalid.|
|400|InvalidTemporary.EndTime|The specifed Temporary.EndTime is not valid.|The error message returned because the specified Temporary.EndTime parameter is invalid.|
|403|LastTokenProcessing|The last token request is processing.|The error message returned because the previous token request is being processed. Try again later.|
|400|Downgrade.NotSupported|Downgrade operation is not supported.|The error message returned because the downgrade operation is not supported.|
|403|InstanceSpecModification.NotEffective|The specified instance has been reserved for making a spec modification and not taken effective in the current contract period.|The error message returned because the instance is reserved due to specification changes. Changes made to it cannot take effect during the current contract period.|
|400|DependencyViolation.InstanceType|The current InstanceType cannot be changed to the specified InstanceType.|The error message returned because the current instance type cannot be changed to the specified instance type.|
|403|InvalidInstanceType.ValueNotSupported|The specified zone does not offer the specified instancetype.|The error message returned because the specified instance type is unavailable in the specified region.|
|403|ImageNotSupportInstanceType|The specified image do not support the InstanceType instance.|The error message returned because the specified image does not support instances of the specified instance type.|
|400|Account.Arrearage|Your account has an outstanding payment.|The error message returned because you have overdue payments in your account.|
|400|InvalidParameter.Bandwidth|The specified parameter Bandwidth is not valid.|The error message returned because the specified bandwidth is invalid.|
|400|InvalidParameter.Conflict|The specified image does not support the specified instance type.|The error message returned because the specified image does not support the specified instance type.|
|400|InvalidParameter.AllowMigrateAcrossZone|The specified parameter CanMigrateAcrossZone is not valid.|The error message returned because the specified AllowMigrateAcrossZone parameter is invalid.|
|400|InvalidParam.SystemDiskCategory|The specified param SystemDisk.Category is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|400|Throttling|Request was denied due to request throttling, please try again after 5 minutes.|The error message returned because your current request is denied due to throttling. Try again five minutes later.|
|400|InvalidInstanceStatus.NotStopped|The specified Instance status is not stopped.|The error message returned because the specified instance is not in the Stopped state.|
|403|InstanceType.Offline|The specified InstanceType has been offline|The error message returned because the specified instance type is retired. Select another instance type and try again.|
|400|InvalidAction|Specified action is not valid.|The error message returned because the operation is invalid.|
|400|IdempotenceParamNotMatch|There is a idempotence signature mismatch between this and last request.|The error message returned because this request and the previous request contain the same client token but different parameters.|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|The error message returned because the specified ClientToken parameter is invalid.|
|400|Price.PricePlanResultNotFound|The internetMaxBandwidthIn or internetMaxBandwidthOut provided is invalid.|The error message returned because specified internetMaxBandwidthIn or internetMaxBandwidthOut parameter is invalid.|
|403|InvalidParameter.NotMatch|%s|The error message returned because a specified parameter is invalid. Check whether the parameter conflicts with another parameter.|
|403|InvalidInstance.EipNotSupport|The specified instance with eip is not supported, please unassociate eip first.|The error message returned because the operation is not supported while an EIP is associated with this instance. Disassociate the EIP first.|
|400|InvalidAction.NotSupport|The ecs on dedicatedHost not support modify instanceType.|The error message returned because you cannot change the instance types of instances hosted on dedicated hosts.|
|400|InvalidMarketImageStatus.NotSupported|The status of specified market image does not support this operation.|The error message returned because the operation is not supported while the specified Alibaba Cloud Marketplace image is in the current state.|
|403|OperationDenied.NoStock|The resource is out of usage.|The error message returned because the instance is not in the Running state. Start the instance or check whether the operation is valid.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|OperationDenied|%s|The error message returned because the operation is denied.|
|403|InvalidOperation.Ipv4CountExceeded|%s|The error message returned because the maximum number of IPv4 addresses has been reached.|
|403|InvalidOperation.Ipv6CountExceeded|%s|The error message returned because the maximum number of IPv6 addresses has been reached.|
|403|InvalidOperation.Ipv6NotSupport|%s|The error message returned because IPv6 addresses do not support the current operation.|
|403|InvalidOperation.InstanceWithEipNotSupport|The special instance with eip not support operate, please unassociate eip first.|The error message returned because the operation is not supported while an EIP is associated with this instance. Disassociate the EIP address first.|
|403|SecurityRisk.3DVerification|We have detected a security risk with your default credit or debit card. Please proceed with verification via the link in your email.|The error message returned because risks are detected in your default credit card or debit card. Click the link in the email for verification.|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|The error message returned because the specified InstanceChargeType parameter does not exist.|
|403|QuotaExceed.ElasticQuota|No additional quota is available for the specified ECS instance type.|The error message returned because the maximum number of instances of the specified instance type that can be created in the current region has been reached. Try another region or instance type, or reduce the purchase quantity. You can also go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type.|The error message returned because the maximum number of instances of the specified instance type that can be created in the current region has been reached. Try another region or instance type, or reduce the purchase quantity. You can also go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|The error message returned because the maximum number of vCPUs for all instance types has been reached. Go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type, or the number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|The error message returned because the maximum number of instances of the specified instance type that can be created in the current region has been reached, or because the maximum number of vCPUs for all instance types has been reached. Go to the ECS console or Quota Center to request a quota increase.|
|400|InvalidOperation.VpcHasEnabledAdvancedNetworkFeature|The specified vpc has enabled advanced network feature.|The error message returned because the specified VPC has advanced features enabled. You cannot create instances that are of low specifications in the VPC.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

