# DescribeCommands

You can call this operation to query the Cloud Assistant commands that you have created. If you specify only the Action and RegionId parameters, all available commands are queried.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeCommands&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeCommands|The operation that you want to perform. Set the value to DescribeCommands. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the command. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|CommandId|String|No|c-7d2a745b412b4601b2d47f6a768d\*\*\*\*|The ID of the command. |
|Name|String|No|testName|The name of the command. Partial command names are not supported. |
|Description|String|No|testDescription|The description of the command. |
|Type|String|No|RunShellScript|The command type. Valid values:

-   RunBatScript: batch commands for Windows instances.
-   RunPowerShellScript: PowerShell commands for Windows instances.
-   RunShellScript: shell commands for Linux instances. |
|ContentEncoding|String|No|PlainText|The encoding method of the `CommandContent` and `Output` response parameters. Valid values:

-   PlainText: returns the original command content and command output.
-   Base64: returns Base64-encoded command content and command output.

Default value: Base64. |
|PageNumber|Long|No|1|The number of the page to return. Pages start from page 1.

Default value: 1. |
|PageSize|Long|No|10|The number of entries to return on each page. Maximum value: 50.

Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Commands|Array| |Details about the commands. |
|Command| | | |
|CommandContent|String|Y2QgL3Jvb3Q=|The Base64-encoded command content. |
|CommandId|String|c-7d2a745b412b4601b2d47f6a768d\*\*\*\*|The ID of the command. |
|CreationTime|String|2018-01-05T15:45:02Z|The time when the command was created. |
|Description|String|testDescription|The description of the command. |
|EnableParameter|Boolean|true|Indicates whether the custom parameter feature was enabled for the command. |
|InvokeTimes|Integer|3|The number of tasks created by running the command. |
|Name|String|testName|The name of the command. |
|ParameterNames|List|\['parameter1','parameter2'\]|A list of custom parameter names which are parsed from the command content specified when the command was being created. If the custom parameter feature is not enabled, an empty list is returned. |
|Timeout|Long|3600|The timeout duration. |
|Type|String|RunShellScript|The type of the command. |
|WorkingDir|String|/home/|The directory path for command execution. |
|PageNumber|Long|1|The page number of the returned page. |
|PageSize|Long|10|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Long|5|The total number of commands. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeCommands
&RegionId=cn-hangzhou
&CommandId=c-7d2a745b412b4601b2d47f6a768d****
&PageNumber=1
&PageSize=10
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeCommandsResponse>
      <TotalCount>5</TotalCount>
      <Commands>
            <Command>
                  <Name>testName</Name>
                  <WorkingDir></WorkingDir>
                  <CommandContent>ZWNobyAxMjM=</CommandContent>
                  <Timeout>3600</Timeout>
                  <Type>RunShellScript</Type>
                  <CommandId>c-7d2a745b412b4601b2d47f6a768d****</CommandId>
                  <Description>testDescription</Description>
                  <EnableParameter>false</EnableParameter>
            </Command>
            <Command>
                  <Name>Test1</Name>
                  <WorkingDir></WorkingDir>
                  <CommandContent>Y2QgL3Jvb3Q=</CommandContent>
                  <Timeout>3600</Timeout>
                  <Type>RunShellScript</Type>
                  <CommandId>c-7d2a745b412b4601b2d47f6a768d****</CommandId>
                  <Description>test1</Description>
                  <EnableParameter>false</EnableParameter>
            </Command>
            <Command>
                  <Name>Test2</Name>
                  <WorkingDir></WorkingDir>
                  <CommandContent>eXVtIHVwZGF0ZQ==</CommandContent>
                  <Timeout>3600</Timeout>
                  <Type>RunShellScript</Type>
                  <CommandId>c-7d2a745b412b4601b2d47f6a768d****</CommandId>
                  <Description>test2</Description>
            </Command>
            <Command>
                  <Name>Test3</Name>
                  <WorkingDir></WorkingDir>
                  <CommandContent>c2VydmljZSBuZ2lueCByZWxvYWQ=</CommandContent>
                  <Timeout>3600</Timeout>
                  <Type>RunShellScript</Type>
                  <CommandId>c-7d2a745b412b4601b2d47f6a768d****</CommandId>
                  <Description>test3</Description>
                  <EnableParameter>false</EnableParameter>
            </Command>
            <Command>
                  <Name>Test4</Name>
                  <WorkingDir></WorkingDir>
                  <CommandContent>ZWNobyB7e25hbWV9fSA=</CommandContent>
                  <Timeout>3600</Timeout>
                  <Type>RunShellScript</Type>
                  <CommandId>c-7d2a745b412b4601b2d47f6a768d****</CommandId>
                  <Description>test4</Description>
                  <EnableParameter>true</EnableParameter>
                  <ParameterNames>name</ParameterNames>
            </Command>
      </Commands>
      <PageNumber>1</PageNumber>
      <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
      <PageSize>10</PageSize>
</DescribeCommandsResponse>
```

`JSON` format

```
{
    "TotalCount": 5,
    "Commands": {
        "Command": [
            {
                "Name": "testName",
                "WorkingDir": "",
                "CommandContent": "ZWNobyAxMjM=",
                "Timeout": 3600,
                "Type": "RunShellScript",
                "CommandId": "c-7d2a745b412b4601b2d47f6a768d****",
                "Description": "testDescription",
                "EnableParameter": false,
                "ParameterNames": []
            },
            {
                "Name": "Test1",
                "WorkingDir": "",
                "CommandContent": "Y2QgL3Jvb3Q=",
                "Timeout": 3600,
                "Type": "RunShellScript",
                "CommandId": "c-7d2a745b412b4601b2d47f6a768d****",
                "Description": "test1",
                "EnableParameter": false,
                "ParameterNames": []
            },
            {
                "Name": "Test2",
                "WorkingDir": "",
                "CommandContent": "eXVtIHVwZGF0ZQ==",
                "Timeout": 3600,
                "Type": "RunShellScript",
                "CommandId": "c-7d2a745b412b4601b2d47f6a768d****",
                "Description": "test2"
            },
            {
                "Name": "Test3",
                "WorkingDir": "",
                "CommandContent": "c2VydmljZSBuZ2lueCByZWxvYWQ=",
                "Timeout": 3600,
                "Type": "RunShellScript",
                "CommandId": "c-7d2a745b412b4601b2d47f6a768d****",
                "Description": "test3",
                "EnableParameter": false,
                "ParameterNames": []
            },
            {
                "Name": "Test4",
                "WorkingDir": "",
                "CommandContent": "ZWNobyB7e25hbWV9fSA=",
                "Timeout": 3600,
                "Type": "RunShellScript",
                "CommandId": "c-7d2a745b412b4601b2d47f6a768d****",
                "Description": "test4",
                "EnableParameter": true,
                "ParameterNames": [
                    "name"
                ]
            }
        ]
    },
    "PageNumber": 1,
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "PageSize": 10
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was sent. Try again later.|
|403|InvalidParam.PageNumber|The specified parameter is invalid.|The error message returned because the specified PageNumber parameter is invalid.|
|403|InvalidParam.PageSize|The specified parameter is invalid.|The error message returned because the specified PageSize parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

