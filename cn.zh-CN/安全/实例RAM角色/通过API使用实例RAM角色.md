# 通过API使用实例RAM角色

您可以通过API创建、授权实例RAM角色，并将其授予实例。

请确保您已经开通RAM服务，详情请参见RAM文档[计费方法](/cn.zh-CN/产品定价/计费方法.md)。

使用限制如下：

-   只有专有网络（VPC）网络类型的ECS实例才能使用实例RAM角色。
-   一个ECS实例一次只能授予一个实例RAM角色。
-   当您给ECS实例授予了实例RAM角色后，并希望在ECS实例内部部署的应用程序中访问云产品的API时，您需要通过实例元数据获取实例RAM角色的临时授权Token。详情请参见[获取临时授权Token](#Token)。
-   如果您是通过RAM用户使用实例RAM角色，您需要通过阿里云账号授权RAM用户使用实例RAM角色。具体操作，请参见[授权RAM用户使用实例RAM角色](#Authorize)。

## 操作步骤

通过API使用实例RAM角色的操作步骤如下：

1.  [步骤一：创建实例RAM角色](#step3)
2.  [步骤二：授权实例RAM角色](#section_jhn_g25_xdb)
3.  [步骤三：授予实例RAM角色](#section_pmw_bf5_xdb)
4.  [步骤四：（可选）收回实例RAM角色](#section_k4m_2f5_xdb)
5.  [步骤五：（可选）获取临时授权Token](#Token)
6.  [步骤六：（可选）授权RAM用户使用实例RAM角色](#Authorize)

## 步骤一：创建实例RAM角色

调用[CreateRole](/cn.zh-CN/API参考/API参考（RAM）/角色管理接口/CreateRole.md)接口创建实例RAM角色。

设置RoleName参数，例如将其值置为EcsRamRoleDocumentTesting。

按如下策略设置参数AssumeRolePolicyDocument：

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

## 步骤二：授权实例RAM角色

1.  调用[CreatePolicy](/cn.zh-CN/API参考/API参考（RAM）/权限策略管理接口/CreatePolicy.md)接口新建授权策略。

    设置如下参数：

    -   设置RoleName参数，例如EcsRamRoleDocumentTestingPolicy。
    -   按如下策略设置参数PolicyDocument：

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

2.  调用[AttachPolicyToRole](/cn.zh-CN/API参考/API参考（RAM）/权限策略管理接口/AttachPolicyToRole.md)接口授权角色策略。

    设置如下参数：

    -   设置PolicyType参数为Custom。
    -   设置PolicyName参数，例如EcsRamRoleDocumentTestingPolicy。
    -   设置RoleName参数，例如EcsRamRoleDocumentTesting。

## 步骤三：授予实例RAM角色

调用[AttachInstanceRamRole](/cn.zh-CN/API参考/实例/AttachInstanceRamRole.md)接口为实例授予RAM角色。

设置如下参数：

-   设置RegionId及InstanceIds参数指定一个ECS实例。
-   设置RamRoleName参数，例如EcsRamRoleDocumentTesting。

## 步骤四：（可选）收回实例RAM角色

调用[DetachInstanceRamRole](/cn.zh-CN/API参考/实例/DetachInstanceRamRole.md)接口收回实例RAM角色。

设置如下参数：

-   设置RegionId及InstanceIds参数指定一个ECS实例。
-   设置RamRoleName参数，例如EcsRamRoleDocumentTesting。

## 步骤五：（可选）获取临时授权Token

您可以获得实例RAM角色的临时授权Token，该临时授权Token可以执行实例RAM角色的权限和资源，并且该临时授权Token会自动周期性地更新。操作步骤如下：

检索名为EcsRamRoleDocumentTesting的实例RAM角色的临时授权Token。

-   Linux实例：执行命令`curl http://100.100.100.200/latest/meta-data/Ram/security-credentials/EcsRamRoleDocumentTesting`。
-   Windows实例：具体操作，请参见[实例元数据](/cn.zh-CN/实例/管理实例/使用实例元数据/ECS实例元数据概述.md)。

获得临时授权Token。返回示例如下：

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

## 步骤六：（可选）授权RAM用户使用实例RAM角色

**说明：** 当您授权RAM用户使用实例RAM角色时，您必须授权RAM用户对该实例RAM角色的PassRole权限。其中，PassRole决定该RAM用户能否直接执行角色策略赋予的权限。

1.  登录[RAM控制台](https://ram.console.aliyun.com/#/overview)。

2.  授权RAM用户使用实例RAM角色。具体操作，请参见[为RAM用户授权](/cn.zh-CN/用户管理/授权管理/为RAM用户授权.md)。

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

    其中，\[ECS RAM Action\]表示可授权RAM用户的权限，详情请参见[鉴权规则](/cn.zh-CN/API参考/鉴权规则.md)。


**相关文档**  


[授予实例RAM角色](/cn.zh-CN/安全/实例RAM角色/授予实例RAM角色.md)

[使用实例RAM角色访问其他云产品](/cn.zh-CN/最佳实践/使用实例RAM角色访问其他云产品.md)

[CreateRole](/cn.zh-CN/API参考/API参考（RAM）/角色管理接口/CreateRole.md)

[ListRoles](/cn.zh-CN/API参考/API参考（RAM）/角色管理接口/ListRoles.md)

[CreatePolicy](/cn.zh-CN/API参考/API参考（RAM）/权限策略管理接口/CreatePolicy.md)

[AttachPolicyToRole](/cn.zh-CN/API参考/API参考（RAM）/权限策略管理接口/AttachPolicyToRole.md)

[AttachInstanceRamRole](/cn.zh-CN/API参考/实例/AttachInstanceRamRole.md)

[DetachInstanceRamRole](/cn.zh-CN/API参考/实例/DetachInstanceRamRole.md)

[DescribeInstanceRamRole](/cn.zh-CN/API参考/实例/DescribeInstanceRamRole.md)

