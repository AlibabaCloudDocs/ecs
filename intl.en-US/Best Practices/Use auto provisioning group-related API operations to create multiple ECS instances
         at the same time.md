# Use auto provisioning group-related API operations to create multiple ECS instances at the same time

You can use ECS API operations to create multiple pay-as-you-go ECS instances at the same time. Compared with the RunInstances operation, the CreateAutoProvisioningGroup operation can help you create a large number of ECS instances at the same time in a simpler and more stable manner.

RunInstances is commonly used when your business requires you to create multiple pay-as-you-go ECS instances. You can call RunInstances to create up to 100 ECS instances at the same time. However, if more than 100 ECS instances are required to be created at the same time, you may encounter technical bottlenecks in use of RunInstances. For more information, see [Possible issues caused by using RunInstances](#section_6v8_ugx_6ro).

**Note:** If you are familiar with the technical bottlenecks caused by using RunInstances, you can skip the preceding section.

To meet your requirements of creating more than 100 ECS instances at the same time, Alibaba Cloud provides auto provisioning groups. You can call the CreateAutoProvisioningGroup operation to create an auto provisioning group and use the group to deploy an instance cluster across different billing methods, instance families, and zones within one click. CreateAutoProvisioningGroup is more suitable than RunInstances when you create a large number of ECS instances. For more information, see [Comparison between RunInstances and CreateAutoProvisioningGroup](#section_xtx_q9a_5s3) and [Benefits of auto provisioning groups](#section_1j8_ea0_iyf).

## Comparison between RunInstances and CreateAutoProvisioningGroup

The following table compares the features of the [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md) and [CreateAutoProvisioningGroup](/intl.en-US/API Reference/Auto provisioning group/CreateAutoProvisioningGroup.md) operations to help you choose an appropriate operation to create ECS instances.

|Item|RunInstances|CreateAutoProvisioningGroup|
|----|------------|---------------------------|
|Maximum number of instances that can be created at the same time|100.|1,000 \(up to 10,000 vCPUs\).|
|Capacity delivery form|Specific number of instances.|Specific number of instances, specific number of vCPUs, and instance types of different weights|
|Support for multiple zones|No.|Yes.|
|Support for multiple instance types|No.|Yes.|
|Support for multiple disk categories|No.|Yes.|
|Provision of policies that you can use to create instances|No.|Yes. The following policies are provided:-   For pay-as-you-go instances
    -   Cost optimization policy: The auto provisioning group selects the lowest-cost instance types from the candidate instance types to create instances.
    -   Priority-based policy: The auto provisioning group attempts to create instances based on the priorities configured for candidate instance types.
-   For preemptible instances
    -   Cost optimization policy: The auto provisioning group selects the lowest-cost instance types from the candidate instance types to create instances.
    -   Balanced distribution policy: The auto provisioning group evenly distributes instances across the specified zones.
    -   Capacity-optimized distribution policy: The auto provisioning group selects the optimal combinations of instance types and zones to create instances based on resource availability. |
|Delivery stability|Affected by resource availability.|Multiple combinations of instance types and zones reduce the impacts of resource availability.|
|Response method|Returns a response in real time.|Returns a response in real time.|

The following example scenarios show you how to use CreateAutoProvisioningGroup in place of RunInstances to create ECS instances:

-   Assume that you called the RunInstances operation to batch create instances of a single instance type in a single zone. When you call the CreateAutoProvisioningGroup operation instead to batch create instances, you need only to configure a combination of instance types and zones.
-   Assume that you manually configure a business deployment plan when you called the RunInstances operation to batch create instances. You can call the CreateAutoProvisioningGroup operation instead to deploy instances that have multiple categories of disks attached across multiple instance types and zones, based on different instance provisioning policies provided by Auto Provisioning.

    For example, you manually configured a business deployment plan that traversed multiple instance types and zones to create instances by calling the RunInstances operation. This improves the success rate of creating instances. If you call the CreateAutoProvisioningGroup operation instead to batch create a large number of instances, you need only to configure multiple combinations of instance types and zones, and select an appropriate policy. The created auto provisioning group automatically batch creates instances based on your configurations and policy.


**Note:** Limits apply to policies that are used for auto provisioning groups to create instances. A maximum of 1,000 instances can be created at the same time. If you specify the weight of each specified instance type by using the `WeightedCapacity` parameter, the maximum weighted capacity that is created one time is 10,000.

## Possible issues caused by using RunInstances

Due to the limits of the RunInstances operation, you may encounter the following issues when you call RunInstances to create instances.

|Issue|Description|Solution|
|-----|-----------|--------|
|A limited number of instances can be created at the same time.|You can call the RunInstances operation to create a maximum of 100 ECS instances at the same time.|If you want to create more than 100 ECS instances, you must call this operation multiple times in a recurring or concurrent manner.|
|The success rate of creating instances is not ensured.|You can call the RunInstances operation to create instances of a single instance type in a single zone. When you call this operation to create multiple ECS instances at the same time, you may encounter the following issues:-   Instances cannot be created due to insufficient resources of a specified instance type.
-   Instances of a specified instance type can no longer be created due to the retirement of the instance type.
-   Instances cannot be created because the specified instance type is unavailable in the specified zone.
-   Instances cannot be created because the specified instance type do not support specified disk categories.

|-   Instances cannot be created mostly due to insufficient resources. To solve this issue, we recommend that you call the [DescribeAvailableResource](/intl.en-US/API Reference/Regions/DescribeAvailableResource.md) operation to query available instance types in zones before you call the RunInstances operation to create ECS instances. You can manually configure multiple combinations of instance types and zones to have sufficient resources to create instances. The complex method of creating instances helps ensure high business delivery stability.

After you configure multiple combinations of instance types and zones, you must create an appropriate policy to create instances. For example, you can create 100 ECS instances in sequence based on multiple combinations that you configured. If only 50 ECS instances can be created by using the available resources provided by the first combination, you must use the second combination to create the remaining 50 ECS instances.

-   Instance types have limits. You can call the [DescribeAvailableResource](/intl.en-US/API Reference/Regions/DescribeAvailableResource.md) operation to query the limits. Then, you can develop fault tolerance solutions based on the limits to avoid the impacts caused by changes in limits.

**Note:** You can also learn about the limits of instance types based on the descriptions in documents about instance families. For more information, see [Instance families](/intl.en-US/Instance/Instance families.md).

Example scenario: The `ecs.g6e.large` instance type supports only the disk category of enhanced SSDs \(ESSDs\) and Beijing Zone X \(`cn-beijing-x`\) does not support ESSDs. |
|Simple policies that are used to create instances cannot meet diversified business requirements.|RunInstances can only be used to create instances of a single instance type in a single zone. If you need to deploy instances in multiple zones to implement geo-disaster recovery or create ECS instances at minimal costs, you must create a business deployment plan on your own to ensure that instances are deployed. A business deployment plan that you create on your own may have the following issues:-   High development costs. You may need to deal with a series of issues when you use the business deployment plan that you configured. For example, you may encounter issues about how to create ECS instances when resources are insufficient and how to ensure computing power at the lowest cost of preemptible instances when you scale up your servers.
-   Low stability and less professionalism. A business deployment plan that you built on your own for the resources provided by Alibaba Cloud is less likely to be built in a professional manner. You also cannot test the plan. This brings risks to the production environment.

|To resolve the issue, you may contact Alibaba Cloud for assistance.|

## Benefits of auto provisioning groups

Alibaba Cloud provides auto provisioning groups to address the issues that you may encounter when you call the RunInstances operation to create multiple ECS instances at the same time. Auto provisioning groups allow you to deploy an instance cluster across different billing methods, instance families, and zones within one click. Auto provisioning groups provide stable computing power, alleviate the instability caused by recycled preemptible instances, and eliminate the need to manually create instances. The following table describes the benefits of auto provisioning groups.

|Benefit|Description|
|-------|-----------|
|Allow you to create a large number of ECS instances at the same time.|You can use an auto provisioning group to create up to 1,000 ECS instances at the same time.|
|Allow you to create instances that have multiple categories of disks attached across instance types and zones.|Auto provisioning groups allow you to configure up to 10 combinations of instance types and zones, and allow you to select up to five disk categories. This ensures high availability when you create ECS instances at the same time.Example scenarios:

When you create ECS instances based on the balanced distribution policy provided by an auto provisioning group, you can configure multiple instance types and zones. As required by the policy, instances need to be created in a relatively balanced manner across zones. However, if the required number of instances cannot be created in a zone, the auto provisioning group attempts to create the same number of instances in other zones.

If you specify multiple disk categories, the auto provisioning group creates disks for instances based on the priorities of the disk categories, and changes a disk category if the disk category is unavailable.

**Note:** If all disk categories are unavailable, the auto provisioning group no longer uses this method but selects another creation method. |
|Support multiple policies to create instances|Auto provisioning groups provide the following policies to create instances:-   For pay-as-you-go instances
    -   Cost optimization policy: The auto provisioning group selects the lowest-cost instance types from the candidate instance types to create instances.
    -   Priority-based policy: The auto provisioning group attempts to create instances based on the priorities configured for candidate instance types.
-   For preemptible instances
    -   Cost optimization policy: The auto provisioning group selects the lowest-cost instance types from the candidate instance types to create instances.
    -   Balanced distribution policy: The auto provisioning group evenly distributes instances across the specified zones.
    -   Capacity-optimized distribution policy: The auto provisioning group selects the optimal combinations of instance types and zones to create instances based on resource availability. |
|Improve availability of preemptible instances|The demand for preemptible instances is increasing due to the advantages in prices of preemptible instances. However, the prices of preemptible instances fluctuate, and the instances are recycled when bidding prices become lower than current market prices after protection periods. This makes preemptible instances difficult to manage. Auto provisioning groups improve the availability of preemptible instances while low costs are maintained. The following items describe how to improve the availability of preemptible instances:-   You can use the default cost optimization policy. If you use this policy, the auto provisioning group attempts to create instances in ascending order of instance type prices each time the group scales out.
-   For preemptible instances, the resources based on instance types are different from those based on zones. You can configure multiple combinations of instances types and zones for preemptible instances to reduce the probability that no resources are available for all the combinations.
-   You can configure multiple disk categories when you create an auto provisioning group. This ensures that the system can select appropriate disk categories to create instances.
-   You can configure the `SpotInstancePoolsToUseCount` parameter to ensure that preemptible instances are created by using the lowest-cost combinations of instance types and zones. This can avoid the issue that computing power significantly reduces when instances of an instance type are recycled. |

## Best practices for creating auto provisioning groups by calling CreateAutoProvisioningGroup

This section provides the sample Java code that is used to create an auto provisioning group \(CreateAutoProvisioningGroup\). This section also describes how to call the CreateAutoProvisioningGroup operation.

1.  Install ECS SDK for Java and the Alibaba Cloud SDK core library.

    For more information, see [Install ECS SDK for Java](/intl.en-US/SDK Reference/Java example/Install ECS SDK for Java.md).

2.  Write the Java code that is used to call the CreateAutoProvisioningGroup operation.

    Sample code:

    ```
    CreateAutoProvisioningGroupRequest request = new CreateAutoProvisioningGroupRequest();
    request.setRegionId(regionId);
    request.setLaunchConfigurationImageId(RequestHelper.IMAGE_ID);
    request.setLaunchConfigurationSecurityGroupId(securityGroupId);
    
    request.setTotalTargetCapacity(totalTargetCapacity);
    request.setPayAsYouGoTargetCapacity(payAsYouGoTargetCapacity);
    request.setSpotTargetCapacity(spotTargetCapacity);
    request.setLaunchConfigurationSystemDiskCategory("cloud_ssd");
    request.setLaunchConfigurationSystemDiskSize(40);
    request.setAutoProvisioningGroupType("instant");
    // Configure the policy that is used to create preemptible instances.
    request.setSpotAllocationStrategy("lowest-price");
    request.setSpotInstancePoolsToUseCount(spotInstancePoolsToUseCount);
    // Configure the policy that is used to create pay-as-you-go instances.
    request.setPayAsYouGoAllocationStrategy("prioritized");
    request.setMaxSpotPrice(maxSpotPrice);
    // Configure a maximum of 10 combinations of instance types and zones.
    request.setLaunchTemplateConfigs(launchTemplateConfigs);
    request.setClientToken(clientToken);
    CreateAutoProvisioningGroupResponse response = client.getAcsResponse(request);
    ```

    Sample response in the JSON format:

    ```
    {
        "autoProvisioningGroupId":"apg-****",
        "launchResults":[
            {
                "instanceIds":[
                    "i-****"
                ],
                "instanceType":"ecs.c5.large",
                "spotStrategy":"NoSpot",
                "zoneId":"cn-shanghai-b"
            },
           {
                "instanceIds":[],
                "instanceType":"ecs.c5.large",
                "spotStrategy":"NoSpot",
                "zoneId":"cn-shanghai-b",
                "errorCode" : "Invalid.Parameter",
                "errorMsg" : "Specific Parameter 'imageId' is not valid"
            }
        ],
        "requestId":"20DA1E9F-BF7F-4BE7-8204-E4DE58E4FC7B"
    }
    ```

    When you call the CreateAutoProvisioningGroup operation to create an auto provisioning group, you need only to configure items that are used to create a large number instances at the same time, without the need to worry about the creation process. The auto provisioning group creates instances in a diligent manner.

    **Note:** If instances are created in a diligent manner, the system attempts to create instances by using another combination of instance types and zones when instances cannot be created by using one combination. This method requires more time to create instances. In addition, the actual creation result may deviate from the creation policy that you configured.


**Related topics**  


[Auto Provisioning overview](/intl.en-US/Elasticity/Manage auto provisioning groups/Auto Provisioning overview.md)

[Configure an auto provisioning group](/intl.en-US/Elasticity/Manage auto provisioning groups/Configure an auto provisioning group.md)

