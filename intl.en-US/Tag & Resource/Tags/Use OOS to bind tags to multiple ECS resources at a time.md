# Use OOS to bind tags to multiple ECS resources at a time

You can use Operation Orchestration Service \(OOS\) to bind tags to multiple ECS resources within the same region to control permissions on these ECS resources based on tags.

You can bind tags for the resources of ECS and other Alibaba Cloud services by using OOS custom templates. For more information about the services that support tags, see [Services that support tags](/intl.en-US/Tag & Resource/Tags/Overview.md). In this topic, a custom template is created in OOS to bind the `owner:zhangsan` tag to ECS instances within the same region.

**Note:** The resources must be located within the same region for a tag to bind.

## Step 1: Create a custom policy and a RAM role

Create a RAM role named OOSServiceRole for OOS and attach permissions to the role.

1.  Log on to the [RAM console](https://ram.console.aliyun.com/) by using an Alibaba Cloud account.

2.  Create a custom policy named OOSAutoBindTag. For more information, see [Create a custom policy](/intl.en-US/Policy Management/Custom policies/Create a custom policy.md).

    The following policy is created.

    **Note:** This policy targets ECS instances, and the permissions in the policy are set to `ecs:DescribeInstances`. You can set the permissions based on your business needs. For example, if you want to add a tag to multiple security groups, you can replace `ecs:DescribeInstances` with `ecs:DescribeSecurityGroups`.

    ```
    {
        "Version": "1",
        "Statement": [
            {
                "Action": [
                    "ecs:DescribeInstances",
                    "ecs:TagResources"
                ],
                "Resource": "*",
                "Effect": "Allow"
            }
        ]
    }
    ```

3.  Create the OOSServiceRole RAM role.

    For more information, see [Create a RAM role for a trusted Alibaba Cloud service](/intl.en-US/RAM Role Management/Create a RAM role/Create a RAM role for a trusted Alibaba Cloud service.md).

4.  Attach the custom policy to the RAM role.

    For more information, see [Grant permissions to a RAM role](/intl.en-US/RAM Role Management/Grant permissions to a RAM role.md). In this step, the OOSAutoBindTag custom policy is attached to the OOSServiceRole RAM role.

5.  Attach the AliyunOSSFullAccess system policy to the OOSServiceRole RAM role.


## Step 2: Bind tags to resources at a time

1.  Log on to the [OOS console](https://oos.console.aliyun.com/).

2.  In the top navigation bar, select a region.

3.  In the left-side navigation pane, click **My Templates**.

4.  Create a custom template.

    1.  On the My Templates page, click **Create Template**.

    2.  In the Create Template dialog box, click the **Empty Template** tab, select Empty Templates, and then click **OK**.

    3.  On the Create Template page, click the **YAML** tab to edit the template. In the upper-right corner of the page, enter OOSAutoBindTag in the Template Name field. After you edit the template, click **Create Template**.

        The following code provides an example:

        ```
        FormatVersion: OOS-2019-06-01
        Description: Tag Resources Without The Specified Tags
        Parameters:
          tags:
            Type: Json
            Description:
              en: The tags to select ECS instances.
              zh-cn:
            AssociationProperty: Tags
          regionId:
            Type: String
            Description:
              en: The region to select ECS instances.
              zh-cn:
          OOSAssumeRole:
            Description:
              en: The RAM role to be assumed by OOS.
              zh-cn:
            Type: String
            Default: OOSServiceRole
        RamRole: OOSServiceRole
        Tasks:
          - Name: getInstancesByTags
            Action: 'ACS::ExecuteAPI'
            Description: ''
            Properties:
              Service: ECS
              API: DescribeInstances
              Parameters:
                Tags: '{{ tags }}'
                RegionId: '{{ regionId }}'
            Outputs:
              InstanceIds:
                Type: List
                ValueSelector: 'Instances.Instance[].InstanceId'
          - Name: getAllInstances
            Action: 'ACS::ExecuteAPI'
            Description: ''
            Properties:
              Service: ECS
              API: DescribeInstances
              Parameters:
                RegionId: '{{regionId}}'
            Outputs:
              InstanceIds:
                Type: List
                ValueSelector: 'Instances.Instance[].InstanceId'
          - Name: TagResources_ECS_Instances
            Action: 'ACS::ExecuteAPI'
            Description:
              zh-cn:
              en: 'tag ecs instances, which are without the specified tags.'
            Properties:
              Service: ECS
              API: TagResources
              Parameters:
                Tags: '{{ tags }}'
                RegionId: '{{regionId}}'
                ResourceType: Instance
                ResourceIds:
                  - '{{ACS::TaskLoopItem}}'
            Loop:
              MaxErrors: 100%
              Concurrency: 20
              Items:
                'Fn::Difference':
                  - '{{ getAllInstances.InstanceIds }}'
                  - '{{ getInstancesByTags.InstanceIds }}'
        Outputs:
          InstanceIds:
            Type: List
            Value:
              'Fn::Difference':
                - '{{ getAllInstances.InstanceIds }}'
                - '{{ getInstancesByTags.InstanceIds }}'
        ```

        The following section describes the parameters:

        -   tags: the tags bound to ECS instances.
        -   regionId: the region ID of the ECS instances to which the selected tags are bound.
        -   OOSAssumeRole: the RAM role used by OOS.
        The following section describes the permissions:

        -   DescribeInstances: filters resources based on source tags.
        -   TagResources: creates tags for or binds tags to specified resources.
5.  Execute the custom template.

    1.  In the left-side navigation pane, click **My Templates**. On the My Templates page, find the OOSAutoBindTag custom template that you created in Step 5, and click **Create Execution** in the **Actions** column.

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4827948951/p77200.png)

    2.  Keep the default settings or re-select the execution mode, and click **Next: Parameter Settings**.

    3.  In the Parameter Settings step, configure parameters and click **Next: OK**.

        In this example, the following parameters are configured:

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4827948951/p77463.png)

        -   tags: Select the `owner:zhangsan` tag.
        -   regionId: Select the region of the instances, such as `cn-shanghai`. For more information, see [Regions and zones]().
        -   oosAssumeRole: Use the RAM role OOSServiceRole.
    4.  In the OK step, click **Create Execution**.

    5.  On the execution details page, click the **Advanced View** tab.

    6.  Click the **Execution Result** tab on the right of the page.

    View the execution result, which demonstrates that the `owner:zhangsan` tag is bound to all the ECS instances within the selected region.

    ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4827948951/p77203.png)

    If Failed is displayed for Execution Status, you can view the information about the execution status and execution logs to make corresponding adjustments.


