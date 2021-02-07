# ConvertNatPublicIpToEip

调用ConvertNatPublicIpToEip将一台专有网络VPC类型ECS实例的公网IP地址（PublicIP）转化为弹性公网IP（EIP）。

## 接口说明

公网IP地址转换为EIP后，EIP将单独计费。请确保您已充分了解[EIP的计费方式](~~122035~~)。

调用该接口时，ECS实例必须满足以下条件：

-   状态为**已停止**（`Stopped`）或者**运行中**（`Running`）。
-   没有绑定EIP。
-   没有未生效的变更配置任务。
-   公网带宽不能为0 Mbit/s。
-   公网带宽采用按使用流量计费。
-   专有网络VPC类型的包年包月ECS实例24小时内不会到期。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ConvertNatPublicIpToEip&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ConvertNatPublicIpToEip|系统规定参数。取值：ConvertNatPublicIpToEip |
|InstanceId|String|是|i-bp171jr36ge2ulvk\*\*\*\*|需要转化公网IP的实例ID。 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ConvertNatPublicIpToEip
&RegionId=cn-hangzhou
&InstanceId=i-bp171jr36ge2ulvk****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ConvertNatPublicIpToEipResponse>
      <RequestId>B154D309-F3E1-4AB7-BA94-FEFCA8B89001</RequestId>
</ConvertNatPublicIpToEipResponse>
```

`JSON`格式

```
{
   "RequestId":"B154D309-F3E1-4AB7-BA94-FEFCA8B89001"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidInstanceId.PlanedChange|%s|您当前的操作无效，由于您指定的实例已经预约了变更操作。|
|403|InvalidEndTime.OperateNotSupport|%s|该实例状态不支持此操作。|
|403|InvalidInstanceStatus.Released|%s|该操作无效，请检查实例状态是否正确。|
|403|IncorrectInstanceStatus|%s|当前实例的状态不支持此操作。|
|403|OperationDenied|%s|拒绝操作。|
|404|InvalidInstanceId.NotFound|%s|指定的实例不存在，请确认参数InstanceId是否正确。|
|403|InvalidInternetChargeType.ValueNotSupported|%s|暂不支持指定的网络计费方式，请确认相关参数是否正确。|
|403|MaxEIPQuotaExceeded|The number of EIP exceeds the limit per region.|EIP数量超过了当前地域可设置的最大值。|
|404|InvalidInstance.IpAddressMissing|%s|指定实例没有配置公网IP，具体信息请参见错误信息%s占位符的实际返回结果。您可以调用DescribeInstances查询指定实例的状态。|
|403|InvalidInstance.OverduePayment|%s|您现在的操作属于逾期付款，请重新创建实例或者联系客服解决。|
|403|InvalidInstance.OverduePayment|The special instance due to overdue payment,this operation is not supported.|您的账号已欠费，请充值后重试。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|Forbidden.RiskControl|This operation is forbidden by Aliyun RiskControl system.|该操作被风险控制系统禁止。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

