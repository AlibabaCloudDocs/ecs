---
keyword: [sdk, java sdk, ecs, aliyun-java-sdk-ecs, preemptible instance]
---

# Create a preemptible instance

This topic describes how to use Alibaba Cloud ECS SDK for Java to call the DescribeAvailableResource operation to query available resources, call the DescribeSpotPriceHistory operation to query the historical prices of preemptible instances, and call the CreateInstance operation to create a preemptible instance.

-   The version of Alibaba Cloud ECS SDK for Java is V4.2.0 or later.
-   The image to be used to create a preemptible instance contains all the environment dependencies that are required to run the instance. We recommend that you use a custom image to create a preemptible instance to ensure that the instance can process business data. In this example, the image ID is m-bp146shijn7hujkui9\*\*\*.
-   Call the DescribeRegions operation to query the region where you want to create ECS instances. In this example, the region is cn-hangzhou.
-   Call the DescribeInstanceTypes operation to query the instance type that you want to select. In this example, the instance type is ecs.g5.large. For more information, see [Instance families](/intl.en-US/Instance/Instance families.md).

Preemptible instances help you build a cost-effective solution to process business data. When you create a preemptible instance, you can set a maximum price per hour to bid for a specified instance type. If your price is higher than the current market price, your instance is created and billed at the current market price. Preemptible instances are used to control computing costs and are suitable for stateless applications. For more information, see [Overview](/intl.en-US/Instance/Instance purchasing options/Preemptible instances/Overview.md).

## Procedure

1.  Encapsulate an ApiCaller.java class to initialize a profile and a client and add exception handling logic.

    ```
    public class ApiCaller {
        IClientProfile profile;
        IAcsClient client;
    
        public ApiCaller() {
            profile = DefaultProfile.getProfile("cn-hangzhou", AKSUtil.accessKeyId, AKSUtil.accessKeySecret);
            client = new DefaultAcsClient(profile);
        }
    
        public  <T extends AcsResponse> T doAction(AcsRequest<T> var1) {
            try {
                return  client.getAcsResponse(var1);
            } catch (ServerException e) {
                e.printStackTrace();
            } catch (ClientException e) {
                System.out.println("ErrCode:" + e.getErrCode());
                System.out.println("ErrMsg:" + e.getErrMsg());
                System.out.println("RequestId:" + e.getRequestId());
            }
            return null;
        }
    
     }
    ```

2.  Call the DescribeAvailableResource operation to query the instance types that are available in the specified region.

    ```
    public class DescribeAvailableResourceSample {
    
        public static void main(String[] args) {
    
            ApiCaller caller = new ApiCaller();
            DescribeAvailableResourceRequest request = new DescribeAvailableResourceRequest();
            // Call the DescribeRegionsRequest operation to obtain the region ID.
            request.setRegionId("cn-hangzhou");
            request.setDestinationResource("InstanceType");
            // Required. Set the InstanceChargeType parameter to PostPaid.
            request.setInstanceChargeType("PostPaid");
            // Required. Set the SpotStrategy parameter of the preemptible instance.
            request.setSpotStrategy("SpotAsPriceGo");
            // If you do not specify a zone ID, all zones in which preemptible instances can be created are queried.
            request.setZoneId("cn-hangzhou-h");
            // If you do not specify an instance type, all instance types that can be selected to create preemptible instances are queried.
            request.setInstanceType("ecs.g5.large");
            request.setSystemDiskCategory("cloud_ssd");
            request.setNetworkCategory("vpc");
    
            DescribeAvailableResourceResponse response = caller.doAction(request);
            System.out.println(JSON.toJSONString(response));
        }
    }
    ```

    Sample success responses:

    ```
    {
        "RequestId": "D8491D5E-AB8A-4E22-BDB4-EEEE1F1C8241",
        "AvailableZones": {
            "AvailableZone": [
                {
                    "Status": "Available",
                    "RegionId": "cn-hangzhou",
                    "AvailableResources": {
                        "AvailableResource": [
                            {
                                "Type": "InstanceType",
                                "SupportedResources": {
                                    "SupportedResource": [
                                        {
                                            "Status": "Available",
                                            "Value": "ecs.g5.large",
                                            "StatusCategory": "WithStock"
                                        }
                                    ]
                                }
                            }
                        ]
                    },
                    "ZoneId": "cn-hangzhou-h",
                    "StatusCategory": "WithStock"
                }
            ]
        }
    }
    ```

3.  Optional. Call the DescribeSpotPriceHistory operation to query the historical prices of preemptible instances.

    **Note:** The DescribeSpotPriceHistory operation allows you to obtain the historical prices for up to the last 30 days.

    ```
    public class DescribeSpotPriceHistorySample {
    
        public static void main(String[] args) {
    
            ApiCaller caller = new ApiCaller();
            List<DescribeSpotPriceHistoryResponse.SpotPriceType> result = new ArrayList<DescribeSpotPriceHistoryResponse.SpotPriceType>();
            int offset = 0;
            while (true) {
                DescribeSpotPriceHistoryRequest request = new DescribeSpotPriceHistoryRequest();
                // Required. The region ID.
                request.setRegionId("cn-hangzhou");
                // Required. The zone ID.
                request.setZoneId("cn-hangzhou-b");
                // Required. The instance type.
                request.setInstanceType("ecs.g5.large");
                // Required. The network type.
                request.setNetworkType("vpc");
                // Optional. The start of the time range to query. By default, the time range is three hours.
                // request.setStartTime("2017-09-20T08:45:08Z");
                // Optional. The end of the time range to query. If the end time is not specified, the default end time is the current time. The prices within three hours earlier than current time are queried.
                // request.setEndTime("2017-09-28T08:45:08Z");
                request.setOffset(offset);
                DescribeSpotPriceHistoryResponse response = caller.doAction(request);
                if (response ! = null && response.getSpotPrices() ! = null) {
                    result.addAll(response.getSpotPrices());
                }
                if (response.getNextOffset() == null || response.getNextOffset() == 0) {
                    break;
                } else {
                    offset = response.getNextOffset();
                }
            }
            if (! result.isEmpty()) {
                for (DescribeSpotPriceHistoryResponse.SpotPriceType spotPriceType : result) {
                    System.out.println(spotPriceType.getTimestamp() + "--->spotPrice:" + spotPriceType.getSpotPrice() + "---->originPrice:" + spotPriceType.getOriginPrice());
                }
                System.out.println(result.size());
            } else {
            }
    
        }
    
    }
    ```

    Sample success responses:

    ```
    2017-09-26T06:28:55Z--->spotPrice:0.24---->originPrice:1.2
    2017-09-26T14:00:00Z--->spotPrice:0.36---->originPrice:1.2
    2017-09-26T15:00:00Z--->spotPrice:0.24---->originPrice:1.2
    2017-09-27T14:00:00Z--->spotPrice:0.36---->originPrice:1.2
    2017-09-27T15:00:00Z--->spotPrice:0.24---->originPrice:1.2
    2017-09-28T14:00:00Z--->spotPrice:0.36---->originPrice:1.2
    2017-09-28T15:00:00Z--->spotPrice:0.24---->originPrice:1.2
    2017-09-29T06:28:55Z--->spotPrice:0.24---->originPrice:1.2
    ```

4.  Call the CreateInstance operation to create a preemptible instance.

    To create multiple preemptible instances at a time, you can call the RunInstances operation. For more information, see [Batch create ECS instances](/intl.en-US/SDK Reference/Java example/Create an ECS instance/Batch create ECS instances.md).

    ```
    public class CreateInstanceSample {
    
        public static void main(String[] args) {
    
            ApiCaller caller = new ApiCaller();
    
            CreateInstanceRequest request = new CreateInstanceRequest();
            // The region ID.
            request.setRegionId("cn-hangzhou");
            // The zone ID.
            request.setZoneId("cn-hangzhou-h"); 
            // The ID of the security group.
            request.setSecurityGroupId("sg-bp11nhf94ivkdxwb2***");
            // The image ID. We recommend that you use a custom image to create a preemptible instance.
            request.setImageId("m-bp146shijn7hujkui9***");
            // The ID of the vSwitch that is in the same VPC as the security group.
            request.setVSwitchId("vsw-bp164cyonthfudn9kj***");
    
            // The instance type that you want to purchase.
            request.setInstanceType("ecs.g5.large"); 
    
            // The category of the system disk. Valid values: cloud_essd, cloud_ssd, cloud_efficiency, and cloud.
            request.setSystemDiskCategory("cloud_ssd");
            request.setSystemDiskSize(40);
    
            // Required. Set the InstanceChargeType parameter to PostPaid.
            request.setInstanceChargeType("PostPaid");
            // Set the SpotStrategy parameter to SpotWithPriceLimit. You can also set the SpotStrategy parameter to SpotAsPriceGo to use the system-provided pay-as-you-go price as the maximum bidding price. In this case, you do not need to specify the SpotPriceLimit parameter.
            request.setSpotStrategy("SpotWithPriceLimit");
            // If you set the SpotStrategy parameter to SpotWithPriceLimit, the maximum bidding price that you specify must be higher than the current market price. Otherwise, the instance cannot be created.
            request.setSpotPriceLimit(0.25F);
    
            // Set the Amount parameter to 2 to create two preemptible instances. By default, only one preemptible instance is created if this parameter is not set.
            // request.setAmount(2);
    
            CreateInstanceResponse response = caller.doAction(request);
            System.out.println(response.getInstanceId());
    
        }
    }
    ```

5.  Query the recycle time of the preemptible instance.

    **Note:** Preemptible instances can be reclaimed. We recommend that you configure a service interruption solution or a load balancing mechanism when you create a preemptible instance. This can avoid problems if the preemptible instance is released.

    -   Method 1: Run the following command in the operating system of the preemptible instance to query the recycle time of the instance based on the instance metadata:

        ```
        curl http://100.100.100.200/latest/meta-data/instance/spot/termination-time
        ```

        **Note:** If the output is empty, you can continue using the preemptible instance. If the output contains a point in time that follows the format of yyyy-MM-ddTHH:mm:ssZ and is displayed in UTC, the preemptible instance is recycled at that point in time. Example: `2015-01-05T18:02:00Z`.

    -   Method 2: Call the DescribeInstances operation to check whether the instance is in the Pending Release state based on the returned OperationLocks parameter.

        ```
        public class DescribeInstancesSample {
          public static void main(String[] args) throws InterruptedException {
        
              ApiCaller caller = new ApiCaller();
              JSONArray allInstances = new JSONArray();
              allInstances.addAll(Arrays.asList("i-bp18hgfai8ekoqwo0***", "i-bp1ecbyds24ij63w1***"));
        
              while (! allInstances.isEmpty()) {
        
                  DescribeInstancesRequest request = new DescribeInstancesRequest();
                  request.setRegionId("cn-hangzhou");
                  // Specify an instance ID to make the query more efficient.
                  request.setInstanceIds(allInstances.toJSONString());
                  DescribeInstancesResponse response = caller.doAction(request);
                  List<DescribeInstancesResponse.Instance> instanceList = response.getInstances();
        
                  if (instanceList ! = null && ! instanceList.isEmpty()) {
                      for (DescribeInstancesResponse.Instance instance : instanceList) {
                          System.out.println("result:instance:" + instance.getInstanceId() + ",was created in zone:" + instance.getZoneId());
                          if (instance.getOperationLocks() ! = null) {
                              for (DescribeInstancesResponse.Instance.LockReason lockReason : instance.getOperationLocks()) {
                                  System.out.println("instance: " + instance.getInstanceId() + "-->lockReason:" + lockReason.getLockReason() + ",instanceStatus:" + instance.getStatus());
                                  if ("Recycling".equals(lockReason.getLockReason())) {
                                      // The recycle time of the instance is returned and the ID of the recycled instance is deleted from the instance ID list.
                                      System.out.println("Preemptible instance will be recycled immediately, instance id: " + instance.getInstanceId());
                                      allInstances.remove(instance.getInstanceId());
                                  }
                              }
                          }
                      }
                      System.out.print("Try describeInstancesRequest again later...") ;
                      Thread.sleep(2 * 60 * 1000);
                  } else {
                      break;
                  }
              }
          }
        }
        ```

        If the following response is returned, the preemptible instance has entered the Pending Release state:

        ```
        instance: i-bp1ecbyds24ij63w1***-->lockReason:Recycling,instanceStatus:Stopped
        Preemptible instance will be recycled immediately, instance id: i-bp1ecbyds24ij63w1***
        ```

    -   Method 3: Call the DescribeSystemEventAttribute operation of Cloud Monitor to query the recycle time of the preemptible instance.

        ```
        public class DescribeSystemEventAttribute {
        
            public static void main(String[] args) {
                DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<accessKeyId>", "<accessSecret>");
                IAcsClient client = new DefaultAcsClient(profile);
        
                DescribeSystemEventAttributeRequest request = new DescribeSystemEventAttributeRequest();
                // The region ID.
                request.setRegionId("cn-hangzhou");
                // The cloud service.
                request.setProduct("ecs");
                // The start of the time range to query.
                request.setStartTime("1574064240000");
        
                try {
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

        If the following response is returned, the preemptible instance has entered the Pending Release state:

        ```
        {
            "SystemEvents": {
                "SystemEvent": [
                    {
                        "Name": "Instance:PreemptibleInstanceInterruption",
                        "Status": "Normal",
                        "Time": 1574064244000,
                        "Product": "ECS",
                        "ResourceId": "acs:ecs:cn-hangzhou:1331602849963181:instance/i-bp19w6o2tqa9jvoh8***",
                        "RegionId": "cn-hangzhou",
                        "Level": "WARN",
                        "Content": "{\"action\":\"delete\",\"instanceId\":\"i-bp19w6o2tqa9jvoh8***\"}",
                        "GroupId": "0",
                        "InstanceName": "i-bp19w6o2tqa9jvoh8***"
                    }
                ]
            },
            "Message": "200",
            "RequestId": "D4730844-EF73-4856-BFF3-1BDAE8E54C81",
            "Success": true,
            "Code": "200"
        }
        ```


**Related topics**  


[DescribeRegions](/intl.en-US/API Reference/Regions/DescribeRegions.md)

[DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md)

[DescribeAvailableResource](/intl.en-US/API Reference/Regions/DescribeAvailableResource.md)

[DescribeInstanceTypes](/intl.en-US/API Reference/Instances/DescribeInstanceTypes.md)

[DescribeSpotPriceHistory](/intl.en-US/API Reference/Instances/DescribeSpotPriceHistory.md)

[CreateInstance](/intl.en-US/API Reference/Instances/CreateInstance.md)

[RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md)

[DescribeSystemEventAttribute](/intl.en-US/API Reference/System events of cloud services/System events/DescribeSystemEventAttribute.md)

