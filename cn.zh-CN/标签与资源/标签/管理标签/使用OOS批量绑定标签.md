# 使用OOS批量绑定标签

如果您希望使用特定标签控制资源的权限，可以使用OOS便捷地操作，批量为同一地域下的需要控制权限的资源绑定特定标签。

通过创建运维编排服务OOS的自定义模板，您可以批量为支持标签的资源绑定标签。云服务器ECS和其他云产品的诸多资源支持绑定标签，详情请参见[产品列表](/cn.zh-CN/标签与资源/标签/标签概述.md)。本文以ECS实例为例，创建一个OOS自定义模板，该模板可以为同一地域下的ECS实例批量绑定标签`owner:zhangsan`。

**说明：** 需要批量绑定标签的资源必须在同一地域下。

## 步骤一：创建自定义策略和RAM角色

为运维编排服务OOS创建RAM服务角色OOSServiceRole，并为RAM角色添加权限。

1.  使用主账号登录[RAM控制台](https://ram.console.aliyun.com/)。

2.  创建自定义策略OOSAutoBindTag，详情请参见[创建自定义策略](/cn.zh-CN/权限策略管理/自定义策略/创建自定义策略.md)。

    本步骤使用的策略如下所示。

    **说明：** 自定义策略OOSAutoBindTag以ECS实例为例，权限设置为`ecs:DescribeInstances`，您可以根据业务需求设置您需要的权限。例如，如果您需要为安全组批量绑定标签，将`ecs:DescribeInstances`替换为`ecs:DescribeSecurityGroups`。

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

3.  创建RAM服务角色OOSServiceRole。

    详情请参见[创建可信实体为阿里云服务的RAM角色](/cn.zh-CN/角色管理/创建RAM角色/创建可信实体为阿里云服务的RAM角色.md)。

4.  将自定义策略授权给RAM服务角色。

    详情请参见[为RAM角色授权](/cn.zh-CN/角色管理/为RAM角色授权.md)。本步骤中将自定义策略OOSAutoBindTag授权给RAM服务角色OOSServiceRole。

5.  为RAM服务角色OOSServiceRole授权系统策略AliyunOOSFullAccess。

    添加权限如下所示：

    ![AliyunOOSFullAccess](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8138819951/p137559.png)


## 步骤二：为资源批量绑定标签

1.  登录[运维编排服务OOS管理控制台](https://oos.console.aliyun.com/)。

2.  在顶部菜单栏左上角处，选择地域。

3.  在左侧导航栏，单击**我的模板**。

4.  创建自定义模板。

    1.  单击**创建模板**。

    2.  选择**空白模板**，单击**选取**。

    3.  单击**YAML**，编辑模板，并在右侧填写模板名称OOSAutoBindTag，模板编辑完成后单击**创建模板**。

        本文中模板代码示例如下所示。

        ```
        FormatVersion: OOS-2019-06-01
        Description: Tag Resources Without The Specified Tags
        Parameters:
          tags:
            Type: Json
            Description:
              en: The tags to select ECS instances.
              zh-cn: 选取已绑定ECS实例的标签。
            AssociationProperty: Tags
          regionId:
            Type: String
            Description:
              en: The region to select ECS instances.
              zh-cn: 输入批量绑定标签的ECS实例所在地域。
          OOSAssumeRole:
            Description:
              en: The RAM role to be assumed by OOS.
              zh-cn: OOS使用的RAM角色。
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
              zh-cn: 对没有绑定已选择的标签的ECS实例进行绑定标签
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

        参数说明：

        -   tags：选取已绑定ECS实例的标签。
        -   regionId：输入批量绑定标签的ECS实例所在地域。
        -   OOSAssumeRole：OOS使用的RAM角色。
        权限说明：

        -   DescribeInstances：根据源标签过滤资源。
        -   TagResources：为指定的资源创建或绑定标签。
5.  执行自定义模板。

    1.  在左侧导航栏，单击**我的模板**，找到新建的自定义模板OOSAutoBindTag，在**操作**列，单击**创建执行**。

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7234559951/p77200.png)

    2.  保持默认设置或重新选择执行模式，然后单击**下一步：设置参数**。

    3.  填写参数，并单击**下一步：确定**。

        本示例中填写的参数：

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7234559951/p77463.png)

        -   tags：选择标签`owner:zhangsan`。
        -   regionId：选择实例所在的地域，例如，选择上海`cn-shanghai`。更多详情，请参见[地域和可用区]()。
        -   oosAssumeRole：使用RAM角色OOSServiceRole。
    4.  在确定页面，单击**创建执行**。

    5.  在基本详情页顶部，单击**高级视图**。

    6.  在高级视图页面右侧，单击**执行结果**。

    查看结果信息，已成功为该地域下的所有ECS实例绑定标签`owner:zhangsan`。

    ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7234559951/p77203.png)

    如果执行状态显示失败，您可以查看状态信息和执行日志来调整执行内容。


