# DescribeInstanceTypeFamilies

调用DescribeInstanceTypeFamilies查询云服务器ECS提供的实例规格族列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceTypeFamilies&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeInstanceTypeFamilies|系统规定参数。取值：DescribeInstanceTypeFamilies |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Generation|String|否|ecs-5|实例规格族的系列信息。更多详情，请参见[实例规格族](~~25378~~)。取值范围：

 -   ecs-1：系列I实例规格，上线时间较早，性价比高。
-   ecs-2：系列II实例规格族，第二次软硬件升级，实例性能增强。
-   ecs-3：系列III实例规格族，实例性能优良，能承载不同业务需求。
-   ecs-4：系列IV实例规格族，包含常见的企业级实例规格（g5、c5、r5等）、弹性裸金属服务器实例规格（ebmc5s、ebmg5s、ebmr5s等）、突发性能实例规格（t5）等，具有强大的场景适应性，能承载海量热门业务需求，延迟更低。
-   ecs-5：系列V实例规格族，包含常见的企业级实例规格（g6、c6、r6等）、弹性裸金属服务器实例规格（ebmg6、ebmg6e、ebmc6等）、存储增强型实例规格（g6e）等，响应更快，性能更优越。
-   ecs-6：系列VI实例规格族，包含企业级实例规格（hfc7、hfg7、hfr7等）、弹性裸金属服务器实例规格（ebmhfg7等），该系列实例规格族正在邀测中。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceTypeFamilies|Array of InstanceTypeFamily| |由实例规格族InstanceTypeFamily组成的集合。 |
|InstanceTypeFamily| | | |
|Generation|String|ecs-5|实例规格族所属代数。 |
|InstanceTypeFamilyId|String|ecs.g6|实例规格族ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceTypeFamilies
&RegionId=cn-hangzhou
&Generation=ecs-5
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeInstanceTypeFamiliesResponse>
      <InstanceTypeFamilies>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.g6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.ebmg6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.ebmg6e</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.g6e</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.c6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.r6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.t6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.hfc6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.hfg6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.hfr6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.ebmc6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.ebmr6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
      </InstanceTypeFamilies>
      <RequestId>A66D039A-EC35-4130-B0D1-E9873C0742D2</RequestId>
</DescribeInstanceTypeFamiliesResponse>
```

`JSON` 格式

```
{
	"InstanceTypeFamilies": {
		"InstanceTypeFamily": [
			{
				"InstanceTypeFamilyId": "ecs.g6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.ebmg6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.ebmg6e",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.g6e",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.c6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.r6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.t6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.hfc6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.hfg6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.hfr6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.ebmc6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.ebmr6",
				"Generation": "ecs-5"
			}
		]
	},
	"RequestId": "A66D039A-EC35-4130-B0D1-E9873C0742D2"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

