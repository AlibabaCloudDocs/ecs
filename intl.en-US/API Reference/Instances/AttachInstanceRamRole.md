# AttachInstanceRamRole

You can call this operation to bind an instance RAM role to one or more ECS instances. If an instance already has an instance RAM role, an error is returned when you bind another instance RAM role to the instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=AttachInstanceRamRole&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AttachInstanceRamRole|The operation that you want to perform. Set the value to AttachInstanceRamRole. |
|InstanceIds|String|Yes|\["i-bp14ss25xca5ex1u\*\*\*\*", "i-bp154z5o1qjalfse\*\*\*\*", "i-bp10ws62o04ubhvi\*\*\*\*"...\]|The IDs of instances to which you want to bind the instance RAM role. It can be a JSON array that consists of up to 100 instance IDs. Separate multiple instance IDs with commas \(,\). |
|RamRoleName|String|Yes|testRamRoleName|The name of the instance RAM role. You can call the [ListRoles](~~28713~~) operation provided by RAM to query the RAM roles that you have created. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Policy|String|No|\{"Statement": \[\{"Action": \["\*"\],"Effect": "Allow","Resource": \["\*"\]\}\],"Version":"1"\}|The permission policy. The policy must be 1 to 1,024 characters in length. When you bind a RAM role to one or more instances, you can specify an additional policy to further restrict the permissions of the RAM role. For more information, see [Policy overview](~~93732~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AttachInstanceRamRoleResults|Array of AttachInstanceRamRoleResult| |Details about the results of binding the instance RAM role. |
|AttachInstanceRamRoleResult| | | |
|Code|String|200|Indicates whether the instance RAM role was bound. If 200 is returned, the RAM role was bound. If any other value is returned, the RAM role failed to be bound. For more information, see the "Error codes" section of this topic. |
|InstanceId|String|i-bp10ws62o04ubhvi\*\*\*\*|The ID of the instance. |
|Message|String|success|Indicates whether the instance RAM role was bound. If success is returned, the RAM role was bound. If any other value is returned, the RAM role failed to be bound. For more information, see the "Error codes" section of this topic. |
|Success|Boolean|true|Indicates whether the RAM role was bound. |
|FailCount|Integer|0|The number of RAM roles that fail to be bound. |
|RamRoleName|String|testRamRoleName|The name of the instance RAM role. |
|RequestId|String|D9553E4C-6C3A-4D66-AE79-9835AF705639|The ID of the request. |
|TotalCount|Integer|1|The total number of instances to which you attempted to attach the instance RAM role. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=AttachInstanceRamRole
&InstanceIds=["i-bp10ws62o04ubhvi****"]
&RamRoleName=testRamRoleName
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AttachInstanceRamRoleResponse>
      <RequestId>E6352369-5C2B-41CD-AB50-471550C8F674</RequestId>
      <AttachInstanceRamRoleResults>
            <AttachInstanceRamRoleResult>
                   <InstanceId>i-bp10ws62o04ubhvi****</InstanceId>
                   <Code>200</Code>
                   <Message>success</Message>
            </AttachInstanceRamRoleResult>
      </AttachInstanceRamRoleResults>
      <TotalCount>1</TotalCount>
      <FailCount>0</FailCount>
      <RamRoleName>testRamRoleName</RamRoleName>
</AttachInstanceRamRoleResponse>
```

`JSON` format

```
{
    "RequestId": "D9553E4C-6C3A-4D66-AE79-9835AF705639",
    "AttachInstanceRamRoleResults": {
        "AttachInstanceRamRoleResult": [
            {
                "Message": "success",
                "InstanceId": "i-bp10ws62o04ubhvi****",
                "Code": "200"
            }
        ]
    },
    "TotalCount": 1,
    "FailCount": 0,
    "RamRoleName": "testRamRoleName"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidInstanceIds.Malformed|The specified instanceIds are not valid.|The error message returned because the specified InstanceIds parameter is invalid.|
|404|InvalidInstanceId.NotFound|The specified instanceId does not exist|The error message returned because the specified instance does not exist. Check whether the instance ID is correct.|
|403|InvalidNetworkType.MismatchRamRole|Ram role cannot be applied to instances of Classic network type.|The error message returned because an instance RAM role can be used only for instances in VPCs, not for instances in the classic network.|
|403|InvalidUser.PassRoleForbidden|The RAM user does not have the privilege to pass a RAM role.|The error message returned because the RAM user is not authorized to pass the RAM role.|
|404|InvalidRamRole.NotFound|The specified RAMRoleName does not exist.|The error message returned because the specified RamRoleName parameter does not exist.|
|404|InvalidRamRole.NotEcsRole|The specified ram role is not authorized for ecs, please check your role policy.|The error message returned because the specified RAM role is not authorized to use ECS. Check your role policy.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

