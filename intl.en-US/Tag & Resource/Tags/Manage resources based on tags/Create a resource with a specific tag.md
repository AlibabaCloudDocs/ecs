# Create a resource with a specific tag

This topic describes how to attach a custom policy to a RAM user. This allows the RAM user to bind specific tags when the RAM user creates ECS resources. Otherwise, the ECS resources cannot be created. The combination of tags and RAM user allows different RAM users to have different access and operation permissions on cloud resources based on their tags.

A RAM user is created under your Alibaba Cloud account. For more information, see [Create a RAM user](/intl.en-US/RAM User Management/Basic operations/Create a RAM user.md).

You can bind tags to the resources of ECS and other Alibaba Cloud services. For more information about the services that support tags, see [Services that support tags](/intl.en-US/Tag & Resource/Tags/Overview.md). By default, you can select whether to bind tags when you create resources. If you want to bind a specific tag when you create a resource, you can create a custom policy. This allows you to control the operations of your RAM users on resources by binding specific tags to the resources.

## Step 1: Create a RAM policy by using your Alibaba Cloud account and attach the RAM policy to the RAM user

To create a resource bound with a specific tag, you must create and attach a custom policy to the RAM user. In this step, the BindTagForRes custom policy is assigned to the userTest RAM user. When the RAM user creates an ECS resource, the RAM user must bind a specific tag to the resource and select a VPC bound with a tag. In this example, the `user:lisi` tag is bound to the VPC and the `owner:zhangsan` tag must be bound to the ECS resource.

1.  Log on to the [RAM console](https://ram.console.aliyun.com/) by using an Alibaba Cloud account.

2.  Create the BindTagForRes custom policy. For more information, see [Create a custom policy](/intl.en-US/Policy Management/Custom policies/Create a custom policy.md).

    The following policy is used in this step. You can configure permissions based on your business needs.

    ```
    {
        "Statement": [
            {
               "Effect": "Allow",
                "Action": "ecs:*",
                "Resource": "*",
                "Condition": {
                    "StringEquals": {
                        "ecs:tag/owner": "zhangsan"
                    }
                }
            },
            {
                "Effect": "Allow",
                "Action": "ecs:*",
                "Resource": "*",
                "Condition": {
                    "StringEquals": {
                        "vpc:tag/user": "lisi"
                    }
                }
            },
            {
                "Action": [
                    "ecs:DescribeTagKeys",
                    "ecs:ListTagResources",
                    "ecs:DescribeTags",
                    "ecs:DescribeKeyPairs",
                    "ecs:DescribeImages",
                    "ecs:DescribeSecurityGroups",
                    "ecs:DescribeLaunchTemplates",
                    "ecs:DescribeDedicatedHosts",
                    "ecs:DescribeDedicatedHostTypes",
                    "ecs:DescribeAutoSnapshotPolicyEx",
                    "vpc:DescribeVpcs",
                    "vpc:DescribeVSwitches",
                    "bss:PayOrder"
                ],
                "Effect": "Allow",
                "Resource": "*"
            },
            {
                "Effect": "Deny",
                "Action": [
                    "ecs:DeleteTags",
                    "ecs:UntagResources",
                    "ecs:CreateTags",
                    "ecs:TagResources"
                ],
                "Resource": "*"
            }
        ],
        "Version": "1"
    }
    ```

    |Permission policy|Parameter|Description|
    |-----------------|---------|-----------|
    |Permission to create or access a resource bound with a tag|`"ecs:tag/owner": "zhangsan"`|    -   When a resource is created, the resource must be bound with this tag.
    -   You can control access to resources bound with this tag. |
    |API permission to query tags|    -   `ecs:DescribeTagKeys`
    -   `ecs:ListTagResources`
    -   `ecs:DescribeTags`
|You can query tags in the ECS console.|
    |API permission to query ECS resources|    -   `ecs:DescribeKeyPairs`
    -   `ecs:DescribeImages`
    -   `ecs:DescribeSecurityGroups`
    -   `ecs:DescribeLaunchTemplates`
    -   `ecs:DescribeDedicatedHosts`
    -   `ecs:DescribeDedicatedHostTypes`
    -   `ecs:DescribeAutoSnapshotPolicyEx`
|You can filter resources by tag. This permission is required when you create resources in the ECS console. The resources include key pairs, images, security groups, instances, dedicated hosts, and snapshots.|
    |API permission to query VPC resources|    -   `vpc:DescribeVpcs`
    -   `vpc:DescribeVSwitches`
|You can query existing VPCs and VSwitches.|
    |API permission to pay for orders|`bss:PayOrder`|This operation applies only to subscription resources.|
    |API permission to disable tag-related operations|    -   `ecs:DeleteTags`
    -   `ecs:UntagResources`
    -   `ecs:CreateTags`
    -   `ecs:TagResources`
|This permission disables tag-related API operations and avoids loss of control permissions on resources caused by modifications on tags. You can grant this permission when necessary. Exercise caution when you perform this operation.|
    |Policy for VPCs to bind tags|`"vpc:tag/user": "lisi"`|The policy requires that a VPC must be bound with a tag. You can also specify whether to require a VPC to be bound with a tag.|

3.  Attach the custom policy to the RAM user or group to which you want to control access. For more information, see [Grant permissions to a RAM role](/intl.en-US/RAM Role Management/Grant permissions to a RAM role.md). In this step, the BindTagForRes custom policy is attached to the userTest RAM user.

    **Note:** Problems may occur if you attach the BindTagForRes custom policy to an existing RAM user that is attached with multiple permission policies.


## Step 2: Create and configure a VPC by using the Alibaba Cloud account

The custom policy created in Step 1 requires that you select a VPC that is bound with the `user:lisi` tag when you create an ECS resource. Therefore, you must create a VPC and bind the VPC with a tag. If the VPC is not bound with a specific tag, you cannot create the ECS resource.

**Note:** You cannot bind a tag to a VPC when the VPC is being created. You must call the TagResources operation to bind a tag to the VPC after the VPC is created.

1.  Create a VPC by using the Alibaba Cloud account. For more information, see [Create a VPC](/intl.en-US/VPCs and vSwitchs/Work with VPCs.md).

2.  Call the [TagResources](/intl.en-US/API reference/Tags/TagResources.md) operation to bind the `user:lisi` tag to the VPC.

    You can also bind other tags to the VPC.

3.  Call the [ListTagResources](/intl.en-US/API reference/Tags/ListTagResources.md) operation to query the VPC created in this step. If the response contains `"TagKey": "user"` and `"TagValue": "lisi"`, the VPC is bound with the `user:lisi` tag.


## Step 3: Create an ECS resource by using the RAM user

Log on to the ECS console as the userTest RAM user and create an ECS instance bound with a tag.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Click **Create Instance** to create an instance.

    **Note:** You must select the VPC bound with the `user:lisi` tag in Step 2 and bind the `owner:zhangsan` tag to the ECS instance. If you do not bind the owner:zhangsan tag, the ECS instance cannot be created, and the **You are not authorized to create ECS instances** message is displayed.

    ![Bind a specific tag](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2827948951/p75575.png)


## What to do next

You can bind specific tags to existing resources. This allows you to control access to these resources. You can also access resources bound with specific tags. For more information, see [Control access to resources by using tags](/intl.en-US/Tag & Resource/Tags/Control access to resources by using tags.md).

