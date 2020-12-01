# 授权RAM用户使用实例RAM角色

如果您需要通过RAM用户授予、更换、收回实例RAM角色，您需要通过云账号授权RAM用户允许使用实例RAM角色。本文操作仅适用于云账号。

当您授权RAM用户使用实例RAM角色时，您必须授权RAM用户对该实例RAM角色的PassRole权限。其中，PassRole决定该RAM用户能否直接执行角色策略赋予的权限。

1.  云账号登录[RAM控制台](https://ram.console.aliyun.com/)。

2.  在左侧导航栏的**人员管理**菜单下，单击**用户**。

3.  在**用户登录名称/显示名称**列表下，找到目标RAM用户。

4.  单击**添加权限**，被授权主体会自动填入。

5.  单击**新建权限策略**，新建自定义权限策略。

    自定义策略如下所示，其中，\[ECS RAM Action\]表示可授权RAM用户的权限，更多取值请参见[鉴权规则](/intl.zh-CN/API参考/鉴权规则.md)。

    ```
    {
        "Version": "1",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "ecs: [ECS RAM Action]",
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

6.  返回**添加权限**面板，在**选择权限**区域单击**自定义策略**。

7.  在左侧**权限策略名称**列表下，单击需要授予RAM用户的自定义权限策略。

    **说明：** 在右侧区域框，选择某条策略并单击**×**，可撤销该策略。

8.  单击**确定**。

9.  单击**完成**。


**相关文档**  


[CreatePolicy](/intl.zh-CN/API参考/API参考（RAM）/权限策略管理接口/CreatePolicy.md)

[AttachPolicyToRole](/intl.zh-CN/API参考/API参考（RAM）/权限策略管理接口/AttachPolicyToRole.md)

