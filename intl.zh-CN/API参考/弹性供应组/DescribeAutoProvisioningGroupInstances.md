# DescribeAutoProvisioningGroupInstances

调用DescribeAutoProvisioningGroupInstances查询一个弹性供应组内的实例。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeAutoProvisioningGroupInstances&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeAutoProvisioningGroupInstances|系统规定参数。取值：DescribeAutoProvisioningGroupInstances |
|AutoProvisioningGroupId|String|是|apg-uf6jel2bbl62wh13\*\*\*\*|弹性供应组的ID。 |
|RegionId|String|是|cn-hangzhou|弹性供应组所在地域的ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|PageNumber|Integer|否|1|分页查询列表的页码。

 起始值：1

 默认值：1 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。

 最大值：100

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Instances|Array of Instance| |弹性供应组下所有实例的信息。 |
|Instance| | | |
|CPU|Integer|2|实例的vCPU核数。 |
|CreationTime|String|2017-12-10T04:04Z|实例创建时间。 |
|InstanceId|String|i-bp67acfmxazb4p\*\*\*\*|实例ID。 |
|InstanceType|String|ecs.g5.large|实例规格。 |
|IoOptimized|Boolean|true|是否为I/O优化型实例。 |
|IsSpot|Boolean|true|是否为抢占式实例。 |
|Memory|Integer|1024|内存大小，单位MiB。 |
|NetworkType|String|vpc|实例的网络类型，取值范围：

 -   vpc：专有网络
-   classic：经典网络 |
|OsType|String|linux|实例的操作系统类型，取值范围：

 -   windows：操作系统类型为Windows。
-   linux：操作系统类型为Linux。 |
|RegionId|String|cn-hangzhou|实例所属地域的ID。 |
|Status|String|Running|实例状态。 |
|ZoneId|String|cn-hangzhou-g|实例所属可用区。 |
|PageNumber|Integer|1|页码。 |
|PageSize|Integer|10|每页行数。 |
|RequestId|String|B48A12CD-1295-4A38-A8F0-0E92C937\*\*\*\*|请求ID。 |
|TotalCount|Integer|2|查询到的弹性供应组内实例的个数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeAutoProvisioningGroupInstances
&AutoProvisioningGroupId=apg-uf6jel2bbl62wh13****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeAutoProvisioningGroupInstancesResponse>
      <PageNumber>1</PageNumber>
      <TotalCount>2</TotalCount>
      <PageSize>2</PageSize>
      <RequestId>A43735F7-30BD-4D89-AB8A-030EB24B****</RequestId>
      <Instances>
            <Instance>
                  <CreationTime>2019-06-17T15:25Z</CreationTime>
                  <IoOptimized>true</IoOptimized>
                  <OsType>linux</OsType>
                  <NetworkType>vpc</NetworkType>
                  <Status>Running</Status>
                  <Memory>8192</Memory>
                  <RegionId>cn-shanghai</RegionId>
                  <InstanceId>i-bp67acfmxazb4p****</InstanceId>
                  <CPU>2</CPU>
                  <ZoneId>cn-shanghai-a</ZoneId>
                  <InstanceType>ecs.g5.large</InstanceType>
            </Instance>
            <Instance>
                  <CreationTime>2019-06-17T15:25Z</CreationTime>
                  <IoOptimized>true</IoOptimized>
                  <OsType>linux</OsType>
                  <NetworkType>vpc</NetworkType>
                  <Status>Running</Status>
                  <Memory>8192</Memory>
                  <RegionId>cn-shanghai</RegionId>
                  <InstanceId>i-bp67acfmxazb5p****</InstanceId>
                  <CPU>2</CPU>
                  <ZoneId>cn-shanghai-a</ZoneId>
                  <InstanceType>ecs.g5.large</InstanceType>
            </Instance>
      </Instances>
</DescribeAutoProvisioningGroupInstancesResponse>
```

`JSON`格式

```
{
    "PageNumber": 1,
    "TotalCount": 2,
    "PageSize": 2,
    "RequestId": "A43735F7-30BD-4D89-AB8A-030EB24B****",
    "Instances": {
        "Instance": [
            {
                "CreationTime": "2019-06-17T15:25Z",
                "IoOptimized": true,
                "OsType": "linux",
                "NetworkType": "vpc",
                "Status": "Running",
                "Memory": 8192,
                "RegionId": "cn-shanghai",
                "InstanceId": "i-bp67acfmxazb4p****",
                "CPU": 2,
                "ZoneId": "cn-shanghai-a",
                "InstanceType": "ecs.g5.large"
            },
            {
                "CreationTime": "2019-06-17T15:25Z",
                "IoOptimized": true,
                "OsType": "linux",
                "NetworkType": "vpc",
                "Status": "Running",
                "Memory": 8192,
                "RegionId": "cn-shanghai",
                "InstanceId": "i-bp67acfmxazb5p****",
                "CPU": 2,
                "ZoneId": "cn-shanghai-a",
                "InstanceType": "ecs.g5.large"
            }
        ]
    }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn't support RAM.|您没有操作此资源的权限，或者此 API 不支持 RAM 角色。|
|400|MissingParamter.RegionId|The regionId should not be null.|参数RegionId不得为空。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

