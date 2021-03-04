---
keyword: [use Cloud Assistant in Java, SDK for Java, use Java to manage ECS instances]
---

# Use Java to manage ECS instances without logon

You can simultaneously run a Cloud Assistant command on multiple ECS instances. The command can be a shell, batch, or PowerShell command. This topic describes how to use SDK for Java to check the status of the Cloud Assistant client, run a Cloud Assistant command, and query the executions results of the Cloud Assistant command.

-   The Cloud Assistant client is installed on the ECS instances that you want to manage. For more information, see [Install the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Install the Cloud Assistant client.md).
-   The ECS instances are in the **Running** \(`Running`\) state. For information about how to use SDK for Java to check the status of ECS instances, see [Query an ECS instance](/intl.en-US/SDK Reference/Java example/Query an ECS instance.md).
-   The aliyun-java-sdk-ecs SDK dependency in Java is updated to V4.18.3 or later. For more information, visit [MavenRepository](https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-ecs) for the latest versions.
-   The shell, batch, or PowerShell command is compiled based on the instance configurations and the operations that you want to perform.

The Cloud Assistant client can run remote commands only when it is in the running state. We recommend that you check the status of the Cloud Assistant client before you use it.

1.  Obtain the AccessKey pair \(AccessKey ID and AccessKey secret\) of your account and query the region ID.

    For more information, see [Regions and zones]() and [Create an AccessKey pair]().

2.  Create a RunCommandBestPractice class to run a Cloud Assistant command on one or more ECS instances.

    The RunCommandBestPractice class performs the following operations:

    1.  Check the status of the Cloud Assistant client on ECS instances.

        The Cloud Assistant client can run remote commands only when it is in the **running** state. In this step, the class checks whether the Cloud Assistant client is in the **running** state, and performs operations based on the check result:

        -   If the client is not in the **running** state, try again later.
        -   If the client is in the **running** state, go to the next step.
    2.  Run a Cloud Assistant command on ECS instances.
    Sample code:

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
            //The IDs of one or more ECS instances.
            List<String> instanceIds = Arrays.asList("<yourInstanceId01>", "<yourInstanceId02>");
    
            if (! checkCloudAssistantStatus(instanceIds)) {
                //After a timeout occurs, the Cloud Assistant client is still not in the running state.
                //Handle the exception or proceed to call the RunCommand operation.
            }
    
            RunCommandResponse runCommandResponse = runCommand(instanceIds);
            System.out.println(new Gson().toJson(runCommandResponse));
            //Call the DescribeInvocations operation to check the execution results of the Cloud Assistant command.
        }
    
        /**
         * Check the status of the Cloud Assistant client on the instances.
         * If a value of false is returned, try again later.
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
                    //Handle exceptions such as the exception thrown when specified instances do not exist or when specified instances are in the Stopped state.
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
         * Call the DescribeCloudAssistantStatus operation to check whether the Cloud Assistant client is installed on the instances.
         * @param instanceIds
         * @return
         */
        private static DescribeCloudAssistantStatusResponse describeCloudAssistantStatus(List<String> instanceIds) {
            DescribeCloudAssistantStatusRequest describeCloudAssistantStatusRequest = new DescribeCloudAssistantStatusRequest();
            describeCloudAssistantStatusRequest.setInstanceIds(instanceIds);
            return sendRequest(describeCloudAssistantStatusRequest);
        }
    
        /**
         * Call the RunCommand operation to run the Cloud Assistant command.
         * @param instanceIds
         * @return
         */
        private static RunCommandResponse runCommand(List<String> instanceIds) {
            RunCommandRequest runCommandRequest = new RunCommandRequest();
            //Edit the Cloud Assistant command.
            runCommandRequest.setCommandContent("<yourScript>");
            runCommandRequest.setInstanceIds(instanceIds);
            runCommandRequest.setType("RunShellScript");
            runCommandRequest.setTimeout(TIME_OUT);
            return sendRequest(runCommandRequest);
        }
    
        /**
         * Use the exponential backoff algorithm to obtain the retry interval.
         * @param retryTime
         * @return
         */
        private static long getWaitInternal(int retryTime) {
            return (long)(Math.pow(2, retryTime) * 1000L);
        }
    
        private static <T extends AcsResponse> T sendRequest(RpcAcsRequest<T> request) {
            //Initialize the profile object and configure the region ID (Example: cn-hangzhou) and the AccessKey pair.
            DefaultProfile profile = DefaultProfile.getProfile("<yourRegionId>", "<yourAccessKeyId>", "<yourAccessKeySecret>");
            IAcsClient client = new DefaultAcsClient(profile);
            try {
                T response = client.getAcsResponse(request);
                return response;
            } catch (ServerException e) {
                //Handle 5XX errors.
                e.printStackTrace();
            } catch (ClientException e) {
                //Handle 4XX errors.
                System.out.println("ErrCode:" + e.getErrCode());
                System.out.println("ErrMsg:" + e.getErrMsg());
                System.out.println("RequestId:" + e.getRequestId());
            }
            return null;
        }
    }
    ```

    **Note:** If the Cloud Assistant client is always in the **not running** state, we recommend that you troubleshoot the problem by performing the following operations:

    -   Check whether the Cloud Assistant client is installed. By default, ECS instances created from public images after December 1, 2017 are pre-installed with the Cloud Assistant client. If your instances are not installed with the Cloud Assistant client, install the client. For more information, see [Install the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Install the Cloud Assistant client.md).
    -   Check the network configurations. Make sure that you can perform domain name resolution or make network requests on the instances and that you can access the endpoint of the Cloud Assistant client in the format of `https://\{regionId\}.axt.aliyun.com`. Replace \{regionId\} with the region ID of your instances.
    A result similar to the following one is returned. Record InvokeId.

    ```
    {
        "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
        "InvokeId": "t-hz0b22o6******",
        "CommandId": "c-b224dc5072f3460fbb10fc2912******"
    }
    ```

3.  Create a DescribeInvocationsSample.java class to check whether the command is executed.

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
            //Enter the execution ID of the Cloud Assistant command.
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


A result similar to the following one is returned. You can call the InvokeInstances operation to view the execution status and results of the command. For more information, see [DescribeInvocations](/intl.en-US/API Reference/Cloud assistant/DescribeInvocations.md).

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

**Related topics**  


[RunCommand](/intl.en-US/API Reference/Cloud assistant/RunCommand.md)

[DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md)

[DescribeInvocations](/intl.en-US/API Reference/Cloud assistant/DescribeInvocations.md)

