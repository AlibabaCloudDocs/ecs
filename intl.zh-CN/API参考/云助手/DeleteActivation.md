# DeleteActivation

调用DeleteActivation删除一个未被使用的激活码。

## 接口说明

激活码必须未被使用，即激活码对应注册的托管实例数量为0。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DeleteActivation&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteActivation|系统规定参数。取值：DeleteActivation |
|ActivationId|String|是|4ECEEE12-56F1-4FBC-9AB1-890F1234\*\*\*\*|未被使用的激活码ID。 |
|RegionId|String|是|cn-hangzhou|地域ID。目前仅支持华东1（杭州）、华北2（北京）、华东2（上海）。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Activation|Struct| |激活码及使用情况信息组成的集合。 |
|ActivationId|String|4ECEEE12-56F1-4FBC-9AB1-890F1234\*\*\*\*|激活码ID。 |
|CreationTime|String|2021-01-20T06:00:00Z|创建时间。 |
|DeregisteredCount|Integer|0|已注销的实例数。 |
|Description|String|This is description.|激活码对应的描述。 |
|InstanceCount|Integer|1|激活码用于注册托管实例的使用次数上限。 |
|InstanceName|String|test-InstanceName|默认的实例名称前缀。 |
|IpAddressRange|String|0.0.0.0/0|允许使用该激活码的主机IP。 |
|RegisteredCount|Integer|0|已注册的实例数。 |
|TimeToLiveInHours|Long|4|激活码的有效时间。单位：小时 |
|RequestId|String|4ECEEE12-56F1-4FBC-9AB1-890F74942176|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DeleteActivation
&ActivationId=4ECEEE12-56F1-4FBC-9AB1-890F1234****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeleteActivationResponse>
      <RequestId>4ECEEE12-56F1-4FBC-9AB1-890F74942176</RequestId>
      <Activation>
            <InstanceName>test-InstanceName</InstanceName>
            <DeregisteredCount>0</DeregisteredCount>
            <InstanceCount>1</InstanceCount>
            <Description>This is description.</Description>
            <CreationTime>2021-01-20T06:00:00Z</CreationTime>
            <ActivationId>4ECEEE12-56F1-4FBC-9AB1-890F1234****</ActivationId>
            <RegisteredCount>0</RegisteredCount>
            <TimeToLiveInHours>4</TimeToLiveInHours>
            <IpAddressRange>0.0.0.0/0</IpAddressRange>
      </Activation>
</DeleteActivationResponse>
```

`JSON`格式

```
{
    "RequestId": "4ECEEE12-56F1-4FBC-9AB1-890F74942176", 
    "Activation": {
        "InstanceName": "test-InstanceName", 
        "DeregisteredCount": "0", 
        "InstanceCount": "1", 
        "Description": "This is description.", 
        "CreationTime": "2021-01-20T06:00:00Z", 
        "ActivationId": "4ECEEE12-56F1-4FBC-9AB1-890F1234****", 
        "RegisteredCount": "0", 
        "TimeToLiveInHours": "4", 
        "IpAddressRange": "0.0.0.0/0"
    }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发送请求时发生错误，请稍后重试。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

