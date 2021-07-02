# Control access to resources by using tags

After you attach tags to your resources, you can use tags to group, categorize, and control access to resources. This topic uses an ECS instance as an example to describe how to attach a policy to a RAM user and allow the user to control access to ECS instances by using tags.

You have created a RAM user by using an Alibaba Cloud account. For more information, see [Create a RAM user](/intl.en-US/RAM User Management/Basic operations/Create a RAM user.md).

Tags are used to identify cloud resources. They help you classify, search for, and aggregate cloud resources with the same characteristics from different dimensions. This simplifies resource management. You can attach multiple tags to each cloud resource.

Alibaba Cloud implements policy-based access control. You can configure RAM policies based on roles of RAM users. You can define multiple tags in each policy and attach one or more policies to RAM users or RAM user groups.

You can attach tags to ECS resources and resources of other Alibaba Cloud services. By default, all resources within the current region are displayed in the resource list. If you want to control which resources are accessible to RAM users, you can create a custom policy and use tags to implement access control.

## Step 1: Use an Alibaba Cloud account to create a policy and attach it to a RAM user

In this step, create a custom policy named UseTagAccessRes and attach the policy to the RAM user userTest. The UseTagAccessRes policy states that RAM users must specify the `owner: zhangsan` and `environment: production` tags before they can access ECS resources.

1.  Log on to the [RAM console](https://ram.console.aliyun.com/) by using an Alibaba Cloud account.

2.  For more information about how to create the UseTagAccessRes custom policy, see [Create a custom policy](/intl.en-US/Policy Management/Custom policies/Create a custom policy.md).

    The following code shows how to configure multiple tags for resources in a policy:

    ```
    {
        "Statement": [
            {
                "Effect": "Allow",
                "Action": "ecs:*",
                "Resource": "*",
                "Condition": {
                    "StringEquals": {
                        "ecs:tag/owner": "zhangsan",
                        "ecs:tag/environment": "production"
                    }
                }
            },
            {
                "Action": [
                    "ecs:DescribeTagKeys",
                    "ecs:DescribeTags"
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

    |Policy|Policy content|Description|
    |------|--------------|-----------|
    |Grants the permission to access resources that are attached with specific tags|    -   `"ecs:tag/owner": "zhangsan"`
    -   `"ecs:tag/environment": "production"`
|This policy allows you to control access to resources that are attached with the specified tags.|
    |Grants the permission to query tags|    -   `ecs:DescribeTagKeys`
    -   `ecs:DescribeTags`
|This policy grants the permission to query tags.|
    |Does not grant permissions to call tag-related API operations|    -   `ecs:DeleteTags`
    -   `ecs:UntagResources`
    -   `ecs:CreateTags`
    -   `ecs:TagResources`
|This policy must exclude all tag-related API operations from its permissions. This ensures that users will not be deprived of permissions due to tag modifications.|

3.  Attach the custom policy to RAM users or user groups whose access you want to control. For more information, see [Grant permissions to a RAM role](/intl.en-US/RAM Role Management/Grant permissions to a RAM role.md). In this step, attach the UseTagAccessRes policy to the RAM user userTest.

    **Note:** To attach the UseTagAccessRes policy to an existing RAM user, note that multiple policies attached to a single RAM user may cause problems.


## Step 2: Use an Alibaba Cloud account to attach tags to existing resources

You can attach tags to existing resources to control access to the resources. In this step, use an Alibaba Cloud account to create an ECS instance and attach tags to the instance.

**Note:** If you have no existing ECS instances, create an instance first. For more information, see [Creation method overview](/intl.en-US/Instance/Create an instance/Creation method overview.md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, click **Tags**.

3.  Click **Create/Bind Tags** to create the `owner: zhangsan` and `environment: production` tags and attach the tags to an existing instance. For more information about how to attach a tag to a resource, see [Create or bind a tag](/intl.en-US/Tag & Resource/Tags/Manage tags/Create or bind a tag.md).


## Step 3: Use credentials of a RAM user to access instances that are attached with tags

Log on to the ECS console and access instances with tags by using credentials of the RAM user userTest who is attached with the UseTagAccessRes policy.

**Note:** The ECS resources that can be attached tags include instances, Block Storage devices, snapshots, images, security groups, ENIs, dedicated hosts, SSH key pairs, and instance launch templates. This step uses an ECS instance as an example.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  Select the specified region. No instance is displayed on the Instances page.

    ![Instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6827948951/p75181.png)

4.  You can specify tags to view resources.

    ![Filter 1:](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6827948951/p75185.png)


