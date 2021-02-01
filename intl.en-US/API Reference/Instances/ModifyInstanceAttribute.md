# ModifyInstanceAttribute

You can call this operation to modify the information about an ECS instance, such as the password, name, description, hostname, security groups, and user data. If the instance is a burstable instance, you can also change its performance mode.

## Description

If the response contains `{"OperationLocks": {"LockReason" : "security"}}` when you query information about an instance, the instance is locked for security reasons and all operations are prohibited on the instance.

When you call this operation, take note of the following items:

-   Modify the hostname \(`HostName`\): You must restart the instance by using the ECS console or by calling the RebootInstance operation for the new hostname to take effect. For more information, see [Restart an instance](~~25440~~) and [RebootInstance](~~25502~~). The modification does not take effect if you restart the instance within the operating system.
-   Reset the password \(`Password`\):
    -   The instance cannot be in the **Starting** \(`Starting`\) state.
    -   You must restart the instance by using the ECS console or by calling the RebootInstance operation for the new password to take effect. For more information, see [Restart an instance](~~25440~~) and [RebootInstance](~~25502~~). The modification does not take effect if you restart the instance within the operating system.
-   Modify user data \(`UserData`\):
    -   The ECS instance must be in the **Stopped** \(`Stopped`\) state.
    -   The instance must meet the limits of user data. For more information, see [Prepare user data](~~49121~~).
-   Change the security groups \(`SecurityGroupIds.N`\):
    -   You can switch an ECS instance to a security group of a different type.

        If you want to switch an ECS instance to a security group of a different type, you must understand the differences between the rule configurations of the two security group types to avoid impacts on the instance network.

    -   The security groups of classic network-type instances cannot be changed.

        For more information, see the description of the `SecurityGroupIds.N` parameter.

-   Modify the queue number of the primary elastic network interface \(ENI\) \(`NetworkInterfaceQueueNumber`\):
    -   The instance must be in the Stopped \(`Stopped`\) state.
    -   The new queue number cannot exceed the maximum queue number of one ENI allowed for the instance type.
    -   The total number of queues for all ENIs bound to the instance cannot exceed the queue quota allowed for the instance type. To obtain the maximum queue number of one ENI and queue quota allowed for an instance type, you can call the [DescribeInstanceTypes](~~25620~~) operation to query the `MaximumQueueNumberPerEni` and `TotalEniQueueQuantity` fields.
    -   If you set this parameter to -1, the value is reset to the default queue number of the primary ENI allowed for the instance type. To obtain the default queue number of the primary ENI allowed for an instance type, you can call the [DescribeInstanceTypes](~~25620~~) operation to query the `PrimaryEniQueueNumber` field.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceAttribute&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyInstanceAttribute|The operation that you want to perform. Set the value to ModifyInstanceAttribute. |
|InstanceId|String|Yes|i-bp67acfmxazb4ph\*\*\*\*|The ID of the instance. |
|Password|String|No|Test123456|The password of the instance. The password must be 8 to 30 characters in length and contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include

```

( ) ` ~ ! @ # $ % ^ & * - _ + = | { } [ ] : ; ' < > , . ? /
                                
```

For a Windows instance, the password cannot start with a forward slash \(/\).

**Note:** If the `Password` parameter is specified, we recommend that you send requests over HTTPS to secure your password. |
|HostName|String|No|testHostName|The hostname of the instance. After the hostname is modified, call the RebootInstance operation for the new hostname to take effect.

-   For Windows Server, the hostname must be 2 to 15 characters in length and can contain letters, digits, and hyphens \(-\). It cannot start or end with a hyphen \(-\), contain consecutive hyphens \(-\), or contain only digits.
-   For other operating systems such as Linux, the hostname must be 2 to 64 characters in length. You can use periods \(.\) to separate a hostname into multiple segments. Each segment can contain letters, digits, and hyphens \(-\). The hostname cannot contain consecutive periods \(.\) or hyphens \(-\). It cannot start or end with a period \(.\) or a hyphen \(-\). |
|InstanceName|String|No|testInstanceName|The name of the instance. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, numbers, colons \(:\), underscores \(\_\), and hyphens \(-\). |
|Description|String|No|testInstanceDescription|The description of the instance. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

This parameter is empty by default. |
|UserData|String|No|ZWNobyBoZWxsbyBlY3Mh|The user data of the instance. User data is encoded in Base64.

The size of the user data must be no greater than 16 KB before it is encoded in Base64. User data is imported in plaintext. We recommend that you do not include confidential information such as passwords and private keys in the user data. If confidential information is required, we recommend that you encrypt the confidential information and encode it in Base64 before you import the confidential information. You can then decrypt the information within your ECS instance in the same mode after the information is passed. |
|CreditSpecification|String|No|Standard|The performance mode of the burstable instance. Valid values:

-   Standard: the standard mode. For more information, see the "Standard mode" section of the [Burstable instances](~~59977~~) topic.
-   Unlimited: the unlimited mode. For more information, see the "Unlimited mode" section of the [Burstable instances](~~59977~~) topic.

This parameter is empty by default. |
|DeletionProtection|Boolean|No|false|The release protection property of the instance. It specifies whether you can use the ECS console or call the [DeleteInstance](~~25507~~) operation to manually release the instance.

This parameter is empty by default.

**Note:** This parameter takes effect only on pay-as-you-go instances. It can protect instances only against manual releases, not against automatic releases. |
|SecurityGroupIds.N|RepeatList|No|sg-bp15ed6xe1yxeycg7o\*\*\*\*|The ID of replacement security group N.

-   All security group IDs must be unique.
-   The instance is moved from the current security groups to the replacement security groups. If you want the instance to remain in the current security groups, you must add the IDs of the current security groups to the list.
-   You can move the instance to security groups of a different type. However, the list cannot contain the IDs of both basic and advanced security groups.
-   The specified security group and instance must belong to the same VPC.
-   The valid values of N are based on the maximum number of security groups to which an instance can belong. For more information, see the "Security group limits" section of the [Limits](~~25412#SecurityGroupQuota1~~) topic.
-   New security groups become valid for corresponding instances after a short latency. |
|NetworkInterfaceQueueNumber|Integer|No|8|The number of queues supported by the primary ENI. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceAttribute
&InstanceId=i-bp67acfmxazb4ph****
&Action=ModifyInstanceAttribute
&CreditSpecification=Standard
&DeletionProtection=false
&Description=testInstanceDescription
&HostName=testHostName
&InstanceName=testInstanceName
&Password=Test123456
&SecurityGroupIds.1=sg-bp15ed6xe1yxeycg7o****
&SecurityGroupIds.2=sg-bp15ed6xe1yxeycg7p****
&SecurityGroupIds.3=sg-bp15ed6xe1yxeycg7q****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyInstanceAttributeResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyInstanceAttributeResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidInstanceName.Malformed|The specified parameter "InstanceName" is not valid.|The error message returned because the specified InstanceName parameter is invalid. The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.|
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|The error message returned because the specified Description parameter is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|400|InvalidHostPassword.Malformed|The specified parameter "Password" is not valid.|The error message returned because the specified Password parameter is invalid.|
|400|InvalidHostName.Malformed|The specified parameter "HostName" is not valid.|The error message returned because the specified HostName parameter is invalid.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|The error message returned because the operation is not supported while the instance is locked for security reasons.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist. Check whether the instance ID is correct.|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|The error message returned because the specified security group does not exist in this account. Check whether the security group ID is correct.|
|403|OperationDenied|The instance amount in the specified SecurityGroup reach its limit.|The error message returned because the maximum number of instances that can be added to the specified security group has been reached.|
|403|OperationDenied|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|400|InvalidPassword.Malformed|The specified parameter "Password" is not valid.|The error message returned because the specified Password parameter is invalid.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|InvalidUserData.Forbidden|User not authorized to input the parameter "UserData"please apply for permission "UserData"|The error message returned because you are not authorized to configure the UserData parameter. Apply for the permissions first.|
|400|InvalidUserData.SizeExceeded|The specified parameter "UserData" exceeds the size.|The error message returned because the maximum size of user data specified by the UserData parameter has been reached.|
|400|InvalidUserData.NotSupported|The specified parameter "UserData" only support the vpc and IoOptimized Instance.|The error message returned because the specified UserData parameter is not supported. UserData is supported only on VPC-type instances and I/O optimized instances.|
|400|ImageNotSupportCloudInit|The specified image does not support cloud-init.|The error message returned because the specified image does not support cloud-init.|
|400|ChargeTypeViolation|Pay-As-You-Go instances do not support this operation.|The error message returned because the pay-as-you-go billing method does not support this operation.|
|400|InvalidParameter.RecycleBin|You do not have permission to set recyclable properties.|The error message returned because you are not authorized to perform this operation.|
|400|InvalidParameter.CreditSpecification|The specified CreditSpecification is not supported in this region.|The error message returned because the specified credit policy is not supported in the region.|
|400|InvalidInstanceStatus.CreditSpecRestricted|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|400|InvalidInstanceStatus.NotRunning|The current status of the resource is invalid, you can only do this operation when instance is running.|The error message returned because the operation is not supported while the instance is in the current state. Try again when the instance is in the Running state.|
|404|Credit.NotFound|The specified credit information does not exist.|The error message returned because the specified credit information does not exist.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|InvalidUser.Unauthorized|The user is not authorized|The error message returned because your account is not authorized.|
|403|SecurityGroupInstanceLimitExceed|%s|The error message returned because the maximum number of instances in the specified security group has been reached.|
|403|InstanceNotInSecurityGroup|The instance not in the group.|The error message returned because the specified instance does not belong to the security group.|
|403|InvalidOperation.InvalidRegion|%s|The error message returned because the specified RegionId parameter is invalid.|
|400|InvalidParameter|The specified parameter is not valid.|The error message returned because a specified parameter is invalid.|
|403|OperationDenied|The specified Image is disabled or is deleted.|The error message returned because the specified image has been disabled or deleted.|
|400|InvalidOperation.InvalidEcsState|%s|The error message returned because the operation is not supported while the instance is in the current state.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

