# DescribeDedicatedHosts

调用DescribeDedicatedHosts查询一台或多台专有宿主机的详细信息，包括专有宿主机的物理性能指标、机器码、使用状态和已创建的ECS实例列表等。

## 接口说明

您可以通过以下任一方式查询一台或多台专有宿主机的详细信息：

-   指定`DedicatedHostIds`查询专有宿主机的详细信息。
-   指定`DedicatedHostClusterId`查询专有宿主机集群内专有宿主机的详细信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeDedicatedHosts&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDedicatedHosts|系统规定参数。取值：DescribeDedicatedHosts |
|RegionId|String|是|cn-hangzhou|专有宿主机所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ZoneId|String|否|cn-hangzhou-g|可用区ID。 |
|DedicatedHostIds|String|否|\["dh-bp165p6xk2tlw61e\*\*\*\*", "dh-bp1f9vxmno7emy96\*\*\*\*"\]|专有宿主机ID列表。单次最多支持100个ID ，ID之间用半角逗号（,）隔开。 |
|DedicatedHostName|String|否|MyDDHTestName|专有宿主机的名称。 |
|Status|String|否|Available|专有宿主机的使用状态。取值范围：

 -   Available：可用状态。
-   UnderAssessment：故障潜伏期，专有宿主机可能会出故障。
-   PermanentFailure：永久性故障，专有宿主机不可用。

 默认值：Available |
|DedicatedHostType|String|否|ddh.g5|专有宿主机的规格类型。 |
|LockReason|String|否|financial|专有宿主机被锁定的原因。取值范围：

 -   financial：因欠费被锁定。
-   security：因安全原因被锁定。 |
|PageNumber|Integer|否|1|响应信息的页码数。

 默认值：1 |
|PageSize|Integer|否|10|响应信息的每页行数。最大值：100

 默认值：10 |
|ResourceGroupId|String|否|rg-aek3b6jzp66\*\*\*\*|专有宿主机所在资源组ID。 |
|DedicatedHostClusterId|String|否|dc-bp12wlf6am0vz9v2\*\*\*\*|专有宿主机集群ID。 |
|Tag.N.Key|String|否|TestKey|专有宿主机的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://`。 |
|Tag.N.Value|String|否|TestValue|专有宿主机的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DedicatedHosts|Array of DedicatedHost| |专有宿主机的详细信息集合。 |
|DedicatedHost| | | |
|ActionOnMaintenance|String|Migrate|当专有宿主机发生故障或者在线修复时，为其所宿实例设置迁移方案。取值范围：

 -   Migrate：迁移实例到其他物理机并重新启动实例。

默认值：Migrate（当专有宿主机上挂载云盘存储时）

-   Stop：在当前专有宿主机上停止实例，确认无法修复专有宿主机后，迁移实例到其他物理机并重新启动实例。

默认值：Stop（当专有宿主机上挂载本地盘存储时） |
|AutoPlacement|String|on|专有宿主机是否加入自动部署资源池。取值范围：

 -   on：加入自动部署资源池。
-   off：不加入自动部署资源池。

 关于自动部署的更多信息，请参见[自动部署功能介绍](~~118938~~)。 |
|AutoReleaseTime|String|2017-01-01T12:00Z|自动释放时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC+0时间，格式为`yyyy-MM-ddTHH:mmZ`。 |
|Capacity|Struct| |专有宿主机性能指标集合。 |
|AvailableLocalStorage|Integer|65|剩余的本地盘容量。单位：GiB。 |
|AvailableMemory|Float|25|剩余的内存容量，单位：GiB。 |
|AvailableVcpus|Integer|5|剩余的vCPU核数。 |
|AvailableVgpus|Integer|2|可用虚拟GPU数量。 |
|LocalStorageCategory|String|i2|本地盘类型。 |
|TotalLocalStorage|Integer|512|本地盘总容量，单位：GiB。 |
|TotalMemory|Float|1024|内存总容量，单位：GiB。 |
|TotalVcpus|Integer|56|vCPU总核数。 |
|TotalVgpus|Integer|10|总虚拟GPU数量。 |
|ChargeType|String|Prepaid|专有宿主机的计费方式。 |
|Cores|Integer|3|单个CPU的核数。 |
|CpuOverCommitRatio|Float|1|CPU超卖比。 |
|CreationTime|String|2018-01-01T12:00Z|专有宿主机的创建时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC+0时间，格式为`yyyy-MM-ddTHH:mmZ`。 |
|DedicatedHostClusterId|String|dc-bp12wlf6am0vz9v2\*\*\*\*|专有宿主机所在的专有宿主机集群ID。 |
|DedicatedHostId|String|dh-bp165p6xk2tlw61e\*\*\*\*|专有宿主机ID。 |
|DedicatedHostName|String|MyDDHTestName|专有宿主机的名称。 |
|DedicatedHostType|String|ddh.g5|专有宿主机的规格类型。 |
|Description|String|this-is-my-DDH|专有宿主机的描述信息。 |
|ExpiredTime|String|2019-01-01T12:00Z|包年包月专有宿主机的到期时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC+0时间，格式为`yyyy-MM-ddTHH:mmZ`。 |
|GPUSpec|String|gpu|GPU型号。 |
|HostDetailInfo|Struct| |该参数即将被弃用，为提高兼容性，建议您尽量使用其他参数。 |
|SerialNumber|String|null|该参数即将被弃用，为提高兼容性，建议您尽量使用其他参数。 |
|Instances|Array of Instance| |专有宿主机上创建的ECS实例。 |
|Instance| | | |
|InstanceId|String|i-bp14ot0ykf8w13a1\*\*\*\*|专有宿主机上创建的ECS实例ID。 |
|InstanceType|String|ecs.g5.large|专有宿主机上创建的ECS实例类型。 |
|MachineId|String|12aaa123456ff19dec12345d3026e\*\*\*\*|专有宿主机机器码。 |
|NetworkAttributes|Struct| |专有宿主机的网络属性值。 |
|SlbUdpTimeout|Integer|60|SLB UDP超时时间。 |
|UdpTimeout|Integer|60|UDP超时时间。 |
|OperationLocks|Array of OperationLock| |专有宿主机资源被锁定原因。 |
|OperationLock| | | |
|LockReason|String|financial|资源锁定原因。可能取值：financial（因账号欠费被锁定）。 |
|PhysicalGpus|Integer|10|物理GPU数量。 |
|RegionId|String|cn-hangzhou|专有宿主机所在地域ID。 |
|ResourceGroupId|String|rg-aek3b6jzp66\*\*\*\*|专有宿主机所在资源组ID。 |
|SaleCycle|String|Month|包年包月单位。可能值：

 -   Month
-   Year |
|Sockets|Integer|5|物理处理器（CPU）数量。 |
|Status|String|Available|专有宿主机的使用状态。可能值：

 -   Available
-   UnderAssessment
-   PermanentFailure |
|SupportedCustomInstanceTypeFamilies|List|ecs.ddh6s.custom|专有宿主机支持的自定义实例规格族。 |
|SupportedInstanceTypeFamilies|List|ecs.g5|专有宿主机支持的ECS实例规格族。 |
|SupportedInstanceTypesList|List|ecs.g5.large|专有宿主机支持的ECS实例规格。 |
|Tags|Array of Tag| |专有宿主机的标签。 |
|Tag| | | |
|TagKey|String|TestKey|专有宿主机的标签键。 |
|TagValue|String|TestValue|专有宿主机的标签值。 |
|ZoneId|String|cn-hangzhou-g|可用区ID。 |
|PageNumber|Integer|5|专有宿主机列表的页码。 |
|PageSize|Integer|1|输入时设置的每页行数。 |
|RequestId|String|7654525A-9964-4ABB-8BCD-98F8835E809A|请求ID。 |
|TotalCount|Integer|3|专有宿主机总数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeDedicatedHosts
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeDedicatedHostsResponse>
      <TotalCount>1</TotalCount>
      <DedicatedHosts>
            <DedicatedHost>
                  <PhysicalGpus>0</PhysicalGpus>
                  <MachineId>73aaa79494ff19dec79446d3026e****</MachineId>
                  <DedicatedHostId>dh-bp165p6xk2tlw61e****</DedicatedHostId>
                  <Description></Description>
                  <ResourceGroupId></ResourceGroupId>
                  <SupportedCustomInstanceTypeFamilies>
            </SupportedCustomInstanceTypeFamilies>
                  <NetworkAttributes></NetworkAttributes>
                  <GPUSpec></GPUSpec>
                  <DedicatedHostName>MyDDHTestName</DedicatedHostName>
                  <Capacity>
                        <AvailableVgpus>0</AvailableVgpus>
                        <LocalStorageCategory></LocalStorageCategory>
                        <TotalVgpus>0</TotalVgpus>
                        <TotalMemory>768</TotalMemory>
                        <AvailableMemory>768</AvailableMemory>
                        <AvailableVcpus>104</AvailableVcpus>
                        <TotalVcpus>104</TotalVcpus>
                        <AvailableLocalStorage>0</AvailableLocalStorage>
                        <TotalLocalStorage>0</TotalLocalStorage>
                  </Capacity>
                  <ExpiredTime>2999-09-08T16:00Z</ExpiredTime>
                  <SaleCycle></SaleCycle>
                  <Status>Available</Status>
                  <ZoneId>cn-hangzhou-h</ZoneId>
                  <AutoPlacement>on</AutoPlacement>
                  <DedicatedHostType>ddh.r6</DedicatedHostType>
                  <OperationLocks>
            </OperationLocks>
                  <Cores>52</Cores>
                  <Instances>
            </Instances>
                  <Sockets>2</Sockets>
                  <ChargeType>PostPaid</ChargeType>
                  <SupportedInstanceTypeFamilies>
                        <SupportedInstanceTypeFamily>ecs.c6</SupportedInstanceTypeFamily>
                        <SupportedInstanceTypeFamily>ecs.g6</SupportedInstanceTypeFamily>
                        <SupportedInstanceTypeFamily>ecs.ic6</SupportedInstanceTypeFamily>
                        <SupportedInstanceTypeFamily>ecs.r6</SupportedInstanceTypeFamily>
                  </SupportedInstanceTypeFamilies>
                  <ActionOnMaintenance>Migrate</ActionOnMaintenance>
                  <CreationTime>2020-04-15T07:12Z</CreationTime>
                  <RegionId>cn-hangzhou</RegionId>
                  <SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.g6.26xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.g6.3xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.g6.8xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.g6.2xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.g6.13xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.g6.6xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.c6.8xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.g6.4xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.g6.xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.g6.16xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.c6.13xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.c6.26xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.r6.xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.r6.26xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.r6.3xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.r6.13xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.r6.16xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.r6.4xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.c6.16xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.r6.6xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.g6.large</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.c6.2xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.r6.2xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.c6.xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.c6.3xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.c6.6xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.c6.4xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.c6.large</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.r6.large</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.r6.8xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.ic6.4xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.ic6.8xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.ic6.xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.ic6.3xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.ic6.6xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.ic6.2xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.ic6.large</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.r6-dbeni.8xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.g6nv.8xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.c6vn.8xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.r6vn.8xlarge</SupportedInstanceTypesList>
                        <SupportedInstanceTypesList>ecs.g6-nfveni.large</SupportedInstanceTypesList>
                  </SupportedInstanceTypesList>
                  <DedicatedHostClusterId></DedicatedHostClusterId>
                  <AutoReleaseTime></AutoReleaseTime>
            </DedicatedHost>
      </DedicatedHosts>
      <RequestId>9E9354D4-C89E-4A82-A70E-3EEAD6007885</RequestId>
      <PageSize>10</PageSize>
      <PageNumber>1</PageNumber>
</DescribeDedicatedHostsResponse>
```

`JSON`格式

```
{
	"TotalCount": 1,
	"DedicatedHosts": {
		"DedicatedHost": [
			{
				"PhysicalGpus": 0,
				"MachineId": "73aaa79494ff19dec79446d3026e****",
				"DedicatedHostId": "dh-bp165p6xk2tlw61e****",
				"Description": "",
				"ResourceGroupId": "",
				"SupportedCustomInstanceTypeFamilies": {
					"SupportedCustomInstanceTypeFamily": []
				},
				"NetworkAttributes": {},
				"GPUSpec": "",
				"DedicatedHostName": "MyDDHTestName",
				"Capacity": {
					"AvailableVgpus": 0,
					"LocalStorageCategory": "",
					"TotalVgpus": 0,
					"TotalMemory": 768,
					"AvailableMemory": 768,
					"AvailableVcpus": 104,
					"TotalVcpus": 104,
					"AvailableLocalStorage": 0,
					"TotalLocalStorage": 0
				},
				"ExpiredTime": "2999-09-08T16:00Z",
				"SaleCycle": "",
				"Status": "Available",
				"ZoneId": "cn-hangzhou-h",
				"AutoPlacement": "on",
				"DedicatedHostType": "ddh.r6",
				"OperationLocks": {
					"OperationLock": []
				},
				"Cores": 52,
				"Instances": {
					"Instance": []
				},
				"Sockets": 2,
				"ChargeType": "PostPaid",
				"SupportedInstanceTypeFamilies": {
					"SupportedInstanceTypeFamily": [
						"ecs.c6",
						"ecs.g6",
						"ecs.ic6",
						"ecs.r6"
					]
				},
				"ActionOnMaintenance": "Migrate",
				"CreationTime": "2020-04-15T07:12Z",
				"RegionId": "cn-hangzhou",
				"SupportedInstanceTypesList": {
					"SupportedInstanceTypesList": [
						"ecs.g6.26xlarge",
						"ecs.g6.3xlarge",
						"ecs.g6.8xlarge",
						"ecs.g6.2xlarge",
						"ecs.g6.13xlarge",
						"ecs.g6.6xlarge",
						"ecs.c6.8xlarge",
						"ecs.g6.4xlarge",
						"ecs.g6.xlarge",
						"ecs.g6.16xlarge",
						"ecs.c6.13xlarge",
						"ecs.c6.26xlarge",
						"ecs.r6.xlarge",
						"ecs.r6.26xlarge",
						"ecs.r6.3xlarge",
						"ecs.r6.13xlarge",
						"ecs.r6.16xlarge",
						"ecs.r6.4xlarge",
						"ecs.c6.16xlarge",
						"ecs.r6.6xlarge",
						"ecs.g6.large",
						"ecs.c6.2xlarge",
						"ecs.r6.2xlarge",
						"ecs.c6.xlarge",
						"ecs.c6.3xlarge",
						"ecs.c6.6xlarge",
						"ecs.c6.4xlarge",
						"ecs.c6.large",
						"ecs.r6.large",
						"ecs.r6.8xlarge",
						"ecs.ic6.4xlarge",
						"ecs.ic6.8xlarge",
						"ecs.ic6.xlarge",
						"ecs.ic6.3xlarge",
						"ecs.ic6.6xlarge",
						"ecs.ic6.2xlarge",
						"ecs.ic6.large",
						"ecs.r6-dbeni.8xlarge",
						"ecs.g6nv.8xlarge",
						"ecs.c6vn.8xlarge",
						"ecs.r6vn.8xlarge",
						"ecs.g6-nfveni.large"
					]
				},
				"DedicatedHostClusterId": "",
				"AutoReleaseTime": ""
			}
		]
	},
	"RequestId": "9E9354D4-C89E-4A82-A70E-3EEAD6007885",
	"PageSize": 10,
	"PageNumber": 1
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidStatus.ValueNotSupported|The pecified dedicated host status is not supported.|当前宿主机状态不支持此操作。|
|400|MissingParamter.RegionId|The regionId should not be null.|参数RegionId不得为空。|
|400|InvalidParameter.DedicatedHostIds|The specified parameter dedicatedHostIds is not valid.|指定的参数DedicatedHostIds无效。|
|400|InvalidRegion.NotFound|The specified parameter RegionId is not valid.|RegionId参数不合法。|
|400|InvalidZone.NotFound|The specified parameter ZoneId is not valid.|指定的ZoneId不合法。|
|403|InvalidDedicatedHostIds.Malformed|The amount of specified dedicatedHostIds exceeds the limit.|参数DedicatedHostIds中的数据最多设置100个。|
|404|InvalidLockReason.NotFound|The specified LockReason is not found|指定的锁定类型不存在。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

