# DescribeEniMonitorData

调用DescribeEniMonitorData查询一块辅助网卡在指定时间段内使用的流量信息。

## 接口说明

可查询的辅助网卡流量信息包括辅助网卡收发数据包的数量、内网出入流量、辅助网卡收发丢包的数量。当返回信息中缺少部分内容时，可能是由于系统没有获取到相应的信息。例如，当实例处于已停止（Stopped）状态或者辅助网卡没有挂载到实例上，即处于可用（Available）状态时，无法获取到相应的信息。调用该接口时，您需要注意：

-   每次最多返回400条监控数据，即如果指定的参数\(EndTime - StartTime\)/Peroid\>400，则返回错误。
-   单次最多能查询近30天内的监控信息，如果指定的参数StartTime超过30天，则返回错误。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeEniMonitorData&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeEniMonitorData|系统规定参数。取值：DescribeEniMonitorData |
|EndTime|String|是|2018-05-21T12:22:00Z|获取数据的结束时间点。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。如果指定的秒（ss）不是00，则自动换算为下一分钟。 |
|InstanceId|String|是|i-bp1a5zr3u7nq9cx\*\*\*\*|辅助网卡绑定的实例ID。 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|StartTime|String|是|2018-05-21T12:19:00Z|获取数据的起始时间点。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。如果指定的秒（ss）不是00，则自动换算为下一分钟。 |
|EniId|String|否|eni-bp19da36d6xdwey\*\*\*\*|辅助网卡的ID。默认查询指定实例上所有已绑定的辅助网卡。 |
|Period|Integer|否|60|获取监控数据的间隔时间，单位：秒。取值范围：

 -   60
-   600
-   3600

 默认值：60 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|MonitorData|Array of EniMonitorData| |辅助网卡流量的监控数据EniMonitorDataType组成的集合。 |
|EniMonitorData| | | |
|DropPacketRx|String|0|辅助网卡接收丢弃的内网数据包，单位：packets。 |
|DropPacketTx|String|0|辅助网卡发送丢弃的内网数据包，单位：packets。 |
|EniId|String|eni-bp19da36d6xdwey\*\*\*\*|辅助网卡ID。 |
|IntranetRx|String|0|辅助网卡接收的内网数据流量，单位：kbits。 |
|IntranetTx|String|0|辅助网卡发送的内网数据流量，单位：kbits。 |
|PacketRx|String|0|辅助网卡接收的内网数据包，单位：packets。 |
|PacketTx|String|0|辅助网卡发送的内网数据包，单位：packets。 |
|TimeStamp|String|2018-05-21T03:22:00Z|查询监控信息的时间戳。按照ISO8601标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|4|返回条目数量。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeEniMonitorData
&EndTime=2018-05-21T12:22:00Z
&InstanceId=i-bp1a5zr3u7nq9cx****
&RegionId=cn-hangzhou
&StartTime=2018-05-21T12:19:00Z
&EniId=eni-bp19da36d6xdwey****
&Period=60
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeEniMonitorDataResponse>
      <RequestId>5A03C2BA-3BCE-4A87-8076-7DC1629</RequestId>
      <MonitorData>
            <EniMonitorData>
                  <PacketTx>0</PacketTx>
                  <TimeStamp>2018-05-21T03:22:00Z</TimeStamp>
                  <IntranetOut>0</IntranetOut>
                  <DropPacketRx>0</DropPacketRx>
                  <IntranetIn>0</IntranetIn>
                  <EniId>eni-bp19da36d6xdwey4****</EniId>
                  <DropPacketTx>0</DropPacketTx>
                  <PacketRx>0</PacketRx>
            </EniMonitorData>
            <EniMonitorData>
                  <PacketTx>0</PacketTx>
                  <TimeStamp>2018-05-21T03:21:00Z</TimeStamp>
                  <IntranetOut>0</IntranetOut>
                  <DropPacketRx>0</DropPacketRx>
                  <IntranetIn>0</IntranetIn>
                  <EniId>eni-bp19da36d6xdwey3****</EniId>
                  <DropPacketTx>0</DropPacketTx>
                  <PacketRx>0</PacketRx>
            </EniMonitorData>
            <EniMonitorData>
                  <PacketTx>52240</PacketTx>
                  <TimeStamp>2018-05-21T03:19:00Z</TimeStamp>
                  <IntranetOut>73344</IntranetOut>
                  <DropPacketRx>0</DropPacketRx>
                  <IntranetIn>467</IntranetIn>
                  <EniId>eni-bp19da36d6xdwey2****</EniId>
                  <DropPacketTx>0</DropPacketTx>
                  <PacketRx>6603</PacketRx>
            </EniMonitorData>
            <EniMonitorData>
                  <PacketTx>34925</PacketTx>
                  <TimeStamp>2018-05-21T03:20:00Z</TimeStamp>
                  <IntranetOut>48871</IntranetOut>
                  <DropPacketRx>0</DropPacketRx>
                  <IntranetIn>350</IntranetIn>
                  <EniId>eni-bp19da36d6xdwey1****</EniId>
                  <DropPacketTx>0</DropPacketTx>
                  <PacketRx>4888</PacketRx>
            </EniMonitorData>
      </MonitorData>
</DescribeEniMonitorDataResponse>
```

`JSON`格式

```
{
 "RequestId":"5A03C2BA-3BCE-4A87-8076-7DC1629",
 "MonitorData":{
     "EniMonitorData":[
         {
             "PacketTx":0,
             "TimeStamp":"2018-05-21T03:22:00Z",
             "IntranetOut":0,
             "DropPacketRx":0,
             "IntranetIn":0,
             "EniId":"eni-bp19da36d6xdwey4****",
             "DropPacketTx":0,
             "PacketRx":0
         },
         {
             "PacketTx":0,
             "TimeStamp":"2018-05-21T03:21:00Z",
             "IntranetOut":0,
             "DropPacketRx":0,
             "IntranetIn":0,
             "EniId":"eni-bp19da36d6xdwey3****",
             "DropPacketTx":0,
             "PacketRx":0
         },
         {
             "PacketTx":52240,
             "TimeStamp":"2018-05-21T03:19:00Z",
             "IntranetOut":73344,
             "DropPacketRx":0,
             "IntranetIn":467,
             "EniId":"eni-bp19da36d6xdwey2****",
             "DropPacketTx":0,
             "PacketRx":6603
         },
         {
             "PacketTx":34925,
             "TimeStamp":"2018-05-21T03:20:00Z",
             "IntranetOut":48871,
             "DropPacketRx":0,
             "IntranetIn":350,
             "EniId":"eni-bp19da36d6xdwey1****",
             "DropPacketTx":0,
             "PacketRx":4888
         }
     ]
 }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDiskId.NotFound|The DiskId provided does not exist in our records.|指定的磁盘不存在。请您检查磁盘ID是否正确。|
|403|InvalidStartTime.Malformed|The specified parameter "StartTime" is not valid.|指定的开始时间格式不合法。|
|403|InvalidEndTime.Malformed|The specified parameter "EndTime" is not valid.|指定的结束时间格式不合法。|
|403|InvalidPeriod.ValueNotSupported|The specified parameter "Period" is not valid.|指定的Period参数不合法。|
|403|InvalidStartTime.TooEarly|The specified parameter "StartTime" is too early.|指定的开始时间太早。|
|403|InvalidParameter.TooManyDataQueried|Too many data queried.|监控数据节点超出范围。|
|403|Throttling|Request was denied due to request throttling.|当前的操作太过频繁，请稍后重试。|
|403|InvalidInstanceType.NotSupportCredit|The InstanceType of the specified instance does not support credit.|实例规格不支持突发性能实例。|
|403|InvalidParameter.EndTime|The specified parameter EndTime is earlier than StartTime.|结束时间不能早于开始时间。|
|4003|InvalidParam.Malformed|The specified parameter "EniId" and "InstanceId" are not valid|指定的参数无效。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

