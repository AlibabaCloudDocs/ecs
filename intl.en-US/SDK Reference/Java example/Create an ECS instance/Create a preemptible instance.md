# Create a preemptible instance

This topic describes how to use the Alibaba Cloud ECS Java SDK to call the DescribeAvailableResource operation to query available resources, call the DescribeSpotPriceHistory operation to query the historical prices of preemptible instances, and call the CreateInstance operation to create a preemptible instance.

-   The Alibaba Cloud ECS Java SDK that you use must be V4.2.0 or later.
-   The image used to create a preemptible instance must contain all of the environment elements required to run the instance. We recommend that you use a custom image to create a preemptible instance to ensure that the instance can process business data. In this example, the ID of the image is m-bp146shijn7hujkui9\*\*\*.
-   Call the DescribeRegions operation to query the region where you want to create ECS instances. In this example, the region is cn-hangzhou.
-   Call the DescribeInstanceTypes operation to query the instance type that you want to select. In this example, the instance type is ecs.g5.large. For more information, see [Instance families](/intl.en-US/Instance/Instance families.md).

Preemptible instances provide a cost-effective solution to process business data. When you create a preemptible instance, you can set a maximum price per hour to bid for a specified instance type. If your price is higher than the current market price, your instance will be created and billed at the current market price. Preemptible instances are often used to control computing costs and are suitable in stateless application scenarios. For more information, see [Overview](/intl.en-US/Instance/Instance purchasing options/Preemptible instances/Overview.md).

## Procedure

1.  Encapsulate an ApiCaller.java class to initialize the profile and client and add exception handling logic.

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
        }
    
     }
    ```

2.  Call the DescribeAvailableResource operation to query the instance types available for the specific region.

    ```
    public class DescribeAvailableResourceSample {
    
        public static void main(String[] args) {
    
            ApiCaller caller = new ApiCaller();
            DescribeAvailableResourceRequest request = new DescribeAvailableResourceRequest();
            // Call the DescribeRegionsRequest operation to obtain the region ID.
            request.setRegionId("cn-hangzhou");
            request.setDestinationResource("InstanceType");
            // Set the billing method to pay-as-you-go. This parameter is required.
            request.setInstanceChargeType("PostPaid");
            // Set the bidding policy. This parameter is required.
            request.setSpotStrategy("SpotAsPriceGo");
            // If no zone ID is specified, all zones in which preemptible instances can be created will be queried.
            request.setZoneId("cn-hangzhou-h");
            // If no instance type is specified, all instance types that can be selected to create preemptible instances will be queried.
            request.setInstanceType("ecs.g5.large");
            request.setSystemDiskCategory("cloud_ssd");
            request.setNetworkCategory("vpc");
    
            DescribeAvailableResourceResponse response = caller.doAction(request);
            System.out.println(JSON.toJSONString(response));
        }
    }
    ```

    Sample response:

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

3.  \(Optional\) Call the DescribeSpotPriceHistory operation to query the historical prices of preemptible instances.

    **Note:** DescribeSpotPriceHistory allows you to obtain the historical prices for up to the last 30 days.

    ```
    public class DescribeSpotPriceHistorySample {
    
        public static void main(String[] args) {
    
            ApiCaller caller = new ApiCaller();
            List<DescribeSpotPriceHistoryResponse.SpotPriceType> result = new ArrayList<DescribeSpotPriceHistoryResponse.SpotPriceType>();
            int offset = 0;
            while (true) {
                DescribeSpotPriceHistoryRequest request = new DescribeSpotPriceHistoryRequest();
                request.setRegionId("cn-hangzhou");// The region is required.
                request.setZoneId("cn-hangzhou-b");// The zone is required.
                request.setInstanceType("ecs.g5.large");// The instance type is required.
                request.setNetworkType("vpc");// The network type is required.
                // request.setStartTime("2017-09-20T08:45:08Z");// Optional. The start time of a time period for which the historical prices of preemptible instances are to be queried. The time period is three days by default.
                // request.setEndTime("2017-09-28T08:45:08Z");// Optional. The end time of a time period for which the historical prices of preemptible instances are to be queried.
                request.setOffset(offset);
                DescribeSpotPriceHistoryResponse response = caller.doAction(request);
                if (response !\ = null && response.getSpotPrices() ! = null) {
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

    Sample response:

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

4.  Call the CreateInstances operation to create a preemptible instance.

    You can call the RunInstance operation to create multiple preemptible instances at a time. For more information, see [Batch create ECS instances](/intl.en-US/SDK Reference/Java example/Create an ECS instance/Batch create ECS instances.md).

    ```
    public class CreateInstancesSample {
    
        public static void main(String[] args) {
            ApiCaller caller = new ApiCaller();
            CreateInstancesRequest request = new CreateInstancesRequest();
            request.setRegionId("cn-hangzhou");// The ID of the region.
            request.setZoneId("cn-hangzhou-h"); // The ID of the zone.
            request.setSecurityGroupId("sg-bp11nhf94ivkdxwb2***");// The ID of the security group.
            request.setImageId("m-bp146shijn7hujkui9***");// We recommend that you use a custom image to create instances more quickly.
            request.setVSwitchId("vsw-bp164cyonthfudn9kj***");// The ID of the VSwitch that is in the same VPC as the security group.
    
            request.setInstanceType("ecs.g5.large"); // Enter the instance type you want to purchase after the query.
            request.setSystemDiskCategory("cloud_ssd");// The category of the system disk. Valid values: cloud_essd, cloud_ssd, cloud_efficiency, and cloud.
            request.setSystemDiskSize(40);
    
            request.setInstanceChargeType("PostPaid");// Set the billing method to pay-as-you-go. This parameter is required.
            request.setSpotStrategy("SpotWithPriceLimit");// SpotWithPriceLimit: the bidding mode. Manually set the maximum price. SpotAsPriceGo: The system provides a price automatically based on the market price.
            request.setSpotPriceLimit(0.25F);// If the bidding mode is set to SpotWithPriceLimit, the maximum price must be set higher than the current market price to create the instance.
            // request.setAmount(2);// Create two preemptible instances. If the parameter is not configured, only one preemptible instance will be created.
    
            CreateInstanceResponse response = caller.doAction(request);
            System.out.println(response.getInstanceId());
    
        }
    }
    ```

5.  Recycle a preemptible instance

    **Note:** After the instance is created, you must make sure to complete all of your business within the guaranteed duration and prepare for inconvenience that may be caused by the recycle of the instance.

    1.  Run the following command in the operating system of the preemptible instance to query the recycle time of the instance based on the instance metadata:

        ```
        curl 'http://100.100.100.200/latest/meta-data/instance/spot/termination-time'
        ```

        **Note:** If the response is empty, the preemptible instance can continue to be used. If information in format of `2015-01-05T18:02:00Z` \(UTC+0\) is returned in the response, the preemptible instance will be recycled at that point of time.

    2.  Call the DescribeInstances operation to determine whether the instance has entered the Pending Release state based on the returned OperationLocks parameter.

        ```
        public class DescribeInstancesSample {
          public static void main(String[] args) throws InterruptedException {
              ApiCaller caller = new ApiCaller();
              JSONArray allInstances = new JSONArray();
              allInstances.addAll(Arrays.asList("i-bp18hgfai8ekoqwo0***", "i-bp1ecbyds24ij63w1***"));
              while (! allInstances.isEmpty()) {
                  DescribeInstancesRequest request = new DescribeInstancesRequest();
                  request.setRegionId("cn-hangzhou");
                  request.setInstanceIds(allInstances.toJSONString());// Specify the ID of the instance and only query the instance whose ID has been specified.
                  DescribeInstancesResponse response = caller.doAction(request);
                  List<DescribeInstancesResponse.Instance> instanceList = response.getInstances();
                  if (instanceList ! = null && ! instanceList.isEmpty()) {
                      for (DescribeInstancesResponse.Instance instance : instanceList) {
                          System.out.println("result:instance:" + instance.getInstanceId() + ",was created in zone:" + instance.getZoneId());
                          if (instance.getOperationLocks() ! = null) {
                              for (DescribeInstancesResponse.Instance.LockReason lockReason : instance.getOperationLocks()) {
                                  System.out.println("instance: " + instance.getInstanceId() + "-->lockReason:" + lockReason.getLockReason() + ",vmStatus:" + instance.getStatus());
                                  if ("Recycling".equals(lockReason.getLockReason())) {
                                      // Return the recycle time of the instance and delete the ID of the recycled instance from the instance ID list.
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
        instance: i-bp1ecbyds24ij63w1***-->lockReason:Recycling,vmStatus:Stopped
        Preemptible instance will be recycled immediately, instance id: i-bp1ecbyds24ij63w1***
        ```


**Related topics**  


[DescribeRegions](/intl.en-US/API Reference/Regions/DescribeRegions.md)

[DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md)

[DescribeAvailableResource](/intl.en-US/API Reference/Regions/DescribeAvailableResource.md)

[DescribeInstanceTypes](/intl.en-US/API Reference/Instances/DescribeInstanceTypes.md)

[DescribeSpotPriceHistory](/intl.en-US/API Reference/Instances/DescribeSpotPriceHistory.md)

[CreateInstance](/intl.en-US/API Reference/Instances/CreateInstance.md)

[RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md)

