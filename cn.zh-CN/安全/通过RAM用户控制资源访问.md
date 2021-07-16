---
keyword: [访问控制, 权限, 虚商, 跨产品, 鉴权, ecs]
---

# 通过RAM用户控制资源访问

本文介绍如何创建RAM用户并授予特定权限策略，从而控制对云服务器ECS资源的访问。

## 前提条件

您已使用阿里云账号登录[RAM控制台](https://ram.console.aliyun.com/)。

## 操作步骤

本文示例使用阿里云账号在RAM控制台创建一个RAM用户，并授予自定义权限或者系统权限：

-   [步骤一：创建RAM用户](#section_s9s_ayg_45l)
-   [（可选）步骤二：创建自定义权限策略](#section_xb2_v3o_mtj)
-   [步骤三：授权RAM用户](#section_cqu_evj_cgs)

## 步骤一：创建RAM用户

按以下步骤在访问控制RAM控制台创建一个RAM用户：

1.  在左侧导航栏的**人员管理**菜单下，单击**用户**。

2.  单击**创建用户**。

    **说明：** 单击**添加用户**，可一次性创建多个RAM用户。

3.  输入**登录名称**和**显示名称**。

4.  在**访问方式**区域下，选择**控制台密码登录**或**编程访问**。

    -   **控制台密码登录**：完成对登录安全的基本设置，包括自动生成或自定义登录密码、是否要求下次登录时重置密码以及是否要求开启多因素认证。
    -   **编程访问**：自动为RAM用户生成访问密钥（AccessKey），支持通过API或其他开发工具访问阿里云。
    **说明：** 为了保障账号安全，建议仅为RAM用户选择一种登录方式，避免RAM用户离开组织后仍可以通过访问密钥访问阿里云资源。

5.  单击**确认**。


![创建RAM用户](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1834129951/p93747.gif)

## （可选）步骤二：创建自定义权限策略

除了使用阿里云提供的系统权限，您还可以按以下步骤在访问控制RAM控制台创建一个自定义权限策略：

1.  在左侧导航栏的**权限管理**菜单下，单击**权限策略管理**。

2.  单击**新建权限策略**。

3.  填写**策略名称**和**备注**。

4.  **配置模式**选择**可视化配置**或**脚本配置**。

    -   **可视化配置**：单击**添加授权语句**，根据界面提示，对权限效力、操作名称和资源等进行配置。

        ![可视化配置创建自定义策略](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1834129951/p93749.gif)

    -   **脚本配置**：请参考[权限策略语法和结构](/cn.zh-CN/权限策略管理/权限策略语言/权限策略语法和结构.md)编辑策略内容。

        ![脚本方式自定义策略](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2834129951/p93905.gif)

    选择**脚本配置**时，Statement结构下的Action和Resource参数取值请参见[鉴权列表](/cn.zh-CN/API参考/鉴权规则.md)，其他参数取值请参见 *访问控制文档*[权限策略语法和结构](/cn.zh-CN/权限策略管理/权限策略语言/权限策略语法和结构.md)。

    -   脚本配置策略示例一：允许RAM用户创建按量付费实例。

        ```
        {
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                            "ecs:DescribeImages", 
                          "vpc:DescribeVpcs", 
                          "vpc:DescribeVSwitches", 
                          "ecs:DescribeSecurityGroups", 
                          "ecs:DescribeKeyPairs",
                          "ecs:DescribeTags", 
                          "ecs:RunInstances"
                  ],
                    "Resource": "*"
                }
            ],
            "Version": "1"
        }
        ```

    -   脚本配置策略示例二：允许RAM用户创建包年包月实例。其中bss相关API主要用于查看并支付包年包月订单，其对应的系统策略为`AliyunBSSOrderAccess`。

        ```
        {
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                            "ecs:DescribeImages", 
                          "vpc:DescribeVpcs", 
                          "vpc:DescribeVSwitches", 
                          "ecs:DescribeSecurityGroups", 
                          "ecs:DescribeKeyPairs",
                          "ecs:DescribeTags", 
                          "ecs:RunInstances",
                          "bss:DescribeOrderList",
                          "bss:DescribeOrderDetail",
                          "bss:PayOrder",
                          "bss:CancelOrder"
                  ],
                    "Resource": "*"
                }
            ],
            "Version": "1"
        }
        ```

    -   脚本配置策略示例三：允许RAM用户创建了ECS实例后查询实例和块存储信息。

        ```
        {
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                            "ecs:DescribeInstances", 
                            "ecs:DescribeDisks"
                  ],
                    "Resource": "*"
                }
            ],
            "Version": "1"
        }
        ```

5.  单击**确定**。


## 步骤三：授权RAM用户

按以下步骤在访问控制RAM控制台创授权RAM用户相关权限：

1.  在左侧导航栏的**人员管理**菜单下，单击**用户**。

2.  在**用户登录名称/显示名称**列表下，找到目标RAM用户。

3.  单击**添加权限**，被授权主体会自动填入。

4.  在左侧**权限策略名称**列表下，单击需要授予RAM用户的权限策略。

    **说明：** 在右侧区域框，选择某条策略并单击**×**，可撤销该策略。

5.  单击**确定**。

6.  单击**完成**。


![为用户授权](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2834129951/p93753.gif)

完成授权后，权限立即生效，RAM用户可以登录[RAM控制台](https://signin.aliyun.com/login.htm)操作目标云资源。

