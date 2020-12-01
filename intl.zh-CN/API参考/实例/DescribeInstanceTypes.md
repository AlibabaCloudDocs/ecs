# DescribeInstanceTypes

调用DescribeInstanceTypes查询云服务器ECS提供的实例规格资源。

## 接口说明

DescribeInstanceTypes仅查询实例规格的配置和性能信息。如果您需要查询具体地域下可购买的实例规格，请使用[DescribeAvailableResource](~~66186~~)。

如果您需要使用非售卖可见的实例规格或特别的规格需求，请[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)联系阿里云。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceTypes&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeInstanceTypes|系统规定参数。取值：DescribeInstanceTypes |
|InstanceTypeFamily|String|否|ecs.g6|实例规格所属的规格族。取值请参见[DescribeInstanceTypeFamilies](~~25621~~)。

 更多详情，请参见[实例规格族](~~25378~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceTypes|Array of InstanceType| |实例规格集合。 |
|InstanceType| | | |
|BaselineCredit|Integer|4|突发性能实例t5、t6的基准vCPU计算性能（所有vCPU之和）。 |
|CpuCoreCount|Integer|8|vCPU内核数目。 |
|EniIpv6AddressQuantity|Integer|1|单块弹性网卡的IPv6地址上限。 |
|EniPrivateIpAddressQuantity|Integer|6|单块弹性网卡的私有IP地址上限。 |
|EniQuantity|Integer|2|支持挂载的弹性网卡上限。 |
|EniTotalQuantity|Integer|0|**说明：** 该参数正在邀测中，暂未开放使用。 |
|EniTrunkSupported|Boolean|false|**说明：** 该参数正在邀测中，暂未开放使用。 |
|GPUAmount|Integer|2|GPU数量。 |
|GPUSpec|String|NVIDIA V100|GPU类型。 |
|InitialCredit|Integer|120|突发性能实例t5、t6的初始vCPU积分值。 |
|InstanceBandwidthRx|Integer|1024000|内网入方向带宽限制。单位：kbit/s |
|InstanceBandwidthTx|Integer|1024000|内网出方向带宽限制。单位：kbit/s |
|InstanceFamilyLevel|String|EnterpriseLevel|实例规格族级别。可能值：

 -   EntryLevel：入门级。
-   EnterpriseLevel：企业级。
-   CreditEntryLevel：积分入门级。详情请参见[突发性能实例](~~59977~~)。 |
|InstancePpsRx|Long|300000|内网入方向网络收发包能力。单位：Pps |
|InstancePpsTx|Long|300000|内网出方向网络收发包能力。单位：Pps |
|InstanceTypeFamily|String|ecs.g5|实例规格族。 |
|InstanceTypeId|String|ecs.g5.large|实例规格ID。 |
|LocalStorageAmount|Integer|1|实例挂载的本地盘的数量。 |
|LocalStorageCapacity|Long|5000|实例挂载的本地盘的单盘容量。单位：GiB |
|LocalStorageCategory|String|local\_ssd\_pro|本地盘类型，详情请参见[本地盘](~~63138~~)。可能值：

 -   local\_hdd\_pro：实例规格族d1ne和d1搭载的SATA HDD本地盘。
-   local\_ssd\_pro：实例规格族i2、i2g、i1、ga1和gn5等搭载的NVMe SSD本地盘。 |
|MaximumQueueNumberPerEni|Integer|8|单块弹性网卡最大队列数。 |
|MemorySize|Float|8.0|内存大小。单位：GiB |
|PrimaryEniQueueNumber|Integer|4|主网卡默认队列数。 |
|SecondaryEniQueueNumber|Integer|4|辅助弹性网卡默认队列数。 |
|TotalEniQueueQuantity|Integer|128|实例规格允许修改的弹性网卡队列数总配额。 |
|RequestId|String|00827261-20B7-4562-83F2-4DF39876A45A|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceTypes
&InstanceTypeFamily=ecs.g6
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeInstanceTypesResponse>
      <RequestId>CEC8A6BA-6805-4807-AB93-EB2E4B59EAF3</RequestId>
      <InstanceTypes>
            <InstanceType>
                  <MemorySize>256</MemorySize>
                  <InstancePpsTx>4000000</InstancePpsTx>
                  <EniIpv6AddressQuantity>1</EniIpv6AddressQuantity>
                  <PrimaryEniQueueNumber>32</PrimaryEniQueueNumber>
                  <CpuCoreCount>64</CpuCoreCount>
                  <TotalEniQueueQuantity>256</TotalEniQueueQuantity>
                  <EniTotalQuantity>60</EniTotalQuantity>
                  <EniTrunkSupported>true</EniTrunkSupported>
                  <InstanceTypeFamily>ecs.g6</InstanceTypeFamily>
                  <InstancePpsRx>4000000</InstancePpsRx>
                  <EniQuantity>8</EniQuantity>
                  <InstanceBandwidthRx>20480000</InstanceBandwidthRx>
                  <GPUAmount>0</GPUAmount>
                  <InstanceBandwidthTx>20480000</InstanceBandwidthTx>
                  <SecondaryEniQueueNumber>32</SecondaryEniQueueNumber>
                  <LocalStorageCategory></LocalStorageCategory>
                  <GPUSpec></GPUSpec>
                  <InstanceFamilyLevel>EnterpriseLevel</InstanceFamilyLevel>
                  <InstanceTypeId>ecs.g6.16xlarge</InstanceTypeId>
                  <EniPrivateIpAddressQuantity>20</EniPrivateIpAddressQuantity>
            </InstanceType>
            <InstanceType>
                  <MemorySize>128</MemorySize>
                  <InstancePpsTx>2000000</InstancePpsTx>
                  <EniIpv6AddressQuantity>1</EniIpv6AddressQuantity>
                  <PrimaryEniQueueNumber>16</PrimaryEniQueueNumber>
                  <CpuCoreCount>32</CpuCoreCount>
                  <TotalEniQueueQuantity>128</TotalEniQueueQuantity>
                  <EniTotalQuantity>8</EniTotalQuantity>
                  <EniTrunkSupported>false</EniTrunkSupported>
                  <InstanceTypeFamily>ecs.g6</InstanceTypeFamily>
                  <InstancePpsRx>2000000</InstancePpsRx>
                  <EniQuantity>8</EniQuantity>
                  <InstanceBandwidthRx>10240000</InstanceBandwidthRx>
                  <GPUAmount>0</GPUAmount>
                  <InstanceBandwidthTx>10240000</InstanceBandwidthTx>
                  <SecondaryEniQueueNumber>16</SecondaryEniQueueNumber>
                  <LocalStorageCategory></LocalStorageCategory>
                  <GPUSpec></GPUSpec>
                  <InstanceFamilyLevel>EnterpriseLevel</InstanceFamilyLevel>
                  <InstanceTypeId>ecs.g6nv.8xlarge</InstanceTypeId>
                  <EniPrivateIpAddressQuantity>20</EniPrivateIpAddressQuantity>
            </InstanceType>
      </InstanceTypes>
</DescribeInstanceTypesResponse>
```

`JSON` 格式

```
{
	"RequestId": "CEC8A6BA-6805-4807-AB93-EB2E4B59EAF3",
	"InstanceTypes": {
		"InstanceType": [
			{
				"MemorySize": 256,
				"InstancePpsTx": 4000000,
				"EniIpv6AddressQuantity": 1,
				"PrimaryEniQueueNumber": 32,
				"CpuCoreCount": 64,
				"TotalEniQueueQuantity": 256,
				"EniTotalQuantity": 60,
				"EniTrunkSupported": true,
				"InstanceTypeFamily": "ecs.g6",
				"InstancePpsRx": 4000000,
				"EniQuantity": 8,
				"InstanceBandwidthRx": 20480000,
				"GPUAmount": 0,
				"InstanceBandwidthTx": 20480000,
				"SecondaryEniQueueNumber": 32,
				"LocalStorageCategory": "",
				"GPUSpec": "",
				"InstanceFamilyLevel": "EnterpriseLevel",
				"InstanceTypeId": "ecs.g6.16xlarge",
				"EniPrivateIpAddressQuantity": 20
			},
			{
				"MemorySize": 128,
				"InstancePpsTx": 2000000,
				"EniIpv6AddressQuantity": 1,
				"PrimaryEniQueueNumber": 16,
				"CpuCoreCount": 32,
				"TotalEniQueueQuantity": 128,
				"EniTotalQuantity": 8,
				"EniTrunkSupported": false,
				"InstanceTypeFamily": "ecs.g6",
				"InstancePpsRx": 2000000,
				"EniQuantity": 8,
				"InstanceBandwidthRx": 10240000,
				"GPUAmount": 0,
				"InstanceBandwidthTx": 10240000,
				"SecondaryEniQueueNumber": 16,
				"LocalStorageCategory": "",
				"GPUSpec": "",
				"InstanceFamilyLevel": "EnterpriseLevel",
				"InstanceTypeId": "ecs.g6nv.8xlarge",
				"EniPrivateIpAddressQuantity": 20
			}
		]
	}
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

