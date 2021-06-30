# Query the interruption events of preemptible instances

If a preemptible instance is forcibly recycled due to a market price change or insufficient resources, an interruption event is triggered. Before the preemptible instance is recycled, it enters the locked state, and you are prompted that the instance will be recycled. This topic describes how to query the interruption events of preemptible instances. You can automate the instance interruption and recycle processes based on the recycle status of instances.

## Query the interruption events of preemptible instances by using CloudMonitor SDK

This section describes how to use CloudMonitor SDK for Java to query the interruption events of preemptible instances.

1.  Access CloudMonitor SDK for Java.

    For more information, see [Cloud Monitor SDK for Java](/intl.en-US/SDK Reference/Cloud Monitor SDK for Java.md).

2.  Query the interruption events of preemptible instances by using the SDK.

    The following section shows the sample code:

    ```
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.IAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.exceptions.ServerException;
    import com.aliyuncs.profile.DefaultProfile;
    import com.google.gson.Gson;
    import java.util.*;
    import com.aliyuncs.cms.model.v20190101.*;
    
    public class DescribeSystemEventAttribute {
        public static void main(String[] args) {
            // Initialize a DefaultAcsClient instance. 
            DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<AccessKeyID>", "<AccessKeySecret>");
            IAcsClient client = new DefaultAcsClient(profile);
    
            // Query the interruption events of preemptible instances. 
            DescribeSystemEventAttributeRequest request = new DescribeSystemEventAttributeRequest();
            request.setRegionId("cn-hangzhou");
            request.setProduct("ECS");
            request.setEventType("StatusNotification");
            request.setName("Instance:PreemptibleInstanceInterruption");
            try {
                // Obtain the responses. 
                DescribeSystemEventAttributeResponse response = client.getAcsResponse(request);
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

3.  Check the interruption events of preemptible instances based on the responses.

    The following section shows the event notification in the JSON format:

    ```
    {
      "ver": "1.0",
      "id": "2256A988-0B26-4E2B-820A-8A********E5",
      "product": "ECS",
      "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
      "level": "INFO",
      "name": "Instance:PreemptibleInstanceInterruption",
      "userId": "169070********30",
      "eventTime": "20190409T121826.922+0800",
      "regionId": "cn-hangzhou",
      "content": {
        "instanceId": "i-bp1ecr********5go2go",  
        "action": "delete"                       
      }
    }
    ```

    The following table describes parameters in the content field.

    |Subfield|Description|Example|
    |--------|-----------|-------|
    |instanceId|The ID of the preemptible instance.|i-bp1ecr\*\*\*\*\*\*\*\*5go2go|
    |action|The action on the preemptible instance. If the parameter is set to delete, the interrupted preemptible instance is forcibly recycled.|delete|


## Query the interruption events of preemptible instances by using instance metadata

1.  Remotely connect to an ECS instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the following command to query instance metadata:

    ```
    curl 'http://100.100.100.200/latest/meta-data/instance/spot/termination-time'
    ```

    -   If the HTTP status code of the response is 404, the instance can still be used.
    -   If information in the yyyy-MM-ddTHH:mm:ssZ \(UTC+0\) format is returned, the preemptible instance is recycled at that point in time. Example: `2015-01-05T18:02:00Z`.

## Query the interruption events of preemptible instances by calling an API operation

This section describes how to call the [DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md) operation to determine whether the instance has entered the To Be Released state based on the returned OperationLocks parameter.

The following section shows the sample code of DescribeInstancesSample.java:

```
import com.alibaba.fastjson.JSONArray;
import com.aliyuncs.AcsRequest;
import com.aliyuncs.AcsResponse;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.ecs.model.v20140526.DescribeInstancesRequest;
import com.aliyuncs.ecs.model.v20140526.DescribeInstancesResponse;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.profile.IClientProfile;
import java.util.*;

public class DescribeInstancesSample {
    public static void main(String[] args) throws InterruptedException {
        // Initialize a DefaultAcsClient instance. 
        OpenApiCaller caller = new OpenApiCaller();
        // Specify the IDs of one or more ECS instances to be queried. 
        JSONArray allInstances = new JSONArray();
        allInstances.addAll(Arrays.asList("i-bp1i9c3qiv1qs6nc****"));
        while (!allInstances.isEmpty()) {
            DescribeInstancesRequest request = new DescribeInstancesRequest();
            // Specify the region where the instances are located. 
            request.setRegionId("cn-hangzhou");
            // Specify the instance IDs for higher query efficiency. 
            request.setInstanceIds(allInstances.toJSONString());
            // Obtain the responses. 
            DescribeInstancesResponse response = caller.doAction(request);
            // Obtain instance-related results. 
            List<DescribeInstancesResponse.Instance> instanceList = response.getInstances();
            if (instanceList != null && !instanceList.isEmpty()) {
                for (DescribeInstancesResponse.Instance instance : instanceList) {
                    // Show the IDs and zone information of the queried instances. 
                    System.out.println("result:instance:" + instance.getInstanceId() + ",az:" + instance.getZoneId());
                    if (instance.getOperationLocks() != null) {
                        for (DescribeInstancesResponse.Instance.LockReason lockReason : instance.getOperationLocks()) {
                            // If an instance is locked, specify the instance ID and the corresponding lock reason. 
                            System.out.println("instance:" + instance.getInstanceId() + "-->lockReason:" + lockReason.getLockReason() + ",vmStatus:" + instance.getStatus());
                            if ("Recycling".equals(lockReason.getLockReason())) {
                                // Specify the IDs of the instances to be recycled. 
                                System.out.println("spot instance will be recycled immediately, instance id:" + instance.getInstanceId());
                                allInstances.remove(instance.getInstanceId());
                            }
                        }
                    }
                }
                // If a preemptible instance is not locked, it is queried every 2 minutes. 
                System.out.print("try describeInstances again later ...");
                Thread.sleep(2 * 60 * 1000);
            } else {
                break;
            }
        }
    }
}

// Initialize a DefaultAcsClient instance. 
class OpenApiCaller{
    IClientProfile profile;
    IAcsClient client;
    public OpenApiCaller() {
        profile = DefaultProfile.getProfile("cn-hangzhou", "<AccessKeyID>", "<AccessKeySecret>");
        client = new DefaultAcsClient(profile);
    }

    public  <T extends AcsResponse> T doAction(AcsRequest<T> var1) {
        try {
            return  client.getAcsResponse(var1);
        } catch (Throwable e) {
            e.printStackTrace();
            return null;
        }
    }
}
```

The following result is returned if the recycle is triggered:

```
result:instance:i-bp1i9c3qiv1qs6nc****,az:cn-hangzhou-i
instance:i-bp1i9c3qiv1qs6nc****-->lockReason:Recycling,vmStatus:Stopped
spot instance will be recycled immediately, instance id:i-bp1i9c3qiv1qs6nc****
```

