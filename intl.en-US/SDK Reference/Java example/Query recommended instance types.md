# Query recommended instance types

This topic describes how to call the DescribeRecommendInstanceType operation by using Alibaba Cloud Elastic Compute Service \(ECS\) SDK for Java to query recommended or alternative instance types. This topic also elaborates the best practices for calling the RunInstances and DescribeRecommendInstanceType operations.

The version of Alibaba Cloud ECS SDK for Java is 4.23.8 or later.

## Scenarios

-   Scenario 1: Before you create ECS instances, you can call the [DescribeRecommendInstanceType]() operation by specifying the number of vCPUs \(Cores\), memory size \(Memory\), and policy for recommending instance types \(PriorityStrategy\) to query recommended instance types. You can set the PriorityStrategy parameter to InventoryFirst, PriceFirst, or NewProductFirst. The system then recommends the instance types that match your specified filter conditions. For the sample code used to call the operation in this scenario, see [Query recommended instance types that have the specified number of vCPUs and memory size](#section_b4h_a7i_kag).
-   Scenario 2: Before you create ECS instances, you can call the [DescribeRecommendInstanceType]() operation by specifying an instance type to query alternative instance types. If an error occurs when you create ECS instances, you can change the instance type to a queried alternative instance type. The error may be that resources of the specified instance type are insufficient, that the specified instance type is retired, and that the instance type is unavailable within the specified region. For the sample code used to call the operation in this scenario, see [Query alternative instance types for a specified instance type](#section_xbs_yme_mg2).
-   Scenario 3: If an error such as insufficient resources of the specified instance type occurs when you call the [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md) operation to create ECS instances, you can call the [DescribeRecommendInstanceType]() operation to query alternative instance types. Then, you can call the RunInstances operation again to create ECS instances of a queried alternative instance type. For the complete sample code used to call the operation in this scenario, see [Best practices for creating ECS instances of alternative instance types](#section_7qm_wd7_nnk).

**Note:** The sample code provided for these scenarios are for reference only. In actual operations, adjust the parameter settings based on your needs.

## Query recommended instance types that have the specified number of vCPUs and memory size

The following sample code provides an example on how to call the DescribeRecommendInstanceType operation to query recommended enterprise-level instance types that have two vCPUs and 4 GiB of memory in the Hangzhou `G` zone. Sample code of the `void` method:

```
public void getRecommendInstanceTypeWithCoresAndMemory() throws ClientException {
    // Create and initialize a DefaultAcsClient instance. 
    DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<yourAccessKeyID>", "<yourAccessKeySecret>");
    IAcsClient client = new DefaultAcsClient(profile);

    // Create an API request and configure the parameters. 
    DescribeRecommendInstanceTypeRequest request = new DescribeRecommendInstanceTypeRequest();
    // Set NetworkType to vpc. 
    request.setNetworkType("vpc");
    // Set IoOptimized to optimized. 
    request.setIoOptimized("optimized");
    // Set InstanceChargeType to PostPaid. 
    request.setInstanceChargeType("PostPaid");
    // Set SpotStrategy to NoSpot. 
    request.setSpotStrategy("NoSpot");
    // Specify the number of vCPUs and memory size. 
    request.setCores(2);
    request.setMemory(4.0f);
    // Set InstanceFamilyLevel to EnterpriseLevel. 
    request.setInstanceFamilyLevel("EnterpriseLevel");
    // Specify the instance families of the recommended instance types. 
    request.setInstanceTypeFamilys(Arrays.asList("ecs.c6","ecs.c5","ecs.hfc5","ecs.hfc6","ecs.sn1ne"));
    // Specify the zone ID of the recommended instance types. The zone must be that of the vSwitch specified by the VSwitchId parameter when you create ECS instances. 
    request.setZoneId("cn-hangzhou-g");
    // If ZoneMatchMode is set to Strict, the query is restricted to the zone specified by ZoneId. 
    // If ZoneMatchMode is set to Include, the query is not restricted to the zone specified by ZondId. Matching instance types in the specified zone are preferentially recommended. If no matching instance types are found in the specified zone, instance types are recommended from all the zones of the same region. 
    request.setZoneMatchMode("Strict");
    // Set PriorityStrategy to InventoryFirst, which indicates that instance types are recommended in descending order of resource availability. If you want instance types to be recommended based on prices, set PriorityStrategy to PriceFirst. 
    request.setPriorityStrategy("InventoryFirst");

    // Obtain the response. 
    DescribeRecommendInstanceTypeResponse response = client.getAcsResponse(request);
    DescribeRecommendInstanceTypeResponse.RecommendInstanceType recommendType = null;
    if(response != null && response.getData().size() != 0){
        recommendType = response.getData().get(0);
    }
    if(recommendType != null) {
        // If matching instance types are found, the information of the instance types is returned, such as the names, zones, regions, billing methods, and bidding policies. 
        System.out.println("recommend instanceType: " + recommendType.getInstanceType().getInstanceType());
        System.out.println("recommend zoneId: " + recommendType.getZoneId());
        System.out.println("recommend regionId: " + recommendType.getRegionId());
        System.out.println("recommend chargeType: " + recommendType.getInstanceChargeType());
        System.out.println("recommend spotStrategy: " + recommendType.getSpotStrategy());
    }else {
        // If no matching instance types are found, a message that indicates no resources are available is returned. 
        System.out.println("no available instanceType");
    }
}
```

Use the `main` method to call the `getRecommendInstanceTypeWithCoresAndMemory` method. The matching instance types are returned. Sample response:

![DescribeRecommendInstanceType](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6579733261/p243060.png)

## Query alternative instance types for a specified instance type

The following sample code provides an example on how to call the DescribeRecommendInstanceType operation to query alternative instance types recommended for ecs.c6.large that belong to specified instance families and have sufficient resources in the Hangzhou `G` zone. Sample code of the `void` method:

**Note:** The number of vCPUs \(`Cores`\) and memory size \(`Memory`\) of returned alternative instance types may be different from those of the specified instance type. For example, when resources of the ecs.mn4.small instance type that has one vCPU and 4 GiB of memory are insufficient, the ecs.n4.small instance type that has one vCPU and 2 GiB of memory may be returned as an alternative.

```
public void getRecommendInstanceType() throws ClientException {
    // Create and initialize a DefaultAcsClient instance. 
    DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<yourAccessKeyID>", "<yourAccessKeySecret>");
    IAcsClient client = new DefaultAcsClient(profile);

    // Create an API request and configure the parameters. 
    DescribeRecommendInstanceTypeRequest request = new DescribeRecommendInstanceTypeRequest();
    // Set NetworkType to vpc. 
    request.setNetworkType("vpc");
    // Set IoOptimized to optimized. 
    request.setIoOptimized("optimized");
    // Set InstanceChargeType to PostPaid. 
    request.setInstanceChargeType("PostPaid");
    // Set SpotStrategy to NoSpot. 
    request.setSpotStrategy("NoSpot");
    // Specify an instance type. 
    request.setInstanceType("ecs.c6.large");
    // Specify the instance families of the alternative instance types. 
    request.setInstanceTypeFamilys(Arrays.asList("ecs.c6","ecs.c5","ecs.hfc5","ecs.hfc6","ecs.sn1ne"));
    // Specify the zone ID of the alternative instance types. The zone must be that of the vSwitch specified by the VSwitchId parameter when you create ECS instances. 
    request.setZoneId("cn-hangzhou-g");
    // If ZoneMatchMode is set to Strict, the query is restricted to the zone specified by ZoneId. 
    // If ZoneMatchMode is set to Include, the query is not restricted to the zone specified by ZondId. Matching instance types in the specified zone are preferentially recommended. If no matching instance types are found in the specified zone, instance types are recommended from all the zones of the same region. 
    request.setZoneMatchMode("Strict");
    // Set PriorityStrategy to InventoryFirst, which indicates that instance types are recommended in descending order of resource availability. If you want instance types to be recommended based on prices, set PriorityStrategy to PriceFirst. 
    request.setPriorityStrategy("InventoryFirst");

    // Obtain the response. 
    DescribeRecommendInstanceTypeResponse response = client.getAcsResponse(request);
    DescribeRecommendInstanceTypeResponse.RecommendInstanceType recommendType = null;
    if(response != null && response.getData().size() != 0){
        recommendType = response.getData().get(0);
    }
    if(recommendType != null) {
        // If matching instance types are found, the information of the instance types is returned, such as the names, zones, regions, billing methods, and bidding policies. 
        System.out.println("recommend instanceType: " + recommendType.getInstanceType().getInstanceType());
        System.out.println("recommend zoneId: " + recommendType.getZoneId());
        System.out.println("recommend regionId: " + recommendType.getRegionId());
        System.out.println("recommend chargeType: " + recommendType.getInstanceChargeType());
        System.out.println("recommend spotStrategy: " + recommendType.getSpotStrategy());
    }else {
        // If no matching instance types are found, a message that indicates no resources are available is returned. 
        System.out.println("no available instanceType");
    }
}
```

Use the `main` method to call the `getRecommendInstanceType` method. The matching instance types are returned. Sample response:

![DescribeRecommendInstanceType](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6579733261/p243060.png)

## Best practices for creating ECS instances of alternative instance types

If an error such as insufficient resources of the specified instance type occurs when you call the RunInstances operation to create ECS instances, you can call the DescribeRecommendInstanceType operation to query alternative instance types. Then, you can call the RunInstances operation again to create ECS instances of a queried alternative instance type.

**Note:** The number of vCPUs \(`Cores`\) and memory size \(`Memory`\) of returned alternative instance types may be different from those of the specified instance type. You can use the `InstanceTypeFamily` parameter to specify the instance families of alternative instance types. For example, when resources of the ecs.mn4.small instance type that has one vCPU and 4 GiB of memory are insufficient, the ecs.n4.small instance type that has one vCPU and 2 GiB of memory may be returned as an alternative. Make sure that you have no strict requirements on instance types.

In the sample code, the following parameter settings are used:

-   InternetChargeType: specifies the billing method for network usage. Set InternetChargeType to PayByTraffic.
-   InstanceChargeType: specifies the instance billing method. Set InstanceChargeType to PostPaid.
-   NetworkType: specifies the network type of the instance. Set NetworkType to vpc. In this case, the `VSwitchId` parameter is required.

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.alibaba.fastjson.JSON;
import java.util.*;
import java.util.UUID;
import com.aliyuncs.ecs.model.v20140526.*;
public class RunInstances {
    public static void main(String[] args) throws ClientException {
        // Create and initialize a DefaultAcsClient instance. 
        DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<yourAccessKeyID>", "<yourAccessKeySecret>");
        IAcsClient client = new DefaultAcsClient(profile);

        // Create an API request and configure the parameters. 
        RunInstancesRequest request = new RunInstancesRequest();
        request.setRegionId("cn-hangzhou");
        request.setImageId("centos_8_2_x64_20G_alibase_20201120.vhd");
        request.setInstanceType("ecs.hfg5.large");
        request.setSecurityGroupId("sg-bp17lchxr133z9gt****");
        // Specify the ID of a vSwitch. In this sample code, no zone ID is specified. In this case, the instances are created within the zone of the specified vSwitch. 
        request.setVSwitchId("vsw-bp1hl0stgh7jq4rsm****");
        request.setInstanceName("MyFirstEcsInstance");
        request.setDescription("MyFirstEcsInstance");
        request.setInternetMaxBandwidthOut(2);
        request.setInternetChargeType("PayByTraffic");
        request.setClientToken(UUID.randomUUID().toString());
        // Attach a 100 GiB standard SSD as a data disk to the instance, and enable the Release Disk with Instance feature for the disk. 
        List<RunInstancesRequest.DataDisk> dataDiskList = new ArrayList<RunInstancesRequest.DataDisk>();
        RunInstancesRequest.DataDisk dataDisk1 = new RunInstancesRequest.DataDisk();
        dataDisk1.setSize(100);
        dataDisk1.setCategory("cloud_efficiency");
        dataDisk1.setDeleteWithInstance(true);
        dataDiskList.add(dataDisk1);
        request.setDataDisks(dataDiskList);
        // Batch create five ECS instances. If Amount is not set, one ECS instance is created. 
        // request.setAmount(5);
        // Specify the minimum number of instances to create if resources are insufficient. 
        // request.setMinAmount(2);
        // Add tags to the ECS instances. 
        List<RunInstancesRequest.Tag> tagList = new ArrayList<RunInstancesRequest.Tag>();
        RunInstancesRequest.Tag tag1 = new RunInstancesRequest.Tag();
        tag1.setKey("TestKey");
        tag1.setValue("TestValue");
        tagList.add(tag1);
        request.setTags(tagList);
        // Enable the dry run feature to check the validity of the request without making the request. The check items include the request format, service limits, resource availability, and whether the specified parameters are valid. 
        // After you set DryRun, you must set Amount to 1 and leave MinAmount empty. In the sample code, DryRun is set to true, which indicates that the request is checked but not made. You can modify the code based on your needs. 
        request.setDryRun(true);
        request.setInstanceChargeType("PostPaid");

        // Initiate the request and handle the response or exceptions. 
        RunInstancesResponse response;
        try {
            response = client.getAcsResponse(request);
            System.out.println(JSON.toJSONString(response));
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            System.out.println("ErrCode:" + e.getErrCode());
            System.out.println("ErrMsg:" + e.getErrMsg());
            System.out.println("RequestId:" + e.getRequestId());
            // Specify a list named noStockCode to match the returned error codes and determine whether to replace the instance type. 
            List<String> noStockCode = Arrays.asList("OperationDenied.NoStock","Zone.NotOnSale","InvalidResourceType.NotSupported","InstanceType.Offline");
            // Query alternative instance types if one of the specified error codes is returned. 
            if(noStockCode.contains(e.getErrCode())){
                DescribeRecommendInstanceTypeRequest request1 = new DescribeRecommendInstanceTypeRequest();
                // Specify the network type of the instance. If VswitchId is specified, set NetworkType to vpc. 
                if((request.getVSwitchId()).length()!=0){
                    request1.setNetworkType("vpc");
                }
                // Specify the policy for recommending instance types. By default, instance types are recommended in descending order of resource availability. 
                request1.setPriorityStrategy("InventoryFirst");
                // Set instance-related parameters to the same values as those used to create ECS instances. 
                request1.setIoOptimized(request.getIoOptimized());
                request1.setInstanceChargeType(request.getInstanceChargeType());
                request1.setSpotStrategy(request.getSpotStrategy());
                request1.setMaxPrice(request.getSpotPriceLimit());
                request1.setInstanceType(request.getInstanceType());
                // Specify the instance families of the recommended instance types. 
                request1.setInstanceTypeFamilys(Arrays.asList("ecs.g5","ecs.g6","ecs.g6e","ecs.hfc5","ecs.hfg7","ecs.sn1ne"));
                String zoneId = request.getZoneId();
                // Set ZoneId to the zone of the specified vSwitch. 
                if((request.getVSwitchId()).length()!=0){
                    DescribeVSwitchesRequest request2 = new DescribeVSwitchesRequest();
                    request2.setVSwitchId(request.getVSwitchId());
                    request2.setRegionId(request.getRegionId());
                    DescribeVSwitchesResponse response2 = client.getAcsResponse(request2);
                    if(response2 != null){
                        zoneId = response2.getVSwitches().get(0).getZoneId();
                    }
                }
                request1.setZoneId(zoneId);
                // If you want the query to be restricted to the specified zone, set ZoneMatchMode to Strict. 
                if((zoneId).length()!=0){
                    request1.setZoneMatchMode("Strict");
                }

                // Obtain the response. 
                DescribeRecommendInstanceTypeResponse response1 = client.getAcsResponse(request1);
                DescribeRecommendInstanceTypeResponse.RecommendInstanceType recommendType = null;
                if(response1 != null && response1.getData().size() != 0){
                    // Query details of the original instance type. 
                    DescribeInstanceTypesRequest typeRequest = new DescribeInstanceTypesRequest();
                    typeRequest.setInstanceTypess(Arrays.asList(request.getInstanceType()));
                    typeRequest.setRegionId(request.getRegionId());
                    DescribeInstanceTypesResponse typeResponse = client.getAcsResponse(typeRequest);
                    DescribeInstanceTypesResponse.InstanceType originType = null;
                    if(typeResponse != null && typeResponse.getInstanceTypes().size() != 0){
                        originType = typeResponse.getInstanceTypes().get(0);
                    }
                    for(DescribeRecommendInstanceTypeResponse.RecommendInstanceType type: response1.getData()){
                        if(request.getInstanceType().equals(type.getInstanceType())){
                            continue;
                        }
                        // You can add some filter conditions to narrow down the query results. For example, you can specify the number of vCPUs and memory size to query alternative instance types that have the same number of vCPUs and memory size as the original instance type. 
                        if(originType != null && originType.getCpuCoreCount().equals(type.getInstanceType().getCores())
                                && type.getInstanceType().getMemory().equals(originType.getMemorySize() * 1024)){
                            recommendType = type;
                            break;
                        }
                    }
                }
                // Display information of alternative solutions. 
                System.out.println("Alternative solutions:");
                System.out.println("recommend instanceType: " + recommendType.getInstanceType().getInstanceType());
                System.out.println("recommend zoneId: " + recommendType.getZoneId());
                System.out.println("recommend regionId: " + recommendType.getRegionId());
                System.out.println("recommend chargeType: " + recommendType.getInstanceChargeType());
                System.out.println("recommend spotStrategy: " + recommendType.getSpotStrategy());
                // Replace the instance type in the request to create ECS instances. 
                request.setInstanceType(recommendType.getInstanceType().getInstanceType());
                // Replace the zone ID in the request to create ECS instances. 
                request.setZoneId(recommendType.getZoneId());
                request.setSystemDiskCategory("cloud_essd");

                response = client.getAcsResponse(request);
                System.out.println("Response in the JSON format to the request to create ECS instances of an alternative instance type");
                System.out.println(JSON.toJSONString(response));
            }
        }
    }
}
```

-   The following figure shows a sample response when `DryRun` is set to true in a RunInstances request to create ECS instances.

    ![DescribeRecommendInstanceType2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6579733261/p243127.png)

-   The following figure shows a sample response when `DryRun` is set to false in the RunInstances request to create ECS instances of an alternative instance type.

    ![runinstances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6579733261/p259045.png)


**Related topics**  


[DescribeRegions](/intl.en-US/API Reference/Regions/DescribeRegions.md)

[DescribeZones](/intl.en-US/API Reference/Regions/DescribeZones.md)

[DescribeImages](/intl.en-US/API Reference/Images/DescribeImages.md)

[DescribeSecurityGroups](/intl.en-US/API Reference/Security groups/DescribeSecurityGroups.md)

[DescribeVSwitches](/intl.en-US/API reference/VSwitch/DescribeVSwitches.md)

