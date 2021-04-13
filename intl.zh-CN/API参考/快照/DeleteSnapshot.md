# DeleteSnapshot

调用DeleteSnapshot删除指定的快照。如果需要取消正在创建的快照，也可以调用该接口删除快照，即取消创建快照任务。

## 接口说明

调用该接口时，您需要注意：

-   如果指定的快照ID不存在，请求将被忽略。
-   如果快照已经被用于创建自定义镜像，将不能执行删除操作。您需要先删除已创建的自定义镜像（[DeleteImage](~~25537~~)），才能继续删除快照。
-   如果快照已经被用于创建云盘，将不能执行删除操作。如果您确定要删除快照，请设置`Force=true`进行强制删除，快照被强制删除后对应的云盘将不能执行重新初始化。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DeleteSnapshot&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteSnapshot|系统规定参数。取值：DeleteSnapshot |
|SnapshotId|String|是|s-bp1c0doj0taqyzzl\*\*\*\*|快照ID。 |
|Force|Boolean|否|false|是否强制删除已经被用于创建云盘的快照。取值范围：

 -   true：强制删除。强制删除后该磁盘无法重新初始化。
-   false：不强制删除。

 默认值：false |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DeleteSnapshot
&SnapshotId=s-bp1c0doj0taqyzzl****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeleteSnapshotResponse>
       <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</DeleteSnapshotResponse>
```

`JSON`格式

```
{
    "RequestId": "CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|SnapshotCreatedImage|The snapshot has been used to create user defined image\(s\).|如果快照已经被用于创建自定义镜像，将不能执行删除操作。您需要先删除已创建的自定义镜像（DeleteImage），才能继续删除快照。|
|403|SnapshotCreatedDisk|The snapshot has been used to create disk\(s\).|指定的快照已经用于创建云盘，将不能执行删除操作。如果您确定要删除快照，请设置Force参数值为true进行强制删除，快照被强制删除后对应的云盘将不能执行重新初始化。|
|400|MissingParameter|The input parameter SnapshotId that is mandatory for processing this request is not supplied.|参数SnapshotId不得为空。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|404|InvalidSnapshotId.NotFound|The specified snapshot is not found|指定的快照不存在。|
|403|Operation.Conflict|The operation may conflicts with others, please retry later.|您当前的操作可能与其他人的操作产生了冲突，请稍后重试。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

