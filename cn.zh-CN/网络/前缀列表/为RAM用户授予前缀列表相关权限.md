# 为RAM用户授予前缀列表相关权限

通过RAM用户可以让您避免与其他用户共享阿里云账号密钥，按需为用户分配最小权限，从而降低企业的信息安全风险。本文介绍如何为RAM用户授予前缀列表相关权限。

本文仅介绍为RAM用户授予前缀列表相关权限，如果您需要在控制台使用其他资源，还需要为RAM用户设置对应的权限策略，例如**系统策略**中的**AliyunECSReadOnlyAccess**（只读访问云服务器服务（ECS）的权限）等。

## 操作步骤

1.  使用阿里云账号登录[RAM控制台](https://ram.console.aliyun.com/)。

2.  创建前缀列表相关权限策略。具体操作，请参见[创建自定义策略](/cn.zh-CN/权限策略管理/自定义策略/创建自定义策略.md)。

    ![PrefixListPolicy](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1119654161/p244134.png)

    创建一个PrefixListPolicy权限策略，策略内容如下所示。

    ```
    {
        "Statement": [
            {
                "Action": [
                    "ecs:CreatePrefixList",
                    "ecs:ModifyPrefixList",
                    "ecs:DescribePrefixLists",
                    "ecs:DescribePrefixListAssociations",
                    "ecs:DescribePrefixListAttributes",
                    "ecs:DeletePrefixList"
                ],
                "Resource": "*",
                "Effect": "Allow"
            }
        ],
        "Version": "1"
    }
    ```

    **说明：** 此处仅提供前缀列表的相关鉴权规则，更多ECS相关的鉴权规则，请参见[鉴权规则](/cn.zh-CN/API参考/鉴权规则.md)。

3.  为RAM用户设置前缀列表相关权限。具体操作，请参见[为RAM用户授权](/cn.zh-CN/用户管理/授权管理/为RAM用户授权.md)。

    ![授权](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7996854161/p244148.png)

    设置完成后，您可以通过RAM用户管理前缀列表。


