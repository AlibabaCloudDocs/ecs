# ModifyInstanceDeployment

You can call this operation to modify the deployment set of an ECS instance or migrate an instance to a dedicated host. You can change the instance type of an instance when you migrate the instance.

## Description

Before you migrate an instance to a dedicated host or change the instance type of an instance when you migrate the instance, make sure that the following requirements are met:

-   The instance is in the **Stopped** \(Stopped\) state before it is migrated. The instance is automatically restarted after it is migrated.
-   The network type of the instance is VPC.
-   The instance and the dedicated host belong to the same region and zone and the same account.
-   A pay-as-you-go instance can be migrated to a subscription dedicated host. A subscription instance can be migrated only between subscription dedicated hosts. The expiration date of the subscription instance cannot be later than the destination dedicated host.
-   You can migrate only pay-as-you-go instances from a shared host to a dedicated host. You cannot migrate subscription or preemptible instances from a shared host to a dedicated host.
-   You can redeploy an ECS instance in a specific dedicated host cluster.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceDeployment&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyInstanceDeployment|The operation that you want to perform. Set the value to ModifyInstanceDeployment. |
|InstanceId|String|Yes|i-bp67acfmxazb4ph\*\*\*|The ID of the instance. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|DeploymentSetId|String|No|ds-bp67acfmxazb4ph\*\*\*\*|The ID of the deployment set.

This parameter is required when you add an ECS instance to a deployment set or change the deployment set of an instance.

**Note:** You cannot change the deployment set when you modify the dedicated host-related parameters, including `Tenancy`, `Affinity`, and `DedicatedHostId`. |
|Force|Boolean|No|false|Specifies whether to forcibly change the host of the instance. Valid values:

-   true: forcibly changes the host of the instance. You can restart instances that are in the **Running \(Running\)** or **Stopped \(Stopped\)** state. The instances in the Stopped state do not include pay-as-you-go instances that have the No Fees for Stopped Instances \(VPC-Connected\) feature enabled.

**Note:** If the ECS instance that you specified is attached with local disks, the local disks are forcibly changed, which may cause data loss in the local disks when the host of the instance is changed. Proceed with caution.

-   false: does not forcibly change the host of the instance. You can add the instance to a deployment set only when the instance resides on the current host. When the Force parameter is set to this value, the deployment set may fail to be replaced.

Default value: false. |
|DedicatedHostId|String|No|dh-bp67acfmxazb4ph\*\*\*\*|The ID of the dedicated host. You can call the [DescribeDedicatedHosts](~~134242~~) operation to query available dedicated hosts.

When you migrate the instance from a shared host to a dedicated host or migrate the instance from a dedicated host to another one:

-   To migrate the instance to a specific dedicated host, you must specify this parameter.
-   To migrate the instance to a system-selected dedicated host, you must leave this parameter empty and set `Tenancy` to host.

For more information about the automatic deployment feature, see [Features of dedicated hosts](~~118938~~). |
|Tenancy|String|No|host|Specifies whether to deploy the instance on a dedicated host. Set the value to host to deploy the instance on a dedicated host. |
|Affinity|String|No|host|Specifies whether to associate the instance with a dedicated host. Valid values:

-   host: associates with a dedicated host. When an instance that has the No Fees for Stopped Instances \(VPC-Connected\) feature enabled is restarted, the instance still resides on the original dedicated host.
-   default: does not associates with a dedicated host. When an instance that has the No Fees for Stopped Instances \(VPC-Connected\) feature enabled is restarted, the instance can be automatically deployed to another dedicated host in the automatic deployment resource pool if resources of the original dedicated host are insufficient.

If you want to migrate the instance from a shared host to a dedicated host, use the default value. Default value: default. |
|MigrationType|String|No|live|Specifies whether to stop the instance before it is migrated to the destination dedicated host. Valid values:

-   reboot: stops the instance before it is migrated.
-   live: migrates the instance without stopping it. If the MigrationType parameter is set to this value, you must specify the DedicatedHostId parameter. In this case, you cannot change the instance type of the instance when the instance is migrated.

Default value: reboot. |
|InstanceType|String|No|ecs.c6.large|The instance type to which the instance is changed. You can call the [DescribeInstanceTypes](~~25620~~) operation to query the most recent list of instance types.

You can change the instance type of an instance when you migrate the instance to a dedicated host. The new instance type must match the type of the specified dedicated host. For more information, see [Dedicated host types](~~68564~~).

-   If you specify this parameter, you must also specify the `DedicatedHostId` parameter.
-   You cannot change the instance type of an instance if you use the automatic deployment feature to migrate the instance. |
|DedicatedHostClusterId|String|No|dc-bp67acfmxazb4ph\*\*\*\*|The ID of the dedicated host cluster. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|04F0F334-1335-436C-A1D7-6C044FE73368|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceDeployment
&InstanceId=i-bp67acfmxazb4ph****
&RegionId=cn-hangzhou
&DedicatedHostId=dh-bp67acfmxazb4ph****
&Tenancy=host
&MigrationType=live
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyInstanceDeploymentResponse>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceDeploymentResponse>
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
|404|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|The error message returned because the specified DedicatedHostId parameter does not exist.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist.|
|400|OperationDenied.UnstoppedInstance|Operation denied due to unstopped instance.|The error message returned because the current operation is invalid. Check whether the instance is in the Stopped state.|
|400|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status.|The error message returned because the operation is not supported while the dedicated host is in the current state.|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|The error message returned because the expiration date of the instance is later than that of the dedicated host.|
|404|InvalidInstanceNetworkType.NotSupport|The specified Instance network type not support.|The error message returned because the network type of the current instance does not support this operation.|
|404|InvalidInstanceType.NotSupport|The Dedicated host not support the specified instance type.|The error message returned because the current dedicated host does not support the specified instance type.|
|403|IncorrectInstanceStatus|%s|The error message returned because the operation is not supported while the instance is in the current state.|
|400|InvalidParam.Tenancy|The specified Tenancy is invalid.|The error message returned because the specified Tenancy parameter is invalid.|
|403|OperationDenied.NoStock|The resource is out of usage.|The error message returned because the instance is not in the Running state. Start the instance or check whether the operation is valid.|
|400|ChargeTypeViolation.PostPaidDedicatedHost|Prepaid instance onto postpaid dedicated host is not allowed.|The error message returned because subscription instances cannot be deployed on pay-as-you-go dedicated hosts.|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned because the specified InstanceType parameter does not exist or because you are not authorized to manage instances of the specified instance type.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

