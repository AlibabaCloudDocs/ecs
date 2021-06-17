---
keyword: [CLoud Shell, 创建ECS实例, CLI方式创建ECS实例, CLI]
---

# 通过CLI使用ECS实例

如果您平时习惯使用CLI方式运维阿里云资源，可以通过CLoud Shell以CLI方式快速创建ECS实例。

## 登录阿里云CLoud Shell控制台

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

    **说明：** 如果未注册阿里云账号，请先注册账号。具体请参见[注册阿里云账号](https://www.alibabacloud.com/help/doc-detail/50482.htm)。

2.  单击右上角的Cloud Shell图标，进入CLoud Shell控制台。

    ![cloud shell](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6576193261/p100574.png)


## 创建ECS实例准备工作

在创建ECS实例前，您需要先创建专有网络VPC和安全组。

1.  创建VPC。

    在**华东1（杭州）**创建专有网络VPC，VPC网段为192.168.0.0/16。

    |API|参数|示例取值|
    |---|--|----|
    |[CreateVpc](/cn.zh-CN/API参考/专有网络（VPC）/CreateVpc.md)|RegionId|地域：cn-hangzhou|
    |CidrBlock|VPC网段：192.168.0.0/16|

    执行以下命令创建VPC。

    ```
    aliyun vpc CreateVpc \
    --RegionId cn-hangzhou \
    --CidrBlock 192.168.0.0/16
    ```

    返回结果如下所示。

    ```
    {
            "RequestId": "EC94C73B-8103-4B86-B353-E65C7C9E****",
            "ResourceGroupId": "rg-acfmzw2jz2z****",
            "RouteTableId": "vtb-bp1jxpr9ji5wcn4yv****",
            "VRouterId": "vrt-bp1dyxemup2q4ouga****",
            "VpcId": "vpc-bp1d9v4763ym2hlzt****"
    }
    ```

2.  创建交换机。

    在VPC中创建交换机，交换机网段为192.168.0.0/24。

    |API|参数|示例取值|
    |---|--|----|
    |[CreateVSwitch](/cn.zh-CN/API参考/交换机/CreateVSwitch.md)|ZoneId|可用区：cn-hangzhou-i|
    |VpcId|VPC ID：根据[CreateVpc](/cn.zh-CN/API参考/专有网络（VPC）/CreateVpc.md)返回结果。 示例：vpc-bp1d9v4763ym2hlzt\*\*\*\* |
    |CidrBlock|交换机网段：192.168.0.0/24|

    执行以下命令创建交换机。

    ```
    aliyun vpc CreateVSwitch \
    --CidrBlock 192.168.0.0/24 \
    --VpcId vpc-bp1d9v4763ym2hlzt**** \
    --ZoneId=cn-hangzhou-i
    ```

    返回结果如下所示。

    ```
    {
            "RequestId": "AF1787C4-0D81-44F0-A324-D5C54EA0****",
            "VSwitchId": "vsw-bp11hf5r945gewysp****"
    }
    ```

3.  创建安全组。

    |API|参数|示例取值|
    |---|--|----|
    |[CreateSecurityGroup](/cn.zh-CN/API参考/安全组/CreateSecurityGroup.md)|RegionId|地域：cn-hangzhou|
    |VpcId|VPC ID：根据[CreateVpc](/cn.zh-CN/API参考/专有网络（VPC）/CreateVpc.md)返回结果。 示例：vpc-bp1d9v4763ym2hlzt\*\*\*\* |

    执行以下命令创建安全组。

    ```
    aliyun ecs CreateSecurityGroup \
    --RegionId cn-hangzhou \
    --VpcId vpc-bp1d9v4763ym2hlzt****
    ```

    返回结果如下所示。

    ```
    {
            "RequestId": "B1C25C34-9B84-49E3-9E50-FB7D7970****",
            "SecurityGroupId": "sg-bp18z2q1jg4gq95t****"
    }
    ```

4.  在安全组中添加入方向放行规则。

    |API|参数|示例取值|
    |---|--|----|
    |[AuthorizeSecurityGroup](/cn.zh-CN/API参考/安全组/AuthorizeSecurityGroup.md)|RegionId|地域：cn-hangzhou|
    |SecurityGroupId|安全组ID：根据[CreateSecurityGroup](/cn.zh-CN/API参考/安全组/CreateSecurityGroup.md)返回结果。 示例：sg-bp18z2q1jg4gq95t\*\*\*\* |
    |IpProtocol|协议：tcp|
    |SourceCidrIp|源CIDR：0.0.0.0/0|
    |PortRange|端口范围：     -   Linux实例：22/22
    -   Windows实例：3389/3389 |

    执行以下命令添加安全组规则。

    ```
    aliyun ecs AuthorizeSecurityGroup  \
    --RegionId cn-hangzhou \
    --SecurityGroupId sg-bp18z2q1jg4gq95t**** \
    --IpProtocol tcp \
    --SourceCidrIp 0.0.0.0/0 \
    --PortRange 22/22
    ```

    返回结果如下所示。

    ```
    {
            "RequestId": "FA8B1E61-C9C9-4D91-9628-64B8E2F4****"
    }
    ```


## 购买ECS实例

购买一个包年包月的ECS实例。

|API|参数|示例取值|
|---|--|----|
|[RunInstances](/cn.zh-CN/API参考/实例/RunInstances.md)|RegionId|地域：cn-hangzhou|
|ImageId|镜像：推荐使用Alibaba Cloud Linux镜像aliyun\_2\_1903\_x64\_20G\_alibase\_20200324.vhd。|
|InstanceType|实例规格： -   个人应用：推荐选择1核2G的实例规格ecs.s6-c1m2.small。
-   中小企业应用：推荐选择2核4G的实例规格ecs.c5.large。 |
|SecurityGroupId|安全组ID：根据[CreateSecurityGroup](/cn.zh-CN/API参考/安全组/CreateSecurityGroup.md)返回结果。 示例：sg-bp18z2q1jg4gq95t\*\*\*\* |
|VSwitchId|交换机ID：根据[CreateVSwitch](/cn.zh-CN/API参考/交换机/CreateVSwitch.md)返回结果。 示例：vsw-bp11hf5r945gewysp\*\*\*\* |
|InstanceName|实例名称。 示例：ecs\_cli\_demo |
|InstanceChargeType|付费方式：实例按照包年包月的付费方式PrePaid。 **说明：** 您需要确保账号余额能够完成支付。 |
|PeriodUnit|付费周期单位：Month|
|Period|付费时长：1|
|InternetMaxBandwidthOut|公网IP带宽：1|
|Password|实例登录密码：<yourPassword\>**说明：** 您需要自定义复杂密码以保护ECS实例的安全。 |

执行以下命令创建包年包月的ECS实例。

```
aliyun ecs RunInstances \
--RegionId cn-hangzhou \
--ImageId aliyun_2_1903_x64_20G_alibase_20200324.vhd \
--InstanceType ecs.s6-c1m2.small \
--SecurityGroupId sg-bp18z2q1jg4gq95t**** \
--VSwitchId vsw-bp11hf5r945gewys**** \
--InstanceName ecs_cli_demo \
--InstanceChargeType PrePaid \
--PeriodUnit Month \
--Period 1 \
--InternetMaxBandwidthOut 1 \
--Password <yourPassword>
```

返回结果如下所示。

```
{
        "InstanceIdSets": {
                "InstanceIdSet": [
                        "i-bp1ducce5hs1jm98****"
                ]
        },
        "RequestId": "7F0166F9-9466-4AE1-8799-E68D6514****",
        "TradePrice": ****
}
```

## 连接ECS实例

此示例介绍通过Cloud Shell登录Linux实例。如果您安装的是Windows实例，登录方式请参见[在本地客户端上连接Windows实例](/cn.zh-CN/实例/连接实例/使用第三方客户端工具连接实例/在本地客户端上连接Windows实例.md)。

1.  查询实例公网IP地址。

    |API|参数|示例取值|
    |---|--|----|
    |[DescribeInstances](/cn.zh-CN/API参考/实例/DescribeInstances.md)|RegionId|地域：cn-hangzhou|
    |InstanceIds|实例ID：根据[RunInstances](/cn.zh-CN/API参考/实例/RunInstances.md)返回结果。 示例：'\["i-bp1ducce5hs1jm98\*\*\*\*"\]' |

    执行以下命令查询实例公网IP。

    ```
    aliyun ecs DescribeInstances \
    --RegionId cn-hangzhou \
    --InstanceIds '["i-bp1ducce5hs1jm98****"]'
    ```

    在返回结果中找到以下公网IP信息。

    ![公网IP](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9396958951/p100712.png)

2.  通过SSH登录ECS实例。

    ![ssh登录](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0496958951/p100726.png)


## 释放ECS实例

包年包月实例到期后，您可以手动释放。如果一直未续费，实例也会自动释放。

如果您想要提前释放包年包月实例，请参见[退款规则及退款流程](https://help.aliyun.com/document_detail/37096.html)。

