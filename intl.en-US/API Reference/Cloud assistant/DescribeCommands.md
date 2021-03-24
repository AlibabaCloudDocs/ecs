# DescribeCommands

You can call this operation to query the Cloud Assistant commands that you created or the public Cloud Assistant commands that Alibaba Cloud provides.

## Description

If you specify only the `Action` and `RegionId` parameters, all the available commands that you created in the specified region are queried by default.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeCommands&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeCommands|The operation that you want to perform. Set the value to DescribeCommands. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the command. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Provider|String|No|AlibabaCloud|The provider of the public command.

-   If you do not specify this parameter, all the commands that you created are queried.
-   If you set this parameter to `AlibabaCloud`, all the public commands provided by Alibaba Cloud are queried.
-   If you set this parameter to a specific provider, all the public commands provided by the provider are queried. For example:
    -   If you set `Provider` to AlibabaCloud.ECS.GuestOS, all the public commands provided by `AlibabaCloud.ECS.GuestOS` are queried.
    -   If you set `Provider` to AlibabaCloud.ECS.GuestOSDiagnose, all the public commands provided by `AlibabaCloud.ECS.GuestOSDiagnose` are queried.

This parameter is empty by default. |
|CommandId|String|No|c-hz01272yr52\*\*\*\*|The ID of the command. |
|Name|String|No|testName|The name of the command. Partial command names are not supported. |
|Description|String|No|testDescription|The description of the command. |
|Type|String|No|RunShellScript|The command type. Valid values:

-   RunBatScript: batch command, applicable to Windows instances
-   RunPowerShellScript: PowerShell command, applicable to Windows instances
-   RunShellScript: shell command, applicable to Linux instances |
|ContentEncoding|String|No|PlainText|The encoding mode of the `CommandContent` and `Output` response parameters. Valid values:

-   PlainText: returns the original command content and command output.
-   Base64: returns the Base64-encoded command content and command output.

Default value: Base64. |
|PageNumber|Long|No|1|The number of the page to return. Pages start from page 1.

Default value: 1. |
|PageSize|Long|No|10|The number of entries to return on each page. Maximum value: 50.

Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Commands|Array of Command| |Details about the commands. |
|Command| | | |
|Category|String|Alibaba Cloud-ECS-instance system|The category of the public command. |
|CommandContent|String|Y2QgL3Jvb3Q=|The Base64-encoded command content. |
|CommandId|String|c-hz01272yr52\*\*\*\*|The ID of the command. |
|CreationTime|String|2020-11-17T06:52Z|The time when the command was created. |
|Description|String|testDescription|The description of the command. |
|EnableParameter|Boolean|true|Indicates whether the custom parameter feature was enabled for the command. |
|InvokeTimes|Integer|2|The number of tasks created by using the command. |
|Latest|Boolean|true|Indicates whether the public command is of the latest version. If multiple public commands of the same provider \(`Provider`\) and the same category have the same name, these commands are of different versions of the same command. This parameter is not returned for the Cloud Assistant commands that you created. |
|Name|String|testName|The name of the command. |
|ParameterNames|List|\['parameter1','parameter2'\]|A list of custom parameter names that are parsed from the command content specified when the command was being created. If the custom parameter feature is not enabled, an empty list is returned. |
|Provider|String|AlibabaCloud.ECS.GuestOS|The provider of the public command. |
|Timeout|Long|3600|The timeout period. |
|Type|String|RunShellScript|The command type. |
|Version|Integer|1|The version of the public command. If multiple public commands of the same provider \(`Provider`\) and the same category have the same name, these commands are of different versions of the same command. This parameter is not returned for the Cloud Assistant commands that you created. |
|WorkingDir|String|/home/|The working directory of the command. |
|PageNumber|Long|1|The page number of the returned page. |
|PageSize|Long|10|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Long|5|The total number of commands. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeCommands
&RegionId=cn-hangzhou
&CommandId=c-hz01272yr52****
&PageNumber=1
&PageSize=10
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeCommandsResponse>
      <TotalCount>1</TotalCount>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <PageSize>10</PageSize>
      <PageNumber>1</PageNumber>
      <Commands>
            <Command>
                  <Category></Category>
                  <Description>test1</Description>
                  <ParameterNames></ParameterNames>
                  <Timeout>3600</Timeout>
                  <Name>testName</Name>
                  <Provider></Provider>
                  <CommandContent>Y2QgL3Jvb3Q=</CommandContent>
                  <WorkingDir></WorkingDir>
                  <Type>RunShellScript</Type>
                  <InvokeTimes>2</InvokeTimes>
                  <CreationTime>2020-11-17T06:52Z</CreationTime>
                  <EnableParameter>false</EnableParameter>
                  <CommandId>c-hz01272yr52****</CommandId>
            </Command>
      </Commands>
</DescribeCommandsResponse>
```

`JSON` format

```
{
    "TotalCount": 1,
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "PageSize": 10,
    "PageNumber": 1,
    "Commands": {
        "Command": [
            {
                "Category": "",
                "Description": "test1",
                "ParameterNames": {
                    "ParameterName": []
                },
                "Timeout": 3600,
                "Name": "testName",
                "Provider": "",
                "CommandContent": "Y2QgL3Jvb3Q=",
                "WorkingDir": "",
                "Type": "RunShellScript",
                "InvokeTimes": 2,
                "CreationTime": "2020-11-17T06:52Z",
                "EnableParameter": false,
                "CommandId": "c-hz01272yr52****"
            }
        ]
    }
}
```

## Error codes

|HTTP stauts code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|RegionId.ApiNotSupported|The api is not supported in this region.|The error message returned because the API operation cannot be called in the specified region. Check whether the RegionId parameter is correct.|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred while the request was being sent. Try again later.|
|403|InvalidParam.PageNumber|The specified parameter is invalid.|The error message returned because the specified PageNumber parameter is invalid.|
|403|InvalidParam.PageSize|The specified parameter is invalid.|The error message returned because the specified PageSize parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

