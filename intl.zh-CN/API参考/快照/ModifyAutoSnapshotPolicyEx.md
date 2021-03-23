# ModifyAutoSnapshotPolicyEx

调用ModifyAutoSnapshotPolicyEx修改一条自动快照策略。修改自动快照策略后，之前已应用该策略的云盘随即执行修改后的自动快照策略。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyAutoSnapshotPolicyEx&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyAutoSnapshotPolicyEx|系统规定参数。取值：ModifyAutoSnapshotPolicyEx |
|autoSnapshotPolicyId|String|是|sp-bp12m37ccmxvbmi5\*\*\*\*|目标自动快照策略ID。您可以调用[DescribeAutoSnapshotPolicyEx](~~25530~~)查看您可用的自动快照策略。 |
|regionId|String|是|cn-hangzhou|自动快照策略所在的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|autoSnapshotPolicyName|String|否|SPTestName|自动快照策略的名称。如果参数为空则代表不修改。 |
|timePoints|String|否|\["0", "1"\]|自动快照的创建时间点。使用UTC +8时间，单位为小时。取值范围：0~23，代表00:00至23:00共24个时间点，如1表示01:00。当一天内需要创建多次自动快照时，可以传入多个时间点：

 -   最多传入24个时间点。
-   多个时间点用一个格式类似`"0", "1", … "23"`的JSON数组表示，时间点之间用半角逗号（,）隔开。 |
|repeatWeekdays|String|否|\["1", "7"\]|自动快照的重复日期，单位为天，周期为星期。取值范围：1~7，如1表示周一。当一星期内需要创建多次自动快照时，可以传入多个时间点：

 -   最多传入7个时间点。
-   多个时间点用一个格式类似`"1", "2", … "7"`的JSON数组表示，时间点之间用半角逗号（,）隔开。 |
|retentionDays|Integer|否|30|自动快照的保留时间，单位为天。取值范围：

 -   -1（默认）：永久保存。
-   1~65536：指定保存天数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyAutoSnapshotPolicyEx
&autoSnapshotPolicyId=sp-bp12m37ccmxvbmi5****
&regionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyAutoSnapshotPolicyResponse>
      <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ModifyAutoSnapshotPolicyResponse>
```

`JSON`格式

```
{
    "RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|ParameterInvalid|The specified automatic snapshot policy does not exist.|指定的自动快照策略不存在，请您检查自动快照策略是否正确。|
|404|ParameterInvalid|The specified automatic snapshot policy does not exist in the region.|指定的自动快照策略不存在，请您检查自动快照策略是否正确。|
|403|ParameterInvalid|The specified RegionId parameter is invalid.|指定的地域ID无效，请您检查该地域是否正确。|
|403|ParameterInvalid|The specified RepeatWeekDays parameter is invalid.|指定的日期无效，请您检查该日期是否正确。|
|403|ParameterInvalid|The specified TimePoints parameter is invalid.|指定的时间点不合法，请您查看该时间点是否填写正确。|
|403|ParameterInvalid|The specified AutoSnapshotPolicyId is invalid.|指定的自动快照规则ID不合法。|
|403|ParameterInvalid|The specified RetentionDays parameter is invalid.|指定的保持天数不合法。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

