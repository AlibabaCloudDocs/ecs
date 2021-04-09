# AllocateDedicatedHosts

You can call this operation to create one or more pay-as-you-go or subscription dedicated hosts. A dedicated host provides a dedicated physical server for a single tenant. You can create ECS instances on a dedicated host and obtain the attributes of the physical server.

## Description

Before you create a dedicated host, you can call the [DescribeAvailableResource](~~66186~~) operation to query the available resources in a specific region or zone.

We recommend that you understand the billing methods of resources before you create a dedicated host. You are charged for resources used by the created dedicated host. For more information, see [Billing overview](~~68978~~).

-   You can create a maximum of 100 pay-as-you-go or subscription dedicated hosts at a time.
-   After a dedicated host is created, you can use its ID that is returned by the system as the value of a request parameter to call the [DescribeDedicatedHosts](~~134242~~) operation to query the status of the dedicated host.
-   After you submit a request to create a dedicated host, an error is returned if a specific parameter is invalid or the requested resources are insufficient. For more information about error reasons, see the "Error codes" section in this topic.
-   After a dedicated host is created, you can call the [ModifyInstanceDeployment](~~134248~~) operation to migrate ECS instances from a shared host to the dedicated host. You can also migrate ECS instances from another dedicated host to the created dedicated host.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=AllocateDedicatedHosts&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AllocateDedicatedHosts|The operation that you want to perform. Set the value to AllocateDedicatedHosts. |
|DedicatedHostType|String|Yes|ddh.c5|The type of the dedicated host. You can call the [DescribeDedicatedHostTypes](~~134240~~) operation to query the most recent list of dedicated host types. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the dedicated host. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Tag.N.Key|String|No|Environment|The key of tag N to be bound to the dedicated host. Valid values of N: 1 to 20.

This parameter cannot be an empty string. It can be up to 128 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. |
|Tag.N.Value|String|No|Production|The value of tag N to be bound to the dedicated host. Valid values of N: 1 to 20.

This parameter can be an empty string. It can be up to 128 characters in length and cannot start with acs: or contain http:// or https://. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4ph\*\*\*|The ID of the resource group to which to assign the dedicated host. |
|ZoneId|String|No|cn-hangzhou-f|The zone ID of the dedicated host.

This parameter is empty by default. If you do not specify a zone, the system automatically selects a zone. |
|DedicatedHostName|String|No|myDDH|The name of the dedicated host. The name must be 2 to 128 characters in length, and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://. |
|DedicatedHostClusterId|String|No|dc-bp12wlf6am0vz9v2\*\*\*\*|The ID of the dedicated host cluster to which to assign the dedicated host. |
|ActionOnMaintenance|String|No|Migrate|The policy used to migrate the instances deployed on the dedicated host when the dedicated host fails or needs to be repaired online. Valid values:

-   Migrate: The instances are migrated to another physical server and restarted.

If the dedicated host is attached with cloud disks, the default value is Migrate.

-   Stop: The instances are stopped. If the dedicated host cannot be repaired, the instances are migrated to another physical server and restarted.

If the dedicated host is attached with local disks, the default value is Stop. |
|NetworkAttributes.SlbUdpTimeout|Integer|No|60|The timeout period for a UDP session between a Server Load Balancer \(SLB\) instance and the dedicated host. Unit: seconds. Valid values: 15 to 310. |
|NetworkAttributes.UdpTimeout|Integer|No|60|The timeout period for a UDP session between a user and an Alibaba Cloud service on the dedicated host. Unit: seconds. Valid values: 15 to 310. |
|Description|String|No|This-is-my-DDH|The description of the dedicated host. It must be 2 to 256 characters in length and cannot start with http:// or https://. |
|AutoPlacement|String|No|off|Specifies whether to add the dedicated host to the resource pool for automatic deployment. If you create an ECS instance on a dedicated host without specifying the **DedicatedHostId** parameter, Alibaba Cloud automatically selects a dedicated host from the resource pool to host the instance. For more information, see [Automatic deployment](~~118938~~). Valid values:

-   on: adds the dedicated host to the resource pool for automatic deployment.
-   off: does not add the dedicated host to the resource pool for automatic deployment.

Default value: on.

**Note:** If you do not want to add the dedicated host to the resource pool for automatic deployment, set the value to off. |
|CpuOverCommitRatio|Float|No|1|The CPU overcommit ratio. You can configure CPU overcommit ratios only for the following dedicated host types: g6s, c6s, and r6s. Valid values: 1 to 5.

The CPU overcommit ratio affects the number of available vCPUs on a dedicated host. You can use the following formula to calculate the number of available vCPUs on a dedicated host: Number of available vCPUs = Number of physical CPU cores × 2 × CPU overcommit ratio. For example, the number of physical CPU cores on each g6s dedicated host is 52. If you change the CPU overcommit ratio of a g6s dedicated host to 4, the number of available vCPUs on the dedicated host is 416. For scenarios that have minimal requirements on CPU stability or where CPU load is not heavy, such as development and test environments, you can increase the number of available vCPUs on a dedicated host by increasing the CPU overcommit ratio. This way, you can deploy more ECS instances of the same specifications on the dedicated host and reduce the unit deployment cost. |
|MinQuantity|Integer|No|2|Specifies the minimum number of dedicated hosts to purchase. Valid values: 1 to 100

**Note:** If the number of available dedicated hosts is less than the minimum number of dedicated hosts to create, the dedicated hosts fail to be created. |
|ChargeType|String|No|PrePaid|The billing method of the dedicated host. Valid values:

-   PrePaid: subscription. If you set this parameter to PrePaid, make sure that you have sufficient account balance or credit. Otherwise, InvalidPayMethod is returned.
-   Default value: PostPaid. |
|Quantity|Integer|No|2|The number of dedicated hosts that you want to create. Valid values: 1 to 100.

Default value : 1. |
|Period|Integer|No|6|The subscription period of the dedicated host. The `Period` parameter takes effect and is required only when the `ChargeType` parameter is set to `PrePaid`. Valid values:

-   If the PeriodUnit parameter is set to Month, valid values of Period are 1, 2, 3, 4, 5, 6, 7, 8, and 9.
-   If the PeriodUnit parameter is set to Year, valid values of Period are 1, 2, 3, 4, and 5. |
|PeriodUnit|String|No|Month|The unit of the subscription period of the dedicated host. Valid values:

-   Month
-   Year

Default value: Month. |
|AutoRenew|Boolean|No|false|Specifies whether to automatically renew the subscription dedicated host.

**Note:** The **AutoRenew** parameter takes effect only when the **ChargeType** parameter is set to PrePaid.

Default value: false. |
|AutoRenewPeriod|Integer|No|1|The auto-renewal period of the dedicated host. Unit: months. Valid values: 1, 2, 3, 6, and 12.

**Note:** The **AutoRenewPeriod** parameter takes effect and is required only when the **AutoRenew** parameter is set to true. |
|AutoReleaseTime|String|No|2019-08-21T12:30:24Z|The automatic release time of the dedicated host. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.

**Note:**

-   It must be at least half an hour later than the current time.
-   It must be at most three years later than the current time.
-   If the value of the seconds \(ss\) is not 00, it is automatically set to 00. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value must contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DedicatedHostIdSets|List|"DedicatedHostIdSets":\{"DedicatedHostId":\["dh-bp67acfmxazb4p\*\*\*\*", "dh-bp67acfmxazb4d\*\*\*\*"\]\}|The IDs of the dedicated hosts. |
|RequestId|String|E2A664A6-2933-4C64-88AE-5033D003EADF|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=AllocateDedicatedHosts
&RegionId=cn-hangzhou
&DedicatedHostType=ddh.sn1ne
&Quantity=2
&ChargeType=PostPaid
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AllocateDedicatedHostsResponse>
    <RequestId>E2A664A6-2933-4C64-88AE-5033D003EADF</RequestId>
    <DedicatedHostIdSets>
        <DedicatedHostId>dh-bp67acfmxazb4p****</DedicatedHostId>
        <DedicatedHostId>dh-bp67acfmxazb4d****</DedicatedHostId>
    </DedicatedHostIdSets>
</AllocateDedicatedHostsResponse>
```

`JSON` format

```
{
    "RequestId":"E2A664A6-2933-4C64-88AE-5033D003EADF",
    "DedicatedHostIdSets":{
        "DedicatedHostId":[
            "dh-bp67acfmxazb4p****",
            "dh-bp67acfmxazb4d****"
        ]
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|The error message returned because you are not authorized to use the specified instance type.|
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|The error message returned because the specified Description parameter is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|403|OperationDenied|The creation of Host to the specified Zone is not allowed.|The error message returned because you are not authorized to create a dedicated host in the specified zone.|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone; try other types of resources or other regions and zones.|The error message returned because the requested resources are insufficient.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|OperationDenied|Sales of this resource are temporarily suspended in the specified region; please try again later.|The error message returned because the requested resource is unavailable in the specified region. Try again later.|
|400|InvalidParameter.Conflict|The specified region and cluster do not match.|The error message returned because the specified region and cluster do not correspond to each other.|
|403|NodeControllerUnavailable|The Node Controller is temporarily unavailable.|The error message returned because the node controller is unavailable.|
|404|OperationDenied|Another Host has been creating|The error message returned because another host is being created.|
|403|OperationDenied|The resource is out of usage.|The error message returned because the instance is not in the Running state. Start the instance or check whether the operation is valid.|
|404|PaymentMethodNotFound|No payment method has been registered on the account.|The error message returned because you have not configured a payment method for your account.|
|404|InvalidDedicatedHostName.Malformed|The specified parameter DedicatedHostName is not valid.|The error message returned because the specified DedicatedHostName parameter is invalid.|
|403|InvalidParameter.ResourceOwnerAccount|ResourceOwnerAccount is Invalid.|The error message returned because the specified ResourceOwnerAccount parameter is invalid.|
|403|InvalidUserData.Forbidden|User not authorized to input the parameter "UserData", please apply for permission "UserData"|The error message returned because you are not authorized to manage user data. Apply for the permission first.|
|403|Zone.NotOpen|The specified zone is not granted to you to buy resources yet.|The error message returned because you are not authorized to purchase resources in the specified zone.|
|403|Zone.NotOnSale|The specified zone is not available for purchase.|The error message returned because the requested resources are unavailable in the specified zone. Change the resource type or select a different zone.|
|403|InvalidDedicatedHostType.ValueNotSupported|The specified DedicatedHostType does not exist or beyond the permitted range.|The error message returned because the specified DedicatedHostType parameter does not exist.|
|403|InvalidDedicatedHostType.ZoneNotSupported|The specified zone does not support this dedicatedHostType.|The error message returned because the specified dedicated host type is not supported in the specified zone.|
|400|InvalidAutoRenewPeriod.ValueNotSupported|The specified autoRenewPeriod is not valid.|The error message returned because the specified AutoRenewPeriod parameter is invalid.|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|The error message returned because the specified Tag.N.Key parameter is invalid.|
|400|InvalidDedicatedHostType.ValueNotSupported|%s|The error message returned because the specified DedicatedHostType parameter is invalid.|
|400|RegionUnauthorized|%s|The error message returned because you are not authorized to perform the operation in the specified region.|
|500|InternalError|%s|The error message returned because an internal error has occurred.|
|400|Zone.NotOnSale|%s|The error message returned because the requested resources are unavailable in the specified zone.|
|400|OperationDenied|The specified DedicatedHostType or Zone is not available or not authorized.|The error message returned because the specified dedicated host type or zone is unavailable or you are not authorized to manage the resources.|
|400|InvalidPeriodUnit.ValueNotSupported|The specified parameter PeriodUnit is not valid.|The error message returned because the specified PeriodUnit parameter is invalid.|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|The error message returned because the specified Tag.N.Value parameter is invalid.|
|403|InvalidParameter.NotMatch|%s|The error message returned because a specified parameter is invalid. Check whether the parameters conflict.|
|403|Account.Arrearage|Your account has been in arrears.|The error message returned because you have insufficient balance within your account. Add funds to your account and try again.|
|400|QuotaExceed.AfterpayDedicatedHost|The maximum number of Pay-As-You-Go DedicatedHosts is exceeded: %s|The error message returned because the pay-as-you-go resources of the specified dedicated host type are insufficient. Reduce the number of dedicated hosts to be created.|
|400|InvalidChargeType.ValueNotSupported|ChargeType is not valid|The error message returned because the specified ChargeType parameter is invalid.|
|400|InvalidParameter.SlbUdpTimeout|The specified value is invalid.|The error message returned because the specified NetworkAttributes.SlbUdpTimeout parameter is invalid.|
|400|InvalidParameter.UdpTimeout|The specified value is invalid.|The error message returned because the specified NetworkAttributes.UdpTimeout parameter is invalid.|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|The error message returned because the specified tag key already exists. Tag keys must be unique.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

