# Use an instance RAM role by calling API operations

You can call API operations to create, authorize, and bind an instance RAM role.

The RAM service is activated. For more information, see [Billing](/intl.en-US/Pricing/Billing.md) in the RAM documentation.

Instance RAM roles have the following limits:

-   Instance RAM roles are applicable only to VPC-type ECS instances.
-   Only one instance RAM role can be bound to an ECS instance at a time.
-   If you have bound an instance RAM role to an ECS instance and want to access the APIs of other Alibaba Cloud services from applications deployed on the instance, you must obtain a temporary authorization token of the instance RAM role by using the instance metadata. For more information, see [Obtain a temporary authorization token](#Token).
-   If you want to use an instance RAM role as a RAM user, you must use the Alibaba Cloud account to authorize the RAM user to use the instance RAM role. For more information, see [Authorize a RAM user to use an instance RAM role](#Authorize).

## Procedure

Perform the following operations to use an instance RAM role by calling API operations:

1.  [Step 1: Create an instance RAM role](#step3)
2.  [Step 2: Authorize the instance RAM role](#section_jhn_g25_xdb)
3.  [Step 3: Bind the instance RAM role](#section_pmw_bf5_xdb)
4.  [\(Optional\) Step 4: Unbind the instance RAM role](#section_k4m_2f5_xdb)
5.  [\(Optional\) Step 5: Obtain a temporary authorization token](#Token)
6.  [\(Optional\) Step 6: Authorize a RAM user to use the instance RAM role](#Authorize)

## Step 1: Create an instance RAM role

Call the [CreateRole](/intl.en-US/API Reference/API Reference (RAM)/Role management APIs/CreateRole.md) operation to create an instance RAM role.

Set theRoleName parameter. For example, set this parameter to EcsRamRoleDocumentTesting.

Set the AssumeRolePolicyDocument parameter based on the following policy:

```
{
     "Statement": [
     {
         "Action": "sts:AssumeRole",
         "Effect": "Allow",
         "Principal": {
         "Service": [
         "ecs.aliyuncs.com"
         ]
         }
     }
     ],
     "Version": "1"
 }
```

## Step 2: Authorize the instance RAM role

1.  Call the [CreatePolicy](/intl.en-US/API Reference/API Reference (RAM)/Policy management APIs/CreatePolicy.md) operation to create an authorization policy.

    Configure the following parameters:

    -   Set the RoleName parameter. For example, set this parameter to EcsRamRoleDocumentTestingPolicy.
    -   Set the PolicyDocument parameter based on the following policy:

        ```
        {
             "Statement": [
                 {
                 "Action": [
                     "oss:Get*",
                     "oss:List*"
                 ],
                 "Effect": "Allow",
                 "Resource": "*"
                 }
             ],
             "Version": "1"
         }
        ```

2.  Call the [AttachPolicyToRole](/intl.en-US/API Reference/API Reference (RAM)/Policy management APIs/AttachPolicyToRole.md) operation to authorize the role policy.

    Configure the following parameters:

    -   Set the PolicyType parameter to Custom.
    -   Set the PolicyName parameter. For example, set this parameter to EcsRamRoleDocumentTestingPolicy.
    -   Set the RoleName parameter. For example, set this parameter to EcsRamRoleDocumentTesting.

## Step 3: Bind the instance RAM role

Call the [AttachInstanceRamRole](/intl.en-US/API Reference/Instances/AttachInstanceRamRole.md) operation to bind the instance RAM role.

Configure the following parameters:

-   Set the RegionId and InstanceIds parameters to specify the ECS instance.
-   Set the RamRoleName parameter. For example, set this parameter to EcsRamRoleDocumentTesting.

## \(Optional\) Step 4: Unbind the instance RAM role

Call the [DettachInstanceRamRole](/intl.en-US/API Reference/Instances/DetachInstanceRamRole.md) operation to unbind the instance RAM role.

Configure the following parameters:

-   Set the RegionId and InstanceIds parameters to specify the ECS instance.
-   Set the RamRoleName parameter. For example, set this parameter to EcsRamRoleDocumentTesting.

## \(Optional\) Step 5: Obtain a temporary authorization token

You can obtain a temporary authorization token for an instance RAM role. With this periodically updated token, you can use the permissions and resources granted to the RAM role. Perform the following operations:

Query the temporary authorization token of the instance RAM role named EcsRamRoleDocumentTesting.

-   Linux instance: Run the `curl http://100.100.100.200/latest/meta-data/Ram/security-credentials/EcsRamRoleDocumentTesting` command.
-   Windows instance: For more information, see [Metadata](/intl.en-US/Instance/Manage instances/Metadata/Overview.md).

Obtain the temporary authorization token. Sample response:

```
{
"AccessKeyId" : "XXXXXXXXX",
"AccessKeySecret" : "XXXXXXXXX",
"Expiration" : "2017-11-01T05:20:01Z",
"SecurityToken" : "XXXXXXXXX",
"LastUpdated" : "2017-10-31T23:20:01Z",
"Code" : "Success"
}
```

## \(Optional\) Step 6: Authorize a RAM user to use the instance RAM role

**Note:** When you authorize a RAM user to use an instance RAM role, you must grant the RAM user the PassRole permission on the instance RAM role. If the RAM user does not have the PassRole permission, the RAM user cannot exercise the permissions specified in role policies.

1.  Log on to the [RAM console](https://ram.console.aliyun.com/#/overview).

2.  Authorize a RAM user to use the instance RAM role. For more information, see [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Grant permissions to a RAM user.md).

    ```
    {
            "Version": "2016-10-17",
            "Statement": [
                {
                "Effect": "Allow",
                "Action": [
                    "ecs: \[ECS RAM Action\]",
                    "ecs: CreateInstance",
                    "ecs: AttachInstanceRamRole",
                    "ecs: DetachInstanceRAMRole"
                ],
                "Resource": "*"
                },
                {
            "Effect": "Allow",
            "Action": "ram:PassRole",
            "Resource": "*"
                }
            ]
    }
    ```

    \[ECS RAM Action\] indicates permissions that can be granted to the RAM user. For more information, see [Authentication rules](/intl.en-US/API Reference/Authentication rules.md).


**References**  


[Bind an instance RAM role](/intl.en-US/Security/Instance RAM roles/Bind an instance RAM role.md)

[Use RAM roles to access other Alibaba Cloud services](/intl.en-US/Best Practices/Use RAM roles to access other Alibaba Cloud services.md)

[CreateRole](/intl.en-US/API Reference/API Reference (RAM)/Role management APIs/CreateRole.md)

[ListRoles](/intl.en-US/API Reference/API Reference (RAM)/Role management APIs/ListRoles.md)

[CreatePolicy](/intl.en-US/API Reference/API Reference (RAM)/Policy management APIs/CreatePolicy.md)

[AttachPolicyToRole](/intl.en-US/API Reference/API Reference (RAM)/Policy management APIs/AttachPolicyToRole.md)

[AttachInstanceRamRole](/intl.en-US/API Reference/Instances/AttachInstanceRamRole.md)

[DetachInstanceRamRole](/intl.en-US/API Reference/Instances/DetachInstanceRamRole.md)

[DescribeInstanceRamRole](/intl.en-US/API Reference/Instances/DescribeInstanceRamRole.md)

