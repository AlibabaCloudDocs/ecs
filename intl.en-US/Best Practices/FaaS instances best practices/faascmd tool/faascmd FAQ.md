# faascmd FAQ

This topic provides answers to commonly asked questions about the faascmd tool.

-   FAQ
    -   [What do I do if the "Name Error:global name'ID' is not defined." error message is returned?](#section_zff_yik_qih)
    -   [What do I do if the "SDK.InvalidRegionId. Can not find endpoint to access." error message is returned?](#section_drz_bmg_89n)
    -   [What do I do if the "HTTP Status: 404 Error: EntityNotExist." Role Error. The specified Role not exists . error message is returned?](#section_kcv_wuf_6k5)
    -   [When I attempt to download an FPGA image, the "HTTP Status:404 Error:SHELL NOT MATCH. The image Shell is not match with fpga Shell! Request ID:D7D1AB1E-8682-4091-8129-C17D54FD10D4" error message is returned. What do I do?](#section_d2n_1oo_sm0)
    -   [When I attempt to download an FPGA image, the "HTTP Status:503 Error:ANOTHER TASK RUNNING. Another task has not finished yet, please retry later! Request ID: 5FCB6F75-8572-4840-9BDC-87C57174F26D" error message is returned. What do I do?](#section_8el_16a_6tb)
    -   [What do I do if the image status is displayed as failed when I run the faascmd list\_images command?](#section_lqa_a7d_mvw)
-   [Error codes](#section_tzt_drr_5fb)

## What do I do if the "Name Error:global name'ID' is not defined." error message is returned?

Cause: faascmd cannot obtain your AccessKey ID or AccessKey secret.

Solution: Run the `faascmd config` command to save the AccessKey ID and AccessKey secret information you entered to the /root/.faascredentials file.

## What do I do if the "SDK.InvalidRegionId. Can not find endpoint to access." error message is returned?

Cause: faascmd cannot obtain the endpoint of FPGA as a Service \(FaaS\).

Solution: Perform the following steps to check whether faascmd configurations meet the specified requirements:

-   Run the `python -V` command to check whether the installed version of Python is 2.7.x.
-   Run the `which python` command to check whether the default installation path of Python is `/usr/bin/python`.
-   Run the `cat /usr/lib/python2.7/site-packages/aliyunsdkcore/__init__.py` command to check whether the installed version of aliyunsdkcore is 2.11.0 or later.

    **Note:** If the aliyunsdkcore version is earlier than 2.11.0, run the `pip install --upgrade aliyun-python-sdk-core` command to upgrade aliyunsdkcore to the latest version.


## What do I do if the "HTTP Status: 404 Error: EntityNotExist." Role Error. The specified Role not exists . error message is returned?

Cause: AliyunFAASDefaultRole does not exist in your Alibaba Cloud account.

Solution: Log on to the [RAM console](https://ram.console.aliyun.com/) to check whether AliyunFAASDefaultRole exists.

-   If AliyunFAASDefaultRole does not exist, run the `faascmd config` and `faascmd auth` commands to create the role and grant permissions to it.
-   If AliyunFAASDefaultRole exists, submit a ticket.

## When I attempt to download an FPGA image, the "HTTP Status:404 Error:SHELL NOT MATCH. The image Shell is not match with fpga Shell! Request ID:D7D1AB1E-8682-4091-8129-C17D54FD10D4" error message is returned. What do I do?

Cause: The shell versions of the target FPGA image and the specified FPGA do not match.

Solution: Perform the following steps:

-   Run the `faascmd list_instances --instance=xxx` command to check the shell version of the current FPGA.
-   Run the `faascmd list_images` command to check the shell version of the specified FPGA image.

    **Note:**

    -   If the two shell versions are different, you must create a new FPGA image of the same shell version as the FPGA, and then download the image.
    -   If the two shell versions are the same, submit a ticket.

## When I attempt to download an FPGA image, the "HTTP Status:503 Error:ANOTHER TASK RUNNING. Another task has not finished yet, please retry later! Request ID: 5FCB6F75-8572-4840-9BDC-87C57174F26D" error message is returned. What do I do?

Cause: The FPGA is still in the operating state due to an unexpected failure or interruption of the download request you submitted.

Solution: We recommend that you wait 10 minutes until the download task ends, and then resubmit an image download request.

**Note:** If this problem persists, submit a ticket.

## What do I do if the image status is displayed as failed when I run the faascmd list\_images command?

Run the following commands to obtain the compilation log for troubleshooting:

```
faascmd list_objects|grep vivado
faascmd get_object --object=<YourObjectName> --file=<YourLocalPath>/vivado.log  #If no path is specified, the compilation log is downloaded to the current folder.
```

## Error codes

|HTTP status code|Error code|Error message|Description|Application scope|
|----------------|----------|-------------|-----------|-----------------|
|400|PARAMETER INVALIDATE|Specify parameters are invalid.|The error message returned because input parameters are invalid.|-   All faascmd commands
-   All API operations |
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an unknown error has occurred. Submit a ticket.|
|404|InvalidProduct.NotFound|Cannot find product according to your specified domain.|The error message returned because the FaaS product does not exist. Check whether the endpoint configuration of Python Core SDK is correct.|
|404|InvalidAccessKeyId.NotFound|Specified access key is not found.|The error message returned because the specified AccessKey ID does not exist.|
|400|InvalidAccessKeyId.Inactive|Specified access key is disabled.|The error message returned because the specified AccessKey pair is disabled.|
|400|InvalidSecurityToken.Expired|Specified SecurityToken is expired.|The error message returned because the specified security token has expired.|
|400|InvalidSecurityToken.Malformed|Specified SecurityToken is malformed.|The error message returned because the specified security token is invalid.|
|400|InvalidSecurityToken.MismatchWithAccessKey|Specified SecurityToken mismatch with the AccessKey.|The error message returned because the specified security token does not match the AccessKey pair.|
|403|NoPermisson|You are not authorized to do this action.|The error message returned because the current RAM user is not authorized to perform this operation.|-   faascmd command: auth
-   API operation: auth |
|401|IMAGE NUMBER EXCEED|The user is allowed to have no more than 30 images.|The error message returned because the number of images has reached the upper limit of 30. Delete images that are no longer needed.|-   faascmd command: create\_image
-   API operation: CreateFpgaImage |
|503|FREQUENCY ERROR|CreateFpgaImage task is allowed to take every half an hour.|The error message returned because the interval between two consecutive image creation requests is less than 30 minutes.|
|404|SHELL NOT SUPPORT|The shellUUID is not supported, please check your input shellUUID.|The error message returned because the specified shell version is not supported.|
|404|EntityNotExist.RoleError|The specified Role not exists.|The error message returned because AliyunFAASDefaultRole does not exist in your account.|
|403|AccessDeniedError|The bucket you visit does not belong to you.|The error message returned because the RAM user used to configure faascmd is not authorized to access the current bucket.|
|403|CALLER TYPE NOT SUPPORT|The callerType is not supported, please use sub user's AK.|The error message returned because the specified user identity credential is not supported. Only the identity credentials of RAM users are supported.|
|404|NoSuchBucketError|The specified bucket does not exist.|The error message returned because the specified OSS bucket does not exist. Check whether the specified bucket name is correct.|
|404|OSS OBJECT NOT FOUND|The specified oss object does not exist.|The error message returned because the specified OSS object does not exist or you have not authorized the FaaS RAM role to access the object.|
|404|IMAGE NOT FOUND|The specify image does not found.|The error message returned because the specified fpgaImage parameter does not exist.|-   faascmd command: delete\_image
-   API operations:
    -   DeleteFpgaImage
    -   DeletePublishFpgaImage |
|401|NOT AUTHORIZED|You are not allowed to access this instance.|The error message returned because you are not authorized to access the specified instance. Check whether the permission policy of your account includes the permission to call the [DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md) operation.|-   faascmd command: list\_instances
-   API operation: DescribeFpgaInstances |
|403|CALLER TYPE NOT SUPPORT|The callerType is not supported.|The error message returned because the specified user identity credential is not supported. Only STS tokens and the AccessKey pairs of RAM users are supported.|
|404|INSTANCE INVALIDATE|The instance you specify is not FPGA type.|The error message returned because the specified instance is not an FPGA-based ECS instance. If you are sure that the instance is an FPGA-based ECS instance, submit a ticket.|
|401|NOT AUTHORIZED|You are not allowed to access this instance.|The error message returned because the specified instance ID does not exist. Check the input parameters.|-   faascmd command: fpga\_status
-   API operation: DescribeLoadTaskStatus |
|404|FPGA NOT FOUND|The fpga you specify is not found.|The error message returned because the specified fpgauuid parameter does not exist. Check the input parameters.|
|503|ANOTHER TASK RUNNING|Another task is running, user is allowed to take this task half an hour.|The error message returned because the previous image download task you submitted is still in the operating state.|-   faascmd command: download\_image
-   API operation: LoadFpgaImage |
|401|IMAGE ACCESS ERROR|You are not allowed to access this fpga image.|The error message returned because the specified image does not belong to your account.|
|401|YOU HAVE NO ACCESS TO THIS INSTANCE|You are not allowed to access this instance.|The error message returned because the specified instance does not belong to your account.|
|404|IMAGE NOT FOUND|The fpga image you specify is not found.|The error message returned because the specified fpgaImage parameter does not exist.|
|404|FPGA NOT FOUND|The fpga you specify is not found.|The error message returned because the specified FPGA-based ECS instance does not exist.|
|404|SHELL NOT MATCH|The imageShell is not match with fpgaShell.|The error message returned because the shell version of the specified image does not match that of the specified FPGA-based ECS instance.|
|403|ASSUME ROLE USER NOT SUPPORT|AssumeRoleUser only support loading market fpga images.|The error message returned because the STS token is used to download an FPGA image that is not an Alibaba Cloud Marketplace image. STS tokens can only be used to download Alibaba Cloud Marketplace images.|
|404|Image not in success state|The fpga image you specify is not in success state.|The error message returned because the specified FPGA image is not in the success state. Only images in the success state can be downloaded.|
|404|FPGA IMAGE STATE ERROR|The specify fpga image is not in success state.|The error message returned because the specified FPGA image is not in the success state.|-   faascmd command: publish\_image
-   API operation: PublishFpgaImage |
|404|FPGA IMAGE NOT FOUND|The specify fpga image does not found.|The error message returned because the specified image does not exist or does not belong to your account.|

