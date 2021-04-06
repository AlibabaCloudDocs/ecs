# ModifySnapshotGroup

调用ModifySnapshotGroup修改指定实例快照的名称与描述信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifySnapshotGroup&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|ModifySnapshotGroup|系统规定参数。取值：ModifySnapshotGroup |
|RegionId|String|是|cn-hangzhou|实例快照所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|SnapshotGroupId|String|是|ssg-j6ciyh3k52qp7ovm\*\*\*\*|实例快照ID。 |
|Name|String|否|testName02|修改后的实例快照名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以`http://`和`https://`开头，可以包含数字、英文句号（.）、下划线（\_）、短划线（-）或者半角冒号（:）。 |
|Description|String|否|This is new description|修改后的描述。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|A00B5E55-76B7-42C8-8A80-AF10E980DCC7|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifySnapshotGroup
&RegionId=cn-hangzhou
&SnapshotGroupId=ssg-j6ciyh3k52qp7ovm****
&Name=testName02
&Description=This is new description
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifySnapshotGroupResponse>
      <RequestId>A00B5E55-76B7-42C8-8A80-AF10E980DCC7</RequestId>
</ModifySnapshotGroupResponse>
```

`JSON`格式

```
{
	"RequestId": "A00B5E55-76B7-42C8-8A80-AF10E980DCC7"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.Name|The specified Name is invalid.|指定的Name参数无效。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

