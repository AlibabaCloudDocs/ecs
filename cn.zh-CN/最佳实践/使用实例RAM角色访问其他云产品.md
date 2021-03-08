# 使用实例RAM角色访问其他云产品

本文以部署在ECS实例上的Python访问OSS为例，详细介绍了如何借助ECS实例RAM角色，使实例内部的应用程序可以使用STS临时凭证访问其他云产品。

已创建一个ECS实例，详情请参见[使用向导创建实例](/cn.zh-CN/实例/创建实例/使用向导创建实例.md)。

以往部署在ECS实例中的应用程序如果需要访问阿里云其他云产品，您通常需要借助AccessKeyID和AccessKeySecret（下文简称AK）来实现。AK是您访问阿里云API的密钥，具有相应账号的完整权限。为了方便应用程序对AK的管理，您通常需要将AK保存在应用程序的配置文件中或以其他方式保存在ECS实例中，这在一定程度上增加了AK管理的复杂性，并且降低了AK的保密性。甚至，如果您需要实现多地域一致性部署，AK会随着镜像以及使用镜像创建的实例扩散出去。这种情况下，当您需要更换AK时，您就需要逐台更新和重新部署实例和镜像。

现在借助于ECS实例RAM角色，您可以将RAM角色和ECS实例关联起来，实例内部的应用程序可以通过STS临时凭证访问其他云产品。其中STS临时凭证由系统自动生成和更新，应用程序可以使用指定的实例元数据URL获取STS临时凭证，无需特别管理。同时借助于RAM，通过对角色和授权策略的管理，您可以达到不同实例对不同云产品或相同云产品具有各自访问权限的目的。

**说明：** 为了方便您随本文样例快速入门，文档里所有操作均在[OpenAPI开发者门户](https://next.api.aliyun.com/api/Ecs/2014-05-26)完成。OpenAPI Explorer通过已登录用户信息获取当前账号临时AK，对当前账号发起线上资源操作，请谨慎操作。创建实例操作会产生费用。操作完成后请及时释放实例。

## 操作步骤

为了使ECS借助实例RAM角色，实现内部Python可以使用STS临时凭证访问OSS，您需要完成以下步骤：

1.  [步骤一：创建RAM角色并配置授权策略](#section_bjf_m1b_l19)
2.  [步骤二：指定RAM角色创建并设置ECS实例](#section_z5t_5l9_x28)
3.  [步骤三：在实例内部访问实例元数据URL获取STS临时凭证](#section_r5g_ndb_7kj)
4.  [步骤四：基于临时凭证，使用Python SDK访问OSS](#section_fgc_wkp_1gq)

## 步骤一：创建RAM角色并配置授权策略

完成以下步骤，创建RAM角色并配置授权策略：

1.  创建RAM角色。

    找到OpenAPI开发者门户RAM产品下CreateRole API。其中：

    -   RoleName：设置角色的名称。根据自己的需要填写，本示例中为 EcsRamRoleTest。
    -   AssumeRolePolicyDocument： 填写如下内容，表示该角色为一个服务角色，受信云服务（本示例中为ECS）可以扮演该角色。

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

2.  创建授权策略。

    找到OpenAPI开发者门户RAM产品下的CreatePolicy API。其中：

    -   PolicyName：设置授权策略的名称。本示例中为EcsRamRolePolicyTest。
    -   PolicyDocument：输入授权策略内容。本示例中填写如下内容，表示该角色具有OSS只读权限。

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

3.  为角色附加授权。找到OpenAPI开发者门户RAM产品下的AttachPolicyToRole API。

    -   PolicyType：填写Custom。
    -   PolicyName：填写第2步创建的策略名称，如本示例中的EcsRamRolePolicyTest。
    -   RoleName：填写第1步创建的角色名称，如本示例中的EcsRamRoleTest。

## 步骤二：指定RAM角色创建并设置ECS实例

您可以通过以下任一种方式为ECS实例指定RAM角色：

-   将实例RAM角色附加到一个已创建的ECS实例上

    您可以使用ECS的AttachInstanceRamRole API附加实例RAM角色到已有的VPC类型ECS实例授权访问，设置信息如下：

    -   RegionId：为实例所在的地域ID。
    -   RamRoleName：RAM角色的名称。本示例中为EcsRamRoleTest。
    -   InstanceIds：需要附加实例RAM角色的VPC类型ECS实例ID。本示例中为\["i-bXXXXXXXX"\]。
-   指定RAM角色创建并设置ECS实例

    按以下步骤指定RAM角色创建并设置ECS实例。

    1.  创建实例。

        找到OpenAPI开发者门户ECS产品下的CreateInstance API，根据实际情况填写请求参数。必须填写的参数包括：

        -   RegionId：实例所在地域。本示例中为cn-hangzhou。
        -   ImageId：实例的镜像。本示例中为centos\_7\_03\_64\_40G\_alibase\_20170503.vhd。
        -   InstanceType：实例的规格。本示例中为ecs.g6.large。
        -   VSwitchId：实例所在的VPC虚拟交换机。因为ECS实例RAM角色目前只支持VPC类型ECS实例，所以VSwitchId是必需的。
        -   RamRoleName：RAM角色的名称。本示例中为EcsRamRoleTest。
        如果您希望授权子账号创建指定RAM角色的ECS实例，那么子账号除了拥有创建ECS实例的权限之外，还需要增加PassRole权限。所以，您需要创建一个如下所示的自定义授权策略并绑定到子账号上。

        -   如果是创建ECS实例，\[ECS RAM Action\]可以是`ecs:CreateInstance`，您也可以根据实际情况添加更多的权限。
        -   如果您需要为子账号授予所有ECS操作权限，\[ECS RAM Action\]应该替换为`ecs:*`。
        **说明：** \[ECS RAM Action\]的取值详情请参见[鉴权规则](/cn.zh-CN/API参考/鉴权规则.md)。

        ```
        {
            "Statement": [
                {
                    "Action": "[ECS RAM Action]", 
                    "Resource": "*", 
                    "Effect": "Allow"
                }, 
                {
                    "Action": "ram:PassRole", 
                    "Resource": "*", 
                    "Effect": "Allow"
                }
            ], 
            "Version": "1"
        }
        ```

    2.  设置密码并启动实例。
    3.  使用API或在控制台设置ECS实例能访问公网。

## 步骤三：在实例内部访问实例元数据URL获取STS临时凭证

完成以下步骤，获取实例的STS临时凭证：

**说明：** STS临时凭证失效前半小时会生成新的STS临时凭证，在这半小时内，新旧STS临时凭证均可使用。

1.  远程连接ECS实例。连接方式请参见[连接方式概述](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

2.  访问`http://100.100.100.200/latest/meta-data/ram/security-credentials/EcsRamRoleTest`获取STS临时凭证。路径最后一部分是RAM角色名称，您应当替换为自己创建的RAM角色名称。

    **说明：** 本示例中使用`curl`命令访问上述URL。如果您使用的是Windows ECS实例，请参见[实例元数据](/cn.zh-CN/实例/管理实例/使用实例元数据/实例元数据概述.md)。

    示例输出结果如下。

    ```
    [root@local ~]# curl http://100.100.100.200/latest/meta-data/ram/security-credentials/EcsRamRoleTest
    {
    "AccessKeyId" : "STS.J8XXXXXXXXXX4",
    "AccessKeySecret" : "9PjfXXXXXXXXXBf2XAW",
    "Expiration" : "2017-06-09T09:17:19Z",
    "SecurityToken" : "CAIXXXXXXXXXXXwmBkleCTkyI+",
    "LastUpdated" : "2017-06-09T03:17:18Z",
    "Code" : "Success"
    }
    ```


## 步骤四：基于临时凭证，使用Python SDK访问OSS

本示例中，我们基于STS临时凭证使用Python SDK列举实例所在地域的某个OSS存储空间（Bucket）里的10个文件。

前提条件：

-   您已经远程连接到ECS实例。
-   您的ECS实例已经安装了Python。如果您用的是Linux ECS实例，必须安装pip。
-   您在实例所在的地域已经创建了存储空间（Bucket），并已经获取Bucket的名称和Endpoint。本示例中，Bucket名称为`ramroletest`，Endpoint为`oss-cn-hangzhou.aliyuncs.com`。

完成以下步骤，使用Python SDK访问OSS：

1.  运行命令`pip install oss2`，安装OSS Python SDK。

    **说明：** 如果您用的是Windows ECS实例，请参见 *对象存储 OSS SDK 参考*的[安装 Python SDK](https://help.aliyun.com/document_detail/32026.html?spm=a2c4g.11186623.2.27.17c718efkTbBei)。

2.  执行下述命令进行测试。

    ```
    import oss2
    from itertools import islice
    auth = oss2.StsAuth(<AccessKeyId>, <AccessKeySecret>, <SecurityToken>)
    bucket = oss2.Bucket(auth, <您的 Endpoint>, <您的 Bucket 名称>)
    for b in islice(oss2.ObjectIterator(bucket), 10):
      print(b.key)
    ```

    其中：

    -   `oss2.StsAuth`中的3个参数分别对应于[步骤三](#section_r5g_ndb_7kj)中返回的AccessKeyId、AccessKeySecret和SecurityToken。
    -   `oss2.Bucket`中后2个参数是Bucket的名称和Endpoint。
    示例输出结果如下。

    ```
    [root@local ~]# python
    Python 2.7.5 (default, Nov  6 2016, 00:28:07)
    [GCC 4.8.5 20150623 (Red Hat 4.8.5-11)] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    >>> import oss2
    >>> from itertools import islice
    >>> auth = oss2.StsAuth("STS.J8XXXXXXXXXX4", "9PjfXXXXXXXXXBf2XAW", "CAIXXXXXXXXXXXwmBkleCTkyI+")
    >>> bucket = oss2.Bucket(auth, "oss-cn-hangzhou.aliyuncs.com", "ramroletest")
    >>> for b in islice(oss2.ObjectIterator(bucket), 10):
    ...     print(b.key)
    ...
    ramroletest.txt
    test.shh
    ```


