# ReportInstancesStatus

调用ReportInstancesStatus反馈一台或者多台ECS实例的异常问题。您可以反馈多台ECS实例发生的相同问题，也可以反馈一台ECS实例的多块磁盘发生的相同问题。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ReportInstancesStatus&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ReportInstancesStatus|系统规定参数。取值：ReportInstancesStatus |
|InstanceId.N|RepeatList|是|i-bp165p6xk2tmdhj0\*\*\*\*|一台或者多台ECS实例ID。N的取值范围：1~100，多个取值使用重复列表的形式。 |
|RegionId|String|是|cn-hangzhou|实例所在地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Description|String|是|本地盘不可用，挂载点拒绝访问，无法加载文件。|异常问题的详细描述。 |
|Reason|String|否|abnormal-local-disk|异常问题对ECS实例造成的影响。取值范围：

 -   instance-hang：ECS实例不可用，或无法连接。
-   instance-stuck-in-status：ECS实例长时间停留在某一个状态，如Starting或Stopping状态。
-   abnormal-network：ECS实例发生网络异常。
-   abnormal-local-disk：ECS实例挂载的本地盘出现异常。
-   abnormal-cloud-disk：ECS实例挂载的云盘或共享块存储出现异常。
-   others：其他异常类型。当以上影响类型不符合条件时，您可以设置`Reason=others`并在`Description`中描述更多信息。 |
|IssueCategory|String|否|hardware-cpu-error|异常问题的类别。该参数仅适用于弹性裸金属服务器实例。取值范围：

 -   hardware-cpu-error：CPU故障
-   hardware-motherboard-error：主板故障
-   hardware-mem-error：内存故障
-   hardware-power-error：电源故障
-   hardware-disk-error：磁盘故障
-   hardware-networkcard-error：网卡故障
-   hardware-raidcard-error：SAS/RAID卡故障
-   hardware-fan-error：风扇故障
-   others：其他 |
|DiskId.N|RepeatList|否|d-bp1aeljlfad7x6u1\*\*\*\*|发生相同异常问题的一块或者多块磁盘ID。如果您使用的是弹性裸金属服务器实例，请填写磁盘设备对应的SN列表。

 N的取值范围：1~100，多个取值使用重复列表的形式。

 **说明：** 当参数`Reason`值为`abnormal-local-disk`或`abnormal-cloud-disk`，或者参数`IssueCategory`值为`hardware-disk-error`时，该参数为必填参数。 |
|Device.N|RepeatList|否|/dev/xvdb|发生相同异常问题的一块或多块磁盘的挂载的设备名列表。如果您使用的是弹性裸金属服务器实例，请填写磁盘设备对应SLOT槽位信息列表。

 N的取值范围：1~100，多个取值使用重复列表的形式。

 **说明：** 对于弹性裸金属服务器实例，当参数`Reason`值为`abnormal-local-disk`或`abnormal-cloud-disk`，或者参数`IssueCategory`值为`hardware-disk-error`时，该参数为必填参数。 |
|StartTime|String|否|2017-11-30T06:32:31Z|实例异常问题开始时间。按照ISO8601标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|EndTime|String|否|2017-11-31T06:32:31Z|实例异常问题结束时间。按照ISO8601标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ReportInstancesStatus
&InstanceId.1=i-bp165p6xk2tmdhj0****
&Reason=abnormal-local-disk
&DiskId.1=d-bp1aeljlfad7x6u1****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ReportInstancesStatusResponse>
    <RequestId>4DD56CA6-6D75-4D33-BE34-E4A44EBE1C3D</RequestId>
</ReportInstancesStatusResponse>
```

`JSON` 格式

```
{
	"RequestId":"4DD56CA6-6D75-4D33-BE34-E4A44EBE1C3D"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|MissingParameter|%s|缺失参数，请检查参数是否完整。|
|403|InvalidParameter|%s|无效的参数。|
|403|InstanceIdLimitExceeded|%s|指定的InstanceId个数不能超过100个。|
|403|DiskIdLimitExceeded|%s|指定的DiskId个数不能超过100个。|
|403|InvalidInstanceId.NotFound|%s|指定的实例不存在，请确认参数InstanceId是否正确。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

