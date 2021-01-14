---
keyword: [Java使用云助手, 云助手SDK示例, Java管理ECS]
---

# Java程序免登录管理ECS实例

云助手命令可以在多台ECS实例中批量执行Shell、Bat或者PowerShell脚本。本文介绍如何通过Java SDK检测云助手客户端状态、运行云助手命令和查询云助手命令执行结果。

-   目标ECS实例已安装云助手客户端。具体操作，请参见[安装云助手客户端](/intl.zh-CN/运维与监控/云助手/配置云助手客户端/安装云助手客户端.md)。
-   ECS实例状态必须为**运行中**（`Running`）。关于如何使用Java SDK查询实例的状态，请参见[查询ECS实例](/intl.zh-CN/SDK示例/Java示例/查询ECS实例.md)。
-   已更新Java开发环境中的SDK依赖aliyun-java-sdk-ecs至4.18.3或以上版本。更多详情，请前往[Maven项目](https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-ecs)获取最新版本。
-   根据ECS实例的配置，以及您需要执行的操作，准备好云助手使用的命令（Shell、Bat或者PowerShell命令）。

云助手客户端只有在运行中状态时，才支持远程执行命令，因此在使用前建议检测云助手客户端的运行状态。

1.  获取阿里云账号AccessKey，以及查询地域ID。

    具体步骤，请参见[地域和可用区]()和[创建AccessKey]()。

2.  新建一个RunCommandBestPractice类，为一台或多台的ECS实例执行云助手命令。

    RunCommandBestPractice类主要实现以下功能：

    1.  检查云助手客户端的运行状态。

        云助手客户端只有在**运行中**状态时，才支持远程执行命令。此步骤先检查云助手客户端状态是否为**运行中**，并根据检查结果判断下一步操作：

        -   如果不是**运行中**，则等待并重试。
        -   如果是**运行中**，则执行下一步。
    2.  执行云助手命令。
    示例代码如下所示：

    ```
    import com.aliyuncs.AcsResponse;
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.IAcsClient;
    import com.aliyuncs.RpcAcsRequest;
    import com.aliyuncs.ecs.model.v20140526.DescribeCloudAssistantStatusRequest;
    import com.aliyuncs.ecs.model.v20140526.DescribeCloudAssistantStatusResponse;
    import com.aliyuncs.ecs.model.v20140526.RunCommandRequest;
    import com.aliyuncs.ecs.model.v20140526.RunCommandResponse;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.exceptions.ServerException;
    import com.aliyuncs.profile.DefaultProfile;
    import com.google.gson.Gson;
    
    import java.util.Arrays;
    import java.util.List;
    
    public class RunCommandBestPractice {
        private static final int MAX_RETRIES = 2;
        private static final long MAX_WAIT_INTERVAL = 20000L;
        private static final long TIME_OUT = 60L;
    
        public static void main(String[] args) throws InterruptedException {
            //一台或多台ECS实例组成的ID列表。
            List<String> instanceIds = Arrays.asList("<yourInstanceId01>", "<yourInstanceId02>");
    
            if (!checkCloudAssistantStatus(instanceIds)) {
                //超时后，云助手状态仍未处于运行中。
                //处理异常或继续调用RunCommand。
            }
    
            RunCommandResponse runCommandResponse = runCommand(instanceIds);
            System.out.println(new Gson().toJson(runCommandResponse));
            //调用DescribeInvocations查询云助手命令执行结果。
        }
    
        /**
         * 检查云助手客户端状态。
         * 如果状态为false，等待一段时间并重试。
         * @param instanceIds
         * @return
         * @throws InterruptedException
         */
        private static boolean checkCloudAssistantStatus(List<String> instanceIds) throws InterruptedException {
            int retryTimes = 0;
            boolean retry = false;
            do {
                long waitTime = Math.min(getWaitInternal(retryTimes), MAX_WAIT_INTERVAL);
                Thread.sleep(waitTime);
                DescribeCloudAssistantStatusResponse describeCloudAssistantStatusResponse = describeCloudAssistantStatus(instanceIds);
                if (describeCloudAssistantStatusResponse == null) {
                    //处理API异常，例如实例不存在或停机等。
                    retry = false;
                } else {
                    for (DescribeCloudAssistantStatusResponse.InstanceCloudAssistantStatus instanceCloudAssistantStatus :
                            describeCloudAssistantStatusResponse.getInstanceCloudAssistantStatusSet()) {
                        if ("false".equals(instanceCloudAssistantStatus.getCloudAssistantStatus())) {
                            retry = true;
                            break;
                        }
                    }
                }
            } while (retry && (retryTimes++ < MAX_RETRIES));
    
            return retryTimes <= MAX_RETRIES;
        }
    
        /**
         * 调用DescribeCloudAssistantStatus查询实例是否安装了云助手客户端。
         * @param instanceIds
         * @return
         */
        private static DescribeCloudAssistantStatusResponse describeCloudAssistantStatus(List<String> instanceIds) {
            DescribeCloudAssistantStatusRequest describeCloudAssistantStatusRequest = new DescribeCloudAssistantStatusRequest();
            describeCloudAssistantStatusRequest.setInstanceIds(instanceIds);
            return sendRequest(describeCloudAssistantStatusRequest);
        }
    
        /**
         * 调用RunCommand运行云助手命令
         * @param instanceIds
         * @return
         */
        private static RunCommandResponse runCommand(List<String> instanceIds) {
            RunCommandRequest runCommandRequest = new RunCommandRequest();
            //编辑云助手使用的命令内容。
            runCommandRequest.setCommandContent("<yourScript>");
            runCommandRequest.setInstanceIds(instanceIds);
            runCommandRequest.setType("RunShellScript");
            runCommandRequest.setTimeout(TIME_OUT);
            return sendRequest(runCommandRequest);
        }
    
        /**
         * 使用指数退避算法获取重试的间隔时间
         * @param retryTime
         * @return
         */
        private static long getWaitInternal(int retryTime) {
            return (long)(Math.pow(2, retryTime) * 1000L);
        }
    
        private static <T extends AcsResponse> T sendRequest(RpcAcsRequest<T> request) {
            // 初始化profile对象，并设置地域ID（例如cn-hangzhou）和AccessKey。
            DefaultProfile profile = DefaultProfile.getProfile("<yourRegionId>", "<yourAccessKeyId>", "<yourAccessKeySecret>");
            IAcsClient client = new DefaultAcsClient(profile);
            try {
                T response = client.getAcsResponse(request);
                return response;
            } catch (ServerException e) {
                //处理5XX错误
                e.printStackTrace();
            } catch (ClientException e) {
                //处理4XX错误
                System.out.println("ErrCode:" + e.getErrCode());
                System.out.println("ErrMsg:" + e.getErrMsg());
                System.out.println("RequestId:" + e.getRequestId());
            }
            return null;
        }
    }
    ```

    **说明：** 如果云助手客户端状态一直为**未运行**，建议您从以下几方面进行排查：

    -   检查是否安装了云助手客户端。2017年12月01日之后使用公共镜像创建的ECS实例，默认预装云助手客户端。如果您的实例未安装云助手客户端，请先手动安装。具体操作，请参见[安装云助手客户端](/intl.zh-CN/运维与监控/云助手/配置云助手客户端/安装云助手客户端.md)。
    -   检查网络配置。请您确保在实例中，能够正常的进行域名解析和网络请求，并且能够访问云助手服务地址（`https://\{regionId\}.axt.aliyun.com`，其中\{regionId\}改为您的实例所在地域）。
    返回结果如下所示，并记录InvokeId。

    ```
    {
        "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
        "InvokeId": "t-hz0b22o6******",
        "CommandId": "c-b224dc5072f3460fbb10fc2912******"
    }
    ```

3.  新建一个DescribeInvocationsSample类，查询命令运行是否成功。

    ```
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.IAcsClient;
    import com.aliyuncs.ecs.model.v20140526.DescribeInvocationsRequest;
    import com.aliyuncs.ecs.model.v20140526.DescribeInvocationsResponse;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.exceptions.ServerException;
    import com.aliyuncs.profile.DefaultProfile;
    import com.google.gson.Gson;
    
    public class DescribeInvocationsSample {
        public static void main(String[] args) {
            DefaultProfile profile = DefaultProfile.getProfile("<yourRegionId>", "<yourAccessKeyId>", "<yourAccessKeySecret>");
            IAcsClient client = new DefaultAcsClient(profile);
    
            DescribeInvocationsRequest request = new DescribeInvocationsRequest();
            // 填写云助手命令的执行ID。
            request.setInvokeId("t-hz0b22o6******");
    
            try {
                DescribeInvocationsResponse response = client.getAcsResponse(request);
                System.out.println(new Gson().toJson(response));
            } catch (ServerException e) {
                e.printStackTrace();
            } catch (ClientException e) {
                System.out.println("ErrCode:" + e.getErrCode());
                System.out.println("ErrMsg:" + e.getErrMsg());
                System.out.println("RequestId:" + e.getRequestId());
            }
        }
    }
    ```

    返回结果如下所示，通过InvokeInstances，您可以查看命令的运行状态和结果。更多信息，请参见[DescribeInvocations](/intl.zh-CN/API参考/云助手/DescribeInvocations.md)。

    ```
    {
        "requestId": "42837BE9-1230-4E66-A21C-EC11C24221A3",
        "totalCount": 1,
        "pageNumber": 1,
        "pageSize": 10,
        "invocations": [{
            "invokeId": "t-hz0b22o6******",
            "creationTime": "2021-01-07T10:11:03Z",
            "commandId": "c-hz0179jxlag****",
            "commandType": "RunShellScript",
            "commandName": "cmd-2021-01-07",
            "commandContent": "******",
            "frequency": "",
            "timed": false,
            "invokeStatus": "PartialFailed",
            "invocationStatus": "PartialFailed",
            "parameters": "{}",
            "username": "",
            "invokeInstances": [{
                "instanceId": "i-bp11entzst4xwyb******",
                "repeats": 1,
                "instanceInvokeStatus": "Finished",
                "invocationStatus": "Success",
                "output": "******",
                "exitCode": 0,
                "dropped": 0,
                "errorCode": "",
                "errorInfo": "",
                "creationTime": "2021-01-07T10:11:03Z",
                "startTime": "2021-01-07T10:11:04Z",
                "stopTime": "",
                "finishTime": "2021-01-07T10:11:05Z",
                "updateTime": "2021-01-07T10:11:05Z"
            }, {
                "instanceId": "i-bp1ida94x2133l******",
                "repeats": 1,
                "instanceInvokeStatus": "Failed",
                "invocationStatus": "Timeout",
                "output": "******",
                "dropped": 49259,
                "errorCode": "ExecutionTimeout",
                "errorInfo": "the command execution has been timeout.",
                "creationTime": "2021-01-07T10:11:03Z",
                "startTime": "2021-01-07T10:11:04Z",
                "stopTime": "",
                "finishTime": "2021-01-07T10:12:04Z",
                "updateTime": "2021-01-07T10:12:04Z"
            }]
        }]
    }
    ```


**相关文档**  


[RunCommand](/intl.zh-CN/API参考/云助手/RunCommand.md)

[DescribeInstances](/intl.zh-CN/API参考/实例/DescribeInstances.md)

[DescribeInvocations](/intl.zh-CN/API参考/云助手/DescribeInvocations.md)

