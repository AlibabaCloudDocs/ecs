# 通过镜像族系创建ECS实例

本文介绍如何通过镜像族系创建ECS实例。目前只支持通过调用RunInstances或CreateInstance接口设置镜像族系参数来创建ECS实例。

已经创建一个或多个可用的自定义镜像并设置了相同的镜像族系，具体操作，请参见[设置镜像族系](/cn.zh-CN/镜像/镜像族系/设置镜像族系.md)。本示例中镜像族系为`image-test`。

通过镜像族系创建ECS实例时，系统会自动选取镜像族系内可用的最新自定义镜像。最新自定义镜像的判断依据为镜像族系内可用自定义镜像的创建时间，创建时间最晚的自定义镜像为最新自定义镜像。例如，您的镜像族系内有两个可用的自定义镜像。一个是2020年01月01日创建的，另一个是2020年01月03日创建的，那么通过该镜像族系创建ECS实例时，系统将默认选择2020年01月03日创建的自定义镜像。

创建ECS实例的接口详情请参见[RunInstances](/cn.zh-CN/API参考/实例/RunInstances.md)或[CreateInstance](/cn.zh-CN/API参考/实例/CreateInstance.md)。本文以RunInstances接口为例创建ECS实例。

## 使用API RunInstances创建ECS实例

1.  登录[OpenAPI开发者门户](https://next.api.aliyun.com/api/Ecs/2014-05-26)。

2.  查找并调用RunInstances接口创建一台ECS实例。

    本示例中，通过镜像族系`image-test`创建ECS示例，API的请求参数说明如下：

    -   RegionId：选择地域。例如，`cn-hangzhou`，即华东1（杭州）。
    -   InstanceType：实例规格。例如，`ecs.g6.large`。
    -   ImageFamily：镜像族系。本示例使用`image-test`。
    -   SecurityGroupId：安全组ID。例如，`sg-bp1i4c0xgqxadew2****`。
    -   VSwitchId：交换机ID。例如，`vsw-bp1ddbrxdlrcbim46****`。
    调用结果示例如下，得到创建的实例ID。

    ```
    {
        "RequestId": "409D4604-84D0-4F16-B99E-809E2E72****",
        "InstanceIdSets": {
            "InstanceIdSet": [
                "i-bp1env7nl3mijm2t****"
            ]
        }
    }
    ```


## 通过调用API验证镜像信息

1.  登录[OpenAPI开发者门户](https://next.api.aliyun.com/api/Ecs/2014-05-26)。

2.  查找并调用DescribeImageFromFamily接口查询指定镜像族系内最新的镜像。

    本示例中，查询镜像族系`image-test`内最新的镜像，API的请求参数说明如下：

    -   RegionId：选择镜像族系同一地域。
    -   ImageFamily：镜像族系。本示例中使用`image-test`。
    返回值部分示例如下，得到最新可用自定义镜像的ID。

    ![11](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4425209951/p93803.png)

3.  查找并调用DescribeInstances接口查询实例的镜像信息。

    通过已创建的实例ID查询对应的镜像ID，判断是否为镜像族系中最新可用自定义镜像的ID。API的请求参数说明如下：

    -   RegionId：选择ECS实例所在的地域。
    -   InstanceIds：实例ID。格式为`["i-bp1env7nl3mijm2t****"]`。
    返回值的部分结果示例如下，对比实例的镜像ID与镜像族系中最新可用自定义镜像的ID一致。

    ![if8](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5425209951/p93653.png)


## 相关文档

-   [DescribeInstances](/cn.zh-CN/API参考/实例/DescribeInstances.md)
-   [DescribeImageFromFamily](/cn.zh-CN/API参考/镜像/DescribeImageFromFamily.md)

