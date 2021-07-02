# ModifyPrefixList

调用ModifyPrefixList修改指定前缀列表的名称、描述和条目。

## 接口说明

-   指定的CIDR地址块应当为标准形式。例如，10.0.0.0/8是正确形式的CIDR地址块，而10.0.0.1/8是错误形式。更多信息，请参见[什么是CIDR](https://www.alibabacloud.com/help/doc-detail/40637.htm#section-jua-0tj-q5m)。
-   新增或删除条目时，不能指定重复的CIDR地址块。例如：
    -   对于IPv4 CIDR地址块：不能同时指定两个CIDR地址块均为10.0.0.0/8的条目；不能同时指定两个CIDR地址块分别为10.0.0.1/32和10.0.0.1的条目，这两个地址块重复。
    -   对于IPv6 CIDR地址块：不能同时指定两个条目的CIDR地址块分别为2001:fd01:0:0:0:0:0:0/32和2001:fd01::/32，这两个地址块重复。
-   新增条目的CIDR地址块不能与删除条目的CIDR地址块重复。例如，在您新增CIDR地址块为10.0.0.0/8的条目时，不能在待删除的条目中包含CIDR地址块10.0.0.0/8。
-   若您需要修改条目的描述，需要指定条目的CIDR地址块（`AddEntry.N.Cidr`）和新的描述信息（`AddEntry.N.Description`）。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyPrefixList&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyPrefixList|系统规定参数。取值：ModifyPrefixList |
|RegionId|String|是|cn-chengdu|地域ID。 |
|PrefixListId|String|是|pl-x1j1k5ykzqlixdcy\*\*\*\*|前缀列表ID。 |
|RemoveEntry.N.Cidr|String|是|192.168.1.0/24|删除的前缀列表条目的CIDR地址块信息。N的取值范围：0~200。

 删除时请您注意：

 -   不允许设置重复的CIDR地址块信息。
-   不允许与`AddEntry.N.Cidr`参数值重复。 |
|AddEntry.N.Cidr|String|是|192.168.2.0/24|添加的前缀列表条目的CIDR地址块信息。N的取值范围：0~200。

 添加时请您注意：

 -   前缀列表的条目数量，不能大于前缀列表支持的最大条目容量。您可以调用[DescribePrefixListAttributes](~~205872~~)查询指定前缀列表的最大条目容量信息。
-   不允许设置重复的CIDR地址块信息。
-   不允许与`RemoveEntry.N.Cidr`参数值重复。 |
|AddEntry.N.Description|String|否|Description Sample 01|前缀列表条目的描述信息。长度为2~32个英文或中文字符，不能以`http://`和`https://`开头。N的取值范围：0~200。 |
|PrefixListName|String|否|PrefixListNameSample|前缀列表的名称。长度为2~128个字符，必须以大小字母或中文开头，不能以`http://`、`https://`、`com.aliyun`和`com.alibabacloud`开头。可以包含中文、英文、数字、半角冒号（:）、下划线（\_）、点号（.）或者短划线（-）。 |
|Description|String|否|This is description.|前缀列表的描述信息。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|38793DB8-A4B2-4AEC-BFD3-111234E9188D|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyPrefixList
&RegionId=cn-chengdu
&PrefixListId=pl-x1j1k5ykzqlixdcy****
&RemoveEntry.1.Cidr=192.168.1.0/24
&AddEntry.1.Cidr=192.168.2.0/24
&AddEntry.1.Description=Description Sample 01
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyPrefixListResponse>
      <RequestId>38793DB8-A4B2-4AEC-BFD3-111234E9188D</RequestId>
</ModifyPrefixListResponse>
```

`JSON`格式

```
{
  "RequestId": "38793DB8-A4B2-4AEC-BFD3-111234E9188D"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|%s|缺失参数，请检查参数是否完整。|
|404|InvalidPrefixListId.NotFound|The specified prefix list was not found.|前缀列表不存在。|
|400|InvalidParameter.PrefixListName|The parameter PrefixListName is not valid.|前缀列表名称不合法。|
|400|InvalidParameter.CidrDuplicated|%s|指定的CIDR地址块重复。|
|400|InvalidParameter.CidrMalformed|%s|指定的CIDR地址块不合法。|
|400|LimitExceed.MaxEntries|The number of entries exceeds the MaxEntries of the specified prefix list.|条目数量超出指定前缀列表支持的最大条目数。|
|400|LimitExceed.Entry|The number of entries added or removed exceeds the limit.|单次增加或删除的条目数量超出限制。|
|404|NotSupported.GrayFunction|The prefix list is a gray-scale function, not currently supported.|前缀列表功能正在邀测中，暂不支持本次操作。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

