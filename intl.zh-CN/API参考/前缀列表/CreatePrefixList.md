# CreatePrefixList

调用CreatePrefixList创建一个前缀列表。

## 接口说明

-   前缀列表是一些网络前缀（即CIDR地址块）的集合，您可以在配置其他资源的网络规则时引用前缀列表。关于前缀列表的详细说明，请参见[前缀列表概述](~~206223~~)。
-   当前仅部分地域支持使用前缀列表功能。
-   创建前缀列表时：
    -   您必须为该前缀列表指定地址族（IPv4或IPv6），同一前缀列表中的条目只能属于同一地址族，且地址族创建后不能修改。
    -   您必须为该前缀列表设置最大条目容量，且创建后不能修改。
    -   您可以为该前缀列表指定一些条目，条目由CIDR地址块和描述构成，条目数量不能超过您设置的最大条目容量。
-   关于前缀列表及其他资源的使用限制说明，请参见[使用限制](~~25412~~)。
-   通过RAM用户可以让您避免与其他用户共享阿里云账号密钥，按需为用户分配最小权限，从而降低企业的信息安全风险。关于如何为RAM用户授予前缀列表相关权限的具体操作，请参见[为RAM用户授予前缀列表相关权限](~~206175~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreatePrefixList&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreatePrefixList|系统规定参数。取值：CreatePrefixList |
|RegionId|String|是|cn-chengdu|地域ID。 |
|AddressFamily|String|是|IPv4|前缀列表的地址族。取值范围：

 -   IPv4
-   IPv6 |
|MaxEntries|Integer|是|10|前缀列表支持的最大条目容量。取值范围：1~200 |
|Entry.N.Cidr|String|是|192.168.1.0/24|前缀列表条目的CIDR地址块信息。N的取值范围：0~200。注意事项：

 -   前缀列表的条目数量不能大于最大条目容量（`MaxEntries`）。
-   条目中的CIDR地址块类型根据地址族决定，一个前缀列表不能同时包含IPv4和IPv6的CIDR地址块。
-   多个条目中的CIDR地址块不能重复。例如，您不能设置两个192.168.1.0/24。
-   支持设置单IP地址，系统会自动转换为CIDR地址块。例如，您设置192.168.1.100，系统会自动转换成192.168.1.100/32。
-   如果使用IPv6 CIDR地址块，系统会自动转换成零压缩表示形式且字母转换为小写。例如，您设置2001:0DB8:0000:0000:0000:0000:0000:0000/32，系统会自动转换成2001:db8::/32。

 关于CIDR地址块的详细信息，请参见[什么是CIDR](https://www.alibabacloud.com/help/doc-detail/40637.htm#title-gu4-uzk-12r)。

 默认值：空 |
|PrefixListName|String|是|PrefixListNameSample|前缀列表的名称。长度为2~128个字符，必须以大小字母或中文开头，不能以`http://`、`https://`、`com.aliyun`和`com.alibabacloud`开头。可以包含中文、英文、数字、半角冒号（:）、下划线（\_）、点号（.）或者短划线（-）。 |
|Entry.N.Description|String|否|Description Sample 01|前缀列表条目的描述信息。长度为2~32个英文或中文字符，不能以`http://`和`https://`开头。N的取值范围：0~200。 |
|ClientToken|String|否|0c593ea1-3bea-11e9-b96b-88e9fe637760|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。`ClientToken`只支持ASCII字符，且不能超过64个字符。更多信息，请参见[如何保证幂等性](~~25693~~)。 |
|Description|String|否|This is description.|前缀列表的描述信息。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|38793DB8-A4B2-4AEC-BFD3-111234E9188D|请求ID。 |
|PrefixListId|String|pl-x1j1k5ykzqlixdcy\*\*\*\*|前缀列表ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreatePrefixList
&RegionId=cn-chengdu
&AddressFamily=IPv4
&MaxEntries=20
&Entry.1.Cidr=192.168.1.0/24
&Entry.1.Description=Description Sample 01
&PrefixListName=PrefixListNameSample
&Description=This is description.
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreatePrefixListResponse>
      <RequestId>38793DB8-A4B2-4AEC-BFD3-111234E9188D</RequestId>
      <PrefixListId>pl-x1j1k5ykzqlixdcy****</PrefixListId>
</CreatePrefixListResponse>
```

`JSON`格式

```
{
  "RequestId": "38793DB8-A4B2-4AEC-BFD3-111234E9188D",
  "PrefixListId": "pl-x1j1k5ykzqlixdcy****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|%s|缺失参数，请检查参数是否完整。|
|400|InvalidParameter.AddressFamily|The parameter AddressFamily should be IPv4 or IPv6.|地址族应为IPv4或IPv6。|
|400|InvalidParameter|%s|无效的参数。|
|400|InvalidParameter.PrefixListName|The parameter PrefixListName is not valid.|前缀列表名称不合法。|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|指定的ClientToken不合法。|
|400|InvalidParameter.CidrMalformed|%s|指定的CIDR地址块不合法。|
|400|InvalidParameter.CidrDuplicated|%s|指定的CIDR地址块重复。|
|400|LimitExceed.Entry|The number of entries added or removed exceeds the limit.|单次增加或删除的条目数量超出限制。|
|400|LimitExceed.MaxEntries|The number of entries exceeds the MaxEntries of the specified prefix list.|条目数量超出指定前缀列表支持的最大条目数。|
|404|NotSupported.GrayFunction|The prefix list is a gray-scale function, not currently supported.|前缀列表功能正在邀测中，暂不支持本次操作。|
|404|LimitExceed.PrefixListPerRegion|The number of prefix lists in the region exceeds the limit.|在当前地域下的前缀列表数量超出限制。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

