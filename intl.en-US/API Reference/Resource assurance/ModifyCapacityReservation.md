# ModifyCapacityReservation

You can call this operation to modify some information of a capacity reservation, such as its name, description, release mode, and total number of reserved instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyCapacityReservation&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|ModifyCapacityReservation|The operation that you want to perform. Set the value to ModifyCapacityReservation. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the capacity reservation. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|PrivatePoolOptions.Id|String|Yes|crp-bp67acfmxazb4\*\*\*\*|The ID of the capacity reservation. |
|PrivatePoolOptions.Name|String|No|eapTestName|The name of the capacity reservation. The name must be 2 to 128 characters in length. It must start with a letter but cannot start with http:// or https://. The name can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). |
|Description|String|No|This is description.|The description of the capacity reservation. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`. |
|StartTime|String|No|Now|The effective mode of the capacity reservation. The capacity reservation can be set only to take effect immediately. You do not need to pass in a value for the parameter.

**Note:** The capacity reservation takes effect immediately when this parameter is left empty. |
|EndTimeType|String|No|Unlimited|The release mode of the capacity reservation. Valid values:

-   Limited: The capacity reservation is released at the specified time. You must also specify the `EndTime` parameter.
-   Unlimited: You must manually release the capacity reservation. You can release capacity reservations at any time. |
|EndTime|String|No|2021-10-30T06:32:00Z|The expiration time of the capacity reservation. This parameter takes effect only when `EndTimeType` is set to Limited. Specify the time in the ISO 8601 standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC. For more information, see [ISO 8601](~~25696~~). |
|Platform|String|No|Linux|The operating system type of the instance reserved. Valid values:

-   Windows: Windows Server operating systems
-   Linux: Linux and Unix-like operating systems

**Note:** This parameter is unavailable. |
|InstanceAmount|Integer|No|100|The total number of instances reserved by the capacity reservation. Valid values: the number of created instances to 1000.

**Note:** When you increase the number of instances reserved, the increase may fail due to insufficient resources. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|8455DD10-84F8-43C9-8365-5F448EB169B6|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyCapacityReservation
&PrivatePoolOptions.Id=crp-bp67acfmxazb4****
&RegionId=cn-hangzhou
&PrivatePoolOptions.Name=eapTestName
&Description=This is description.
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyCapacityReservationResponse>
      <RequestId>8455DD10-84F8-43C9-8365-5F448EB169B6</RequestId>
</ModifyCapacityReservationResponse>
```

`JSON` format

```
{
    "RequestId": "8455DD10-84F8-43C9-8365-5F448EB169B6"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|401|InvalidUser.Unauthorized|The user is not authorized|The error message returned because you are not authorized to perform this operation.|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone; try other types of resources or other regions and zones.|The error message returned because resources are insufficient in the specified zone. Try other types of resources, or select other regions and zones.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

