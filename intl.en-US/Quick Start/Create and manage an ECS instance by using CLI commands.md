---
keyword: [CLoud Shell, create an ECS instance, use CLI commands to create an ECS instance, CLI]
---

# Create and manage an ECS instance by using CLI commands

If you are familiar with using Alibaba Cloud Command Line Interface \(CLI\) commands to manage Alibaba Cloud resources, you can use CLI commands to create ECS instances in the Cloud Shell console.

## Log on to the Cloud Shell console

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the upper-right corner, click the Cloud Shell icon to go to the Cloud Shell console.

    ![cloud shell](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7957219951/p100574.png)


## Preparations

Before you create an ECS instance, you must create a VPC and a security group.

1.  Create a VPC.

    Create a VPC in the **China \(Hangzhou\)** region. The CIDR block of the VPC is 192.168.0.0/16.

    |API operation|Parameter|Example|
    |-------------|---------|-------|
    |[CreateVpc](/intl.en-US/API reference/Virtual Private Cloud (VPC)/CreateVpc.md)|RegionId|The region ID of the VPC. Example: cn-hangzhou.|
    |CidrBlock|The CIDR block of the VPC. Example: 192.168.0.0/16|

    Run the following command to create a VPC:

    ```
    aliyun vpc CreateVpc \         
    --RegionId cn-hangzhou \       
    --CidrBlock 192.168.0.0/16
    ```

    The following command output is displayed:

    ```
    {
            "RequestId": "EC94C73B-8103-4B86-B353-E65C7C9E****",
            "ResourceGroupId": "rg-acfmzw2jz2z****",
            "RouteTableId": "vtb-bp1jxpr9ji5wcn4yv****",
            "VRouterId": "vrt-bp1dyxemup2q4ouga****",
            "VpcId": "vpc-bp1d9v4763ym2hlzt****"
    }
    ```

2.  Create a vSwitch.

    Create a vSwitch in the VPC. The CIDR block of the vSwitch is 192.168.0.0/24.

    |API operation|Parameter|Example|
    |-------------|---------|-------|
    |[CreateVSwitch](/intl.en-US/API reference/VSwitch/CreateVSwitch.md)|ZoneId|The zone ID of the vSwitch. Example: cn-hangzhou-i.|
    |VpcId|The ID of the VPC. Set the value to the VpcId value returned by the [CreateVpc](/intl.en-US/API reference/Virtual Private Cloud (VPC)/CreateVpc.md) operation. Example: vpc-bp1d9v4763ym2hlzt\*\*\*\*. |
    |CidrBlock|The CIDR block of the vSwitch. Example: 192.168.0.0/24.|

    Run the following command to create a vSwitch:

    ```
    aliyun vpc CreateVSwitch \
    --CidrBlock 192.168.0.0/24 \
    --VpcId vpc-bp1d9v4763ym2hlzt**** \
    --ZoneId=cn-hangzhou-i
    ```

    The following command output is displayed:

    ```
    {
            "RequestId": "AF1787C4-0D81-44F0-A324-D5C54EA0****",
            "VSwitchId": "vsw-bp11hf5r945gewysp****"
    }
    ```

3.  Create a security group.

    |API operation|Parameter|Example|
    |-------------|---------|-------|
    |[CreateSecurityGroup](/intl.en-US/API Reference/Security groups/CreateSecurityGroup.md)|RegionId|The region ID of the security group. Example: cn-hangzhou.|
    |VpcId|The ID of the VPC. Set the value to the VpcId value returned by the [CreateVpc](/intl.en-US/API reference/Virtual Private Cloud (VPC)/CreateVpc.md) operation. Example: vpc-bp1d9v4763ym2hlzt\*\*\*\*. |

    Run the following command to create a security group:

    ```
    aliyun ecs CreateSecurityGroup \
    --RegionId cn-hangzhou \
    --VpcId vpc-bp1d9v4763ym2hlzt****
    ```

    The following command output is displayed:

    ```
    {
            "RequestId": "B1C25C34-9B84-49E3-9E50-FB7D7970****",
            "SecurityGroupId": "sg-bp18z2q1jg4gq95t****"
    }
    ```

4.  Add an inbound rule to the security group.

    |API operation|Parameter|Example|
    |-------------|---------|-------|
    |[AuthorizeSecurityGroup](/intl.en-US/API Reference/Security groups/AuthorizeSecurityGroup.md)|RegionId|The region ID of the security group. Example: cn-hangzhou.|
    |SecurityGroupId|The ID of the security group. Set the value to the SecurityGroupId value returned by the [CreateSecurityGroup](/intl.en-US/API Reference/Security groups/CreateSecurityGroup.md) operation. Example: sg-bp18z2q1jg4gq95t\*\*\*\*. |
    |IpProtocol|The Internet protocol. Example: tcp.|
    |SourceCidrIp|The source CIDR block. Example: 0.0.0.0/0.|
    |PortRange|The port range:     -   Linux instances: 22/22
    -   Windows instances: 3389/3389 |

    Run the following command to add a security group rule:

    ```
    aliyun ecs AuthorizeSecurityGroup  \
    --RegionId cn-hangzhou \
    --SecurityGroupId sg-bp18z2q1jg4gq95t**** \
    --IpProtocol tcp \
    --SourceCidrIp 0.0.0.0/0 \
    --PortRange 22/22
    ```

    The following command output is displayed:

    ```
    {
            "RequestId": "FA8B1E61-C9C9-4D91-9628-64B8E2F4****"
    }
    ```


## Purchase an ECS instance

Purchase a subscription ECS instance.

|API operation|Parameter|Example|
|-------------|---------|-------|
|[RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md)|RegionId|The region ID of the instance. Example: cn-hangzhou.|
|ImageId|The ID of the image. The aliyun\_2\_1903\_x64\_20G\_alibase\_20200324.vhd Alibaba Cloud Linux image is recommended.|
|InstanceType|The instance type. -   Individual applications: The ecs.s6-c1m2.small instance type with one vCPU and 2 GiB of memory is recommended.
-   Applications for small and medium-sized enterprises: The ecs.c5.large instance type with two vCPUs and 4 GiB of memory is recommended. |
|SecurityGroupId|The ID of the security group. Set the value to the SecurityGroupId value returned by the [CreateSecurityGroup](/intl.en-US/API Reference/Security groups/CreateSecurityGroup.md) operation. Example: sg-bp18z2q1jg4gq95t\*\*\*\*. |
|VSwitchId|The ID of the vSwitch. Set the value to the VSwitchId value returned by the [CreateVSwitch](/intl.en-US/API reference/VSwitch/CreateVSwitch.md) operation. Example: vsw-bp11hf5r945gewysp\*\*\*\*. |
|InstanceName|The name of the instance to be created. Example: ecs\_cli\_demo. |
|InstanceChargeType|The billing method. To create a subscription instance, set the value to PrePaid. **Note:** You must make sure that you have sufficient balance in your account. |
|PeriodUnit|The unit of the billing cycle. Example: Month.|
|Period|The period of the billing cycle. Example: 1.|
|InternetMaxBandwidthOut|The maximum outbound public bandwidth. Example: 1.|
|Password|The logon password of the instance: <Your password\>. **Note:** You must customize a complex password to ensure instance security. |

Run the following command to create a subscription instance:

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

The following command output is displayed:

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

## Connect to the ECS instance

This section describes how to connect to a Linux instance by using Cloud Shell. For information about how to connect to a Windows instance, see [Connect to a Windows instance from a local client](/intl.en-US/Instance/Connect to instances/Connect to Windows instances/Connect to a Windows instance from a local client.md).

1.  Query the public IP address of the instance.

    |API operation|Parameter|Example|
    |-------------|---------|-------|
    |[DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md)|RegionId|The region ID of the instance. Example: cn-hangzhou.|
    |InstanceIds|The ID of the instance. Set the value to the InstanceIds value returned by the [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md) operation. Example: '\["i-bp1ducce5hs1jm98\*\*\*\*"\]'. |

    Run the following command to query the public IP address of the instance:

    ```
    aliyun ecs DescribeInstances \
    --RegionId cn-hangzhou \
    --InstanceIds '["i-bp1ducce5hs1jm98****"]'
    ```

    Find the following public IP address in the command output.

    ![Public IP address](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9957219951/p100712.png)

2.  Use an SSH key pair to log on to the instance.

    ![Logon with an SSH key pair](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0067219951/p100726.png)


## Release an ECS instance

You can manually release a subscription instance after it expires. If you do not renew the instance after it expires, the instance is automatically released.

