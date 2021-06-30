# DescribeInstanceMonitorData

调用DescribeInstanceMonitorData查询一台ECS实例的监控信息。可查询的指标包括ECS实例的vCPU使用率、突发性能实例积分、接收的数据流量、发送的数据流量、平均带宽等。

## 接口说明

调用该接口时，您需要注意：

-   每次最多返回400条监控数据，如果指定的参数`(EndTime - StartTime)/Period`大于400时，则返回错误信息。
-   单次最多能查询近30天内的监控信息，如果指定的参数`StartTime`超过30天，则返回错误信息。
-   当返回信息中缺少部分内容时，可能是系统没有获取到相应的信息。例如，当时实例处于已停止（Stopped）状态。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceMonitorData&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeInstanceMonitorData|系统规定参数。取值：**DescribeInstanceMonitorData**。 |
|InstanceId|String|是|i-bp1a36962lrhj4ab\*\*\*\*|待查询的实例ID。 |
|StartTime|String|是|2014-10-29T23:00:00Z|获取数据的起始时间点。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。如果指定的秒（`ss`）不是`00`，则自动换算为下一分钟。 |
|EndTime|String|是|2014-10-30T08:00:00Z|获取数据的结束时间点。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。如果指定的秒（`ss`）不是`00`，则自动换算为下一分钟。 |
|Period|Integer|否|60|获取监控数据的间隔时间，单位：秒。取值范围：

 -   60
-   600
-   3600

 默认值：60 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|MonitorData|Array of InstanceMonitorData| |实例的监控数据集合。 |
|InstanceMonitorData| | | |
|CPUCreditBalance|Float|120|突发性能实例积分总数。 |
|BPSRead|Integer|1000|实例云盘（包括系统盘和数据盘）的读带宽，单位：Byte/s。 |
|InternetTX|Integer|343|在查询监控信息时（`TimeStamp`），实例在指定的间隔时间（`Period`）内发送的公网数据流量。单位：kbits。 |
|CPU|Integer|2|实例vCPU的使用比例，单位：百分比（%）。 |
|CPUCreditUsage|Float|30|突发性能实例已使用的积分数。 |
|IOPSWrite|Integer|200|实例云盘（包括系统盘和数据盘）的I/O写操作，单位：次/s。 |
|IntranetTX|Integer|343|在查询监控信息时（`TimeStamp`），实例在指定的间隔时间（`Period`）内发送的内网数据流量。单位：kbits。 |
|InstanceId|String|i-bp1a36962lrhj4\*\*\*\*|实例ID。 |
|BPSWrite|Integer|13585|实例云盘（包括系统盘和数据盘）的写带宽，单位：Byte/s。 |
|CPUNotpaidSurplusCreditUsage|Float|0.5|超额未支付积分。 |
|CPUAdvanceCreditBalance|Float|0.4|超额积分（突发性能实例积分超限部分）。 |
|IOPSRead|Integer|1000|实例云盘（包括系统盘和数据盘）的I/O读操作，单位：次/s。 |
|InternetBandwidth|Integer|10|实例的公网带宽，单位时间内的网络流量，单位：kbits/s。 |
|InternetRX|Integer|122|在查询监控信息时（`TimeStamp`），实例在指定的间隔时间（`Period`）内接收的公网数据流量。单位：kbits。 |
|TimeStamp|String|2014-10-30T05:00:00Z|查询监控信息的时间戳。 |
|IntranetRX|Integer|122|在查询监控信息时（`TimeStamp`），实例在指定的间隔时间（`Period`）内接收的内网数据流量。单位：kbits。 |
|IntranetBandwidth|Integer|10|实例的内网带宽，单位时间内的网络流量，单位：kbits/s。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceMonitorData
&EndTime=2014-10-30T08:00:00Z
&InstanceId=i-bp1a36962lrhj4ab****
&StartTime=2014-10-29T23:00:00Z
&Period=3600
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeInstanceMonitorDataResponse>
    <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
    <MonitorData>
        <InstanceMonitorData>
            <InstanceId>i-bp1a36962lrhj4ab****</InstanceId>
            <CPU>2</CPU>
            <IntranetRX>122</IntranetRX>
            <IntranetTX>343</IntranetTX>
            <IntranetFlow>675</IntranetFlow>
            <IntranetBandwidth>10</IntranetBandwidth>
            <InternetRX>122</InternetRX>
            <InternetTX>343</InternetTX>
            <InternetFlow>675</InternetFlow>
            <InternetBandwidth>10</InternetBandwidth>
            <IOPSRead>1000</IOPSRead>
            <IOPSWrite>200</IOPSWrite>
            <BPSRead>1000</BPSRead>
            <BPSWrite>13585</BPSWrite>
            <TimeStamp>2014-10-30T05:00:00Z</TimeStamp>
        </InstanceMonitorData>
    </MonitorData>
</DescribeInstanceMonitorDataResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "C8B26B44-0189-443E-9816-D951F59623A9",
  "MonitorData" : {
    "InstanceMonitorData" : [ {
      "InstanceId" : "i-bp1a36962lrhj4ab****",
      "CPU" : 0,
      "IntranetRX" : 122,
      "IntranetTX" : 343,
      "IntranetFlow" : 675,
      "IntranetBandwidth" : 10,
      "InternetRX" : 122,
      "InternetTX" : 343,
      "InternetFlow" : 675,
      "InternetBandwidth" : 10,
      "IOPSRead" : 1000,
      "IOPSWrite" : 13585,
      "BPSRead" : 1000,
      "BPSWrite" : 200,
      "TimeStamp" : "2014-10-30T05:00:00Z"
    } ]
  }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidStartTime.Malformed|The specified parameter "StartTime" is not valid.|指定的开始时间格式不合法。|
|400|InvalidEndTime.Malformed|The specified parameter "EndTime" is not valid.|指定的结束时间格式不合法。|
|400|InvalidPeriod.ValueNotSupported|The specified parameter "Period" is not valid.|指定的Period参数不合法。|
|400|InvalidStartTime.TooEarly|The specified parameter "StartTime" is too early.|指定的开始时间太早。|
|400|InvalidParameter.TooManyDataQueried|Too many data queried.|监控数据节点超出范围。|
|400|Throttling|Request was denied due to request throttling.|当前的操作太过频繁，请稍后重试。|
|400|InvalidStartTime.ValueNotSupported|The specified parameter StartTime is later than EndTime.|结束时间不能早于开始时间。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

