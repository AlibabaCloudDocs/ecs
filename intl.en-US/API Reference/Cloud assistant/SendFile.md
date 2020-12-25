# SendFile

You can call this operation to send a remote file to one or more ECS instances.

## Description

-   The ECS instances to which to send a remote file must be in the Running \(`Running`\) state.
-   The Cloud Assistant client must be installed on the instances. For information about how to install the Cloud Assistant client, see [InstallCloudAssistant](~~85916~~).
-   The Cloud Assistant client can be used to send remote files only when its version is later than specific ones. If the `ClientNeedUpgrade` error code is returned, you must upgrade the Cloud Assistant client by following the instructions described in [Update or disable updates for the Cloud Assistant client](~~134383~~).
    -   For Linux instances, the version of the Cloud Assistant client must be later than 1.0.2.569.
    -   For Windows instances, the version of the Cloud Assistant client must be later than 1.0.0.149.
-   The remote file to be sent must not exceed 32 KB in size after it is encoded in Base64.
-   The remote file may fail to be sent due to exceptions on instances, network, or the Cloud Assistance client. Call the [DescribeSendFileResults](~~~~) operation to troubleshoot the issues.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=SendFile&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SendFile|The operation that you want to perform. Set the value to SendFile. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance to which to send the remote file. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Name|String|Yes|file.txt|The name of the remote file. The name can be up to 255 characters in length and can contain any characters. |
|InstanceId.N|RepeatList|Yes|i-bp185dy2o3o6n\*\*\*\*|The ID of instance N to which to send the remote file. A maximum of 50 instance IDs can be specified. Valid values of N: 1 to 50. |
|TargetDir|String|Yes|/home|The destination directory on the instance to which to send the remote file. If this parameter is not specified, the system automatically selects a directory on the instance. |
|Content|String|Yes|\#! /bin/bash echo "Current User is :" echo $\(ps \| grep "$$" \| awk '\{print $2\}'\) -------- oss://bucketName/objectName|The content of the remote file. The content must not exceed 32 KB in size after it is encoded in Base64.

-   If `ContentType` is set to `PlainText`, the Content value is a plaintext string.
-   If `ContentType` is set to `Base64`, the Content value is a Base64-encoded string. |
|Description|String|No|This is a test file.|The description of the remote file. The description can be up to 512 characters in length and can contain any characters. |
|ContentType|String|No|PlainText|The content type of the remote file. Valid values:

-   PlainText
-   Base64

Default value: PlainText. |
|Timeout|Long|No|60|The timeout period for sending the remote file. Unit: seconds.

-   A timeout error occurs if the file fails to be sent due to specific reasons. For example, a process error occurs, a specific module does not exist, or the Cloud Assistant client is not installed.
-   If the specified timeout period is less than 10 seconds, the system automatically sets the timeout period to 10 seconds to ensure that the file is sent to the instances.

Default value: 60. |
|FileOwner|String|No|root|The owner of the remote file. This parameter takes effect only on Linux instances. Default value: root. |
|FileGroup|String|No|root|The user group of the remote file. This parameter takes effect only on Linux instances. Default value: root. |
|FileMode|String|No|0644|The permissions on the remote file. This parameter takes effect only on Linux instances. You can configure this parameter in the same way as you configure the chmod command.

The default value is 0644 and indicates that the owner of the file has the read and write permissions on the file and that the user group of the file and other users have only the read permission on the file. |
|Overwrite|Boolean|No|true|Specifies whether to overwrite a file in the destination directory if the file has the same name as the sent file.

-   true: overwrites the file.
-   false: does not overwrite the file.

Default value: false. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|InvokeId|String|f-7d2a745b412b46\*\*\*\*|The ID of the execution. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=SendFile
&Content='echo hello'
&InstanceId.1=i-bp185dy2o3o6n****
&Name=file.txt
&RegionId=cn-hangzhou
&TargetDir=/home
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SendFileResponse>
          <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
          <InvokeId>f-7d2a745b412b46****</InvokeId>
</SendFileResponse>
```

`JSON` format

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "InvokeId": "f-7d2a745b412b46****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was being sent. Try again later.|
|403|FileSize.ExceedLimit|The length of file content exceeds limit.|The error message returned because the maximum length of the file content has been reached.|
|403|FileName.ExceedLimit|The length of file name exceeds limit.|The error message returned because the maximum length of the file name has been reached.|
|403|FileDesc.ExceedLimit|The length of file description exceeds limit.|The error message returned because the maximum length of the file description has been reached.|
|403|FileTargetDir.Invalid|The target directory of file is invalid.|The error message returned because the specified TargetDir parameter is invalid.|
|403|InstanceIds.ExceedLimit|The number of instance IDs exceeds the upper limit.|The error message returned because more than 50 instances are specified.|
|403|FileMode.Invalid|The mode of file is invalid.|The error message returned because the specified FileMode parameter is invalid.|
|403|FileContent.DecodeError|The Content can not be base64 decoded.|The error message returned because the file content cannot be decoded in Base64.|
|403|FileContentType.Invalid|The ContentType of file is invalid.|The error message returned because the specified ContentType parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

