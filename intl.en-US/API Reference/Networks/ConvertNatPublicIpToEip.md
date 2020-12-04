# ConvertNatPublicIpToEip

You can call this operation to convert the public IP address of a VPC-type instance to an elastic IP address \(EIP\).

## Description

After a public IP address is converted to an EIP, the EIP will be billed separately. Make sure that you have fully understood the billing methods of EIPs. For more information, see [Billing overview](~~122035~~).

Before you call this operation, make sure that the following requirements are met:

-   The instance is in the **Stopped** \(`Stopped`\) or **Running** \(`Running`\) state.
-   The instance has no EIPs associated.
-   The instance has no configuration change tasks that have not taken effect.
-   The public bandwidth of the instance cannot be 0 Mbit/s.
-   The public bandwidth of the instance is billed on a pay-by-traffic basis.
-   If the instance is a VPC-type subscription instance, it does not expire within 24 hours.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ConvertNatPublicIpToEip&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ConvertNatPublicIpToEip|The operation that you want to perform. Set the value to ConvertNatPublicIpToEip. |
|InstanceId|String|Yes|i-bp171jr36ge2ulvk\*\*\*\*|The ID of the instance for which you want to convert its public IP address to an EIP. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ConvertNatPublicIpToEip
&RegionId=cn-hangzhou
&InstanceId=i-bp171jr36ge2ulvk****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ConvertNatPublicIpToEipResponse>
      <RequestId>B154D309-F3E1-4AB7-BA94-FEFCA8B89001</RequestId>
</ConvertNatPublicIpToEipResponse>
```

`JSON` format

```
{
   "RequestId":"B154D309-F3E1-4AB7-BA94-FEFCA8B89001"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|InvalidInstanceId.PlanedChange|%s|The error message returned because the instance has scheduled configuration change tasks.|
|403|InvalidEndTime.OperateNotSupport|%s|The error message returned because this operation is not supported while the instance is in the current state.|
|403|InvalidInstanceStatus.Released|%s|The error message returned because the specified operation is invalid. Check whether the instance status is correct.|
|403|IncorrectInstanceStatus|%s|The error message returned because the operation is not supported while the instance is in the current state.|
|403|OperationDenied|%s|The error message returned because the operation is denied.|
|404|InvalidInstanceId.NotFound|%s|The error message returned because the specified InstanceId parameter does not exist.|
|403|InvalidInternetChargeType.ValueNotSupported|%s|The error message returned because the specified InternetChargeType parameter is not supported. Check whether the parameter is correct.|
|403|MaxEIPQuotaExceeded|The number of EIP exceeds the limit per region.|The error message returned because the maximum number of EIPs in the current region has been reached.|
|403|InvalidInstance.OverduePayment|%s|The error message returned because you have overdue payments in your account. Create an instance again or contact the customer service.|
|403|InvalidInstance.OverduePayment|The special instance due to overdue payment,this operation is not supported.|The error message returned because you have overdue payments in your account. Top up your account before proceeding.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Add funds to your account before you proceed.|
|403|Forbidden.RiskControl|This operation is forbidden by Aliyun RiskControl system.|The error message returned because the operation is forbidden by the risk control system.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

