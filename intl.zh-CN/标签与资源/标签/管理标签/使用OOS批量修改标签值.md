---
keyword: [OOS, 运维编排, 修改标签值, OOS模板]
---

# 使用OOS批量修改标签值

通过创建OOS自定义模板，您可以一次修改数百个资源的同一标签的标签值。

已为资源绑定一个标签，详情请参见[创建或绑定标签](/intl.zh-CN/标签与资源/标签/管理标签/创建或绑定标签.md)。

本文以ECS实例为例，创建一个OOS自定义模板，该模板支持一次性修改数百台ECS实例的同一标签值。本示例中，ECS实例的源标签键值对为`TagKey:OldTagValue`，修改后将变为`TagKey:NewTagValue`。

**说明：**

-   批量修改资源的数量上限为1000，资源数量大于1000时需要多次执行自定义模板。
-   OOS自定义模板可以修改同一地域下任何支持绑定标签的资源，您只需要根据您的业务需求修改相应接口，支持绑定标签的资源，详情请参见[标签概述](/intl.zh-CN/标签与资源/标签/标签概述.md)。OOS支持的资源，详情请参见[OOS支持的云产品列表](https://www.alibabacloud.com/help/doc-detail/120682.htm)。

## 步骤一：创建模板

您可以参照以下步骤，创建批量修改标签值的OOS自定义模板。

1.  登录[运维编排服务OOS管理控制台](https://oos.console.aliyun.com/)。

2.  在顶部菜单栏左上角处，选择地域。

3.  在左侧导航栏，单击**我的模板**。

4.  单击**创建模板**。

5.  单击**空白模板**页签，选择**空白模板**，单击**选取。**

6.  在右侧**基本信息**栏中，输入模板名称，按需添加标签。

7.  选择**JSON**页签，在下方代码区域编写模板代码。代码示例如下所示。

    ```
    {
        "Description": "批量修改资源的标签值",
        "FormatVersion": "OOS-2019-06-01",
        "Parameters": {
            "operateId": {
                "Description": "自定义您的操作ID",
                "Type": "String",
                "MinLength": 1,
                "MaxLength": 64
            },
            "tagKey": {
                "Description": "当前标签键",
                "Type": "String",
                "MinLength": 1,
                "MaxLength": 64
            },
            "tagValue": {
                "Description": "当前标签值",
                "Type": "String",
                "MinLength": 1,
                "MaxLength": 64
            },
            "newTagValue": {
                "Description": "修改后的标签值",
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
                    "zh-cn": "通过标签过滤ECS实例",
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
                    "zh-cn": "更新ECS实例标签",
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

8.  单击**创建模板**，完成模板创建。


## 步骤二：执行模板

您可以参照以下步骤，执行步骤一创建的模板来批量修改标签值。

1.  在左侧导航栏，单击**我的模板**。

2.  找到步骤一新建的模板，单击对应**操作**列下的**创建执行**。

3.  填写执行描述，并选择执行模式，单击**下一步：设置参数**。

4.  参见参数说明，输入各项参数，单击**下一步：确定**。

    参数说明如下：

    -   operateId：操作ID，用于区分每次操作，可自定义输入。
    -   tagKey：当前标签键，即想修改标签值的对应标签键，本示例为`TagKey`。
    -   tagValue：当前标签值，即修改前的标签值，本示例为`OldTagValue`。
    -   newTagValue：新标签值，即修改后的标签值，本示例为`NewTagValue`。
5.  单击**创建**开始执行。执行完成后将自动跳转到执行详情页面，可查看执行结果。

    **说明：** 若执行失败，您可以查看日志获取失败原因，以调整执行内容。


