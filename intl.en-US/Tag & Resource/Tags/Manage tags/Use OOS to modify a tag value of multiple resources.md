---
keyword: [OOS, Operation Orchestration Service, modify tag value, OOS template]
---

# Use OOS to modify a tag value of multiple resources

This topic describes how to modify a tag value of multiple resources at a time by using an Operation Orchestration Service \(OOS\) custom template.

A tag is bound to resources. For more information, see [Create or bind a tag](/intl.en-US/Tag & Resource/Tags/Manage tags/Create or bind a tag.md).

In this topic, a custom template is created in OOS. This template can be used to modify a tag value of hundreds of ECS instances at a time. In this example, a tag value of the ECS instances is changed from OldTagValue to NewTagValue. The corresponding tag key-value pair is changed from `TagKey:OldTagValue` to `TagKey:NewTagValue`.

**Note:**

-   You can use the OOS custom template to modify a tag value for up to 1,000 resources at a time. If the number of resources is greater than 1,000, you must execute the template multiple times.
-   You can use the OOS custom template to modify the tag values of any resources that support tagging in the same region. You can modify the API operations in the template to make it applicable to various resources. For more information about resources that support tagging, see [Overview](/intl.en-US/Tag & Resource/Tags/Overview.md).For information about the resources that OOS supports, see [List of supported cloud services](https://www.alibabacloud.com/help/doc-detail/120682.htm).

## Step 1: Create a template

You can perform the following steps to create an OOS custom template to modify a tag value of multiple resources.

1.  Log on to the [OOS console](https://oos.console.aliyun.com/).

2.  In the top navigation bar, select a region.

3.  In the left-side navigation pane, click **My Templates**.

4.  Click **Create Template**.

5.  In the Create Template dialog box, click the **Empty Templates** tab, select **Empty Templates**, and then click **OK**.

6.  In the **Basic Information** section on the right of the Create Template page, enter a template name in the Template Name field and add tags.

7.  Click the **JSON** tab and write code in the code editor. The following code provides an example:

    ```
    {
        "Description": "Modify a tag value for multiple resources",
        "FormatVersion": "OOS-2019-06-01",
        "Parameters": {
            "operateId": {
                "Description": "Define the operation ID",
                "Type": "String",
                "MinLength": 1,
                "MaxLength": 64
            },
            "tagKey": {
                "Description": "Current tag key",
                "Type": "String",
                "MinLength": 1,
                "MaxLength": 64
            },
            "tagValue": {
                "Description": "Current tag value",
                "Type": "String",
                "MinLength": 1,
                "MaxLength": 64
            },
            "newTagValue": {
                "Description": "New tag value",
                "Type": "String",
                "MinLength": 1,
                "MaxLength": 64
            }
        },
        "Tasks": [
            {
                "Name": "DescribeInstances_ECS",
                "Action": "ACS::ExecuteAPI",
                "Description": {
                    "zh-cn": "Filter ECS instances by tag",
                    "en": "filter ecs instances by tags"
                },
                "Properties": {
                    "Service": "ECS",
                    "API": "DescribeInstances",
                    "AutoPaging": true,
                    "Parameters": {
                        "Tags": [
                            {
                                "Key": "{{ tagKey }}",
                                "Value": "{{ tagValue }}"
                            }
                        ]
                    }
                },
                "Outputs": {
                    "Instances": {
                        "Type": "List",
                        "ValueSelector": "Instances.Instance[].InstanceId"
                    }
                }
            },
            {
                "Name": "TagResources_ECS_Instances",
                "Action": "ACS::ExecuteAPI",
                "Description": {
                    "zh-cn": "Update the tag of ECS instances",
                    "en": "tag ecs instances"
                },
                "Properties": {
                    "Service": "ECS",
                    "API": "TagResources",
                    "Parameters": {
                        "Tags": [
                            {
                                "Key": "{{ tagKey }}",
                                "Value": "{{ newTagValue }}"
                            }
                        ],
                        "ResourceType": "Instance",
                        "ResourceIds": [
                            "{{ACS::TaskLoopItem}}"
                        ]
                    }
                },
                "Loop": {
                    "MaxErrors": "100%",
                    "Concurrency": 20,
                    "Items": "{{DescribeInstances_ECS.Instances}}"
                }
            }
        ],
        "Outputs": {}
    }
    ```

8.  Click **Create Template**.


## Step 2: Execute the template

You can perform the following steps to execute the template created in Step 1 to modify a tag value of multiple resources.

1.  In the left-side navigation pane, click **My Templates**.

2.  Find the template created in Step 1 and click **Create Execution** in the **Actions** column.

3.  On the Create page, enter an execution description and select an execution mode in the Basic Information step. Then, click **Next: Parameter Settings**.

4.  In the Parameter Settings step, configure parameters and click **Next: OK**.

    The following section describes the parameters.

    -   operateId: the operation ID, which is used to identify each operation. You can customize an operation ID.
    -   tagKey: the key of the tag whose value you want to modify, which is `TagKey` in this example.
    -   tagValue: the tag value to be modified, which is `OldTagValue` in this example.
    -   newTagValue: the new tag value, which is `NewTagValue` in this example.
5.  Click **Create**. The execution details page appears. You can view the execution results.

    **Note:** If the execution fails, you can check the logs for the cause of the failure and make adjustments accordingly.


