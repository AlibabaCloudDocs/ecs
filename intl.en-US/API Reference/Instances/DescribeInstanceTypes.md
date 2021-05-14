# DescribeInstanceTypes

You can call this operation to query all instance types provided by Elastic Compute Service \(ECS\). You can also query information about a specific instance type.

## Description

The DescribeInstanceTypes operation is used to query only the specifications and performance information of instance types. To query instance types that are available in a region, call the [DescribeAvailableResource](~~66186~~) operation.

To use special instance types such as instance types that are unavailable for purchase, [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceTypes&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeInstanceTypes|The operation that you want to perform. Set the value to DescribeInstanceTypes. |
|InstanceTypeFamily|String|No|ecs.g6|The instance family to which the instance type belongs. For the valid values, see [DescribeInstanceTypeFamilies](~~25621~~).

 For more information, see [Instance families](~~25378~~). |
|InstanceTypes.N|RepeatList|No|ecs.g6.large|Instance type N. Valid values of N: 1 to 10. If this parameter is empty, information about all instance types is queried. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|InstanceTypes|Array of InstanceType| |Details about the instance types. |
|InstanceType| | | |
|BaselineCredit|Integer|4|The baseline vCPU computing performance \(overall computing performance of all vCPUs\) of the t5 or t6 burstable instance family. |
|CpuCoreCount|Integer|2|The number of vCPUs. |
|DiskQuantity|Integer|17|The maximum number of cloud disks that can be attached per instance. |
|EniIpv6AddressQuantity|Integer|1|The maximum number of IPv6 addresses per elastic network interface \(ENI\). |
|EniPrivateIpAddressQuantity|Integer|6|The maximum number of private IP addresses per ENI. |
|EniQuantity|Integer|2|The maximum number of ENIs that can be bound per instance. |
|EniTotalQuantity|Integer|0|**Note:** This parameter is in invitational preview and unavailable. |
|EniTrunkSupported|Boolean|false|**Note:** This parameter is in invitational preview and unavailable. |
|GPUAmount|Integer|0|The number of GPUs. |
|GPUSpec|String|NVIDIA V100|The GPU type. |
|InitialCredit|Integer|120|The initial vCPU credits of the t5 or t6 burstable instance family. |
|InstanceBandwidthRx|Integer|1024000|The maximum inbound internal bandwidth. Unit: Kbit/s |
|InstanceBandwidthTx|Integer|1024000|The maximum outbound internal bandwidth. Unit: Kbit/s |
|InstanceFamilyLevel|String|EnterpriseLevel|The level of the instance family. Valid values:

 -   EntryLevel.
-   EnterpriseLevel.
-   CreditEntryLevel. For more information, see [Burstable instance families](~~59977~~). |
|InstancePpsRx|Long|300000|The inbound packet forwarding rate over the internal network. Unit: pps. |
|InstancePpsTx|Long|300000|The outbound packet forwarding rate over the internal network. Unit: pps. |
|InstanceTypeFamily|String|ecs.g6|The instance family. |
|InstanceTypeId|String|ecs.g6.large|The ID of the instance type. |
|LocalStorageAmount|Integer|1|The number of local disks attached per instance. |
|LocalStorageCapacity|Long|5000|The capacity of each local disk attached per instance. Unit: GiB. |
|LocalStorageCategory|String|local\_ssd\_pro|The category of the local disks. For more information, see [Local disks](~~63138~~). Valid values:

 -   local\_hdd\_pro: local SATA HDDs, which are attached to d1ne or d1 instances
-   local\_ssd\_pro: local NVMe SSDs, which are attached to i2, i2g, i1, ga1, or gn5 instances |
|MaximumQueueNumberPerEni|Integer|2|The maximum number of queues per ENI. |
|MemorySize|Float|8.0|The memory size. Unit: GiB. |
|PrimaryEniQueueNumber|Integer|2|The default number of queues supported by the primary ENI. |
|SecondaryEniQueueNumber|Integer|2|The default number of queues supported by the secondary ENI. |
|TotalEniQueueQuantity|Integer|4|The maximum number of queues on ENIs that the instance type supports. |
|RequestId|String|00827261-20B7-4562-83F2-4DF39876A45A|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceTypes
&InstanceTypeFamily=ecs.g6
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeInstanceTypesResponse>
      <RequestId>00827261-20B7-4562-83F2-4DF39876A45A</RequestId>
      <InstanceTypes>
            <InstanceType>
                  <MemorySize>8</MemorySize>
                  <InstancePpsTx>300000</InstancePpsTx>
                  <MaximumQueueNumberPerEni>2</MaximumQueueNumberPerEni>
                  <EniIpv6AddressQuantity>1</EniIpv6AddressQuantity>
                  <PrimaryEniQueueNumber>2</PrimaryEniQueueNumber>
                  <CpuCoreCount>2</CpuCoreCount>
                  <TotalEniQueueQuantity>4</TotalEniQueueQuantity>
                  <EniTotalQuantity>2</EniTotalQuantity>
                  <EniTrunkSupported>false</EniTrunkSupported>
                  <InstanceTypeFamily>ecs.g6</InstanceTypeFamily>
                  <InstancePpsRx>300000</InstancePpsRx>
                  <EniQuantity>2</EniQuantity>
                  <InstanceBandwidthRx>1024000</InstanceBandwidthRx>
                  <GPUAmount>0</GPUAmount>
                  <InstanceBandwidthTx>1024000</InstanceBandwidthTx>
                  <SecondaryEniQueueNumber>2</SecondaryEniQueueNumber>
                  <DiskQuantity>17</DiskQuantity>
                  <LocalStorageCategory></LocalStorageCategory>
                  <GPUSpec></GPUSpec>
                  <InstanceFamilyLevel>EnterpriseLevel</InstanceFamilyLevel>
                  <InstanceTypeId>ecs.g6.large</InstanceTypeId>
                  <EniPrivateIpAddressQuantity>6</EniPrivateIpAddressQuantity>
            </InstanceType>
      </InstanceTypes>
</DescribeInstanceTypesResponse>
```

`JSON` format

```
{
	"RequestId": "00827261-20B7-4562-83F2-4DF39876A45A",
	"InstanceTypes": {
		"InstanceType": [
			{
				"MemorySize": 8,
				"InstancePpsTx": 300000,
				"MaximumQueueNumberPerEni": 2,
				"EniIpv6AddressQuantity": 1,
				"PrimaryEniQueueNumber": 2,
				"CpuCoreCount": 2,
				"TotalEniQueueQuantity": 4,
				"EniTotalQuantity": 2,
				"EniTrunkSupported": false,
				"InstanceTypeFamily": "ecs.g6",
				"InstancePpsRx": 300000,
				"EniQuantity": 2,
				"InstanceBandwidthRx": 1024000,
				"GPUAmount": 0,
				"InstanceBandwidthTx": 1024000,
				"SecondaryEniQueueNumber": 2,
				"DiskQuantity": 17,
				"LocalStorageCategory": "",
				"GPUSpec": "",
				"InstanceFamilyLevel": "EnterpriseLevel",
				"InstanceTypeId": "ecs.g6.large",
				"EniPrivateIpAddressQuantity": 6
			}
		]
	}
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

