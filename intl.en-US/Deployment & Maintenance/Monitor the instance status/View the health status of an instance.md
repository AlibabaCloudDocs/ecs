---
keyword: [instance health, Alibaba Cloud, ECS]
---

# View the health status of an instance

You can perform regular checks on an instance to monitor its health status. This topic describes how to view the health status of an instance by using the ECS console or calling API operations.

The health status of an instance is centered around network configuration exceptions, software failure, and hardware usage. The system can record network, software, or hardware problems of an instance in a timely manner by monitoring the health status of the instance,.

This feature can be used together with the metric monitoring feature of Cloud Monitor to dynamically customize the standard health level of computing resource maintenance. For more information, see [What is Cloud Monitor?](/intl.en-US/Product Introduction/What is Cloud Monitor?.md)

The following table describes the texts in the console and API parameter values that indicate the health status of instances.

|Text in the console|API parameter value|Description|Alert color in the console|
|:------------------|:------------------|:----------|:-------------------------|
|Passed|Ok|The instance has passed the health check.|Green|
|Impaired|Impaired|The instance performance is deteriorated.|Red|
|Warning|Warning|The instance performance is at risk and may decline due to maintenance or technical problems.|
|Maintaining System|Maintaining|The instance is under maintenance.|
|Initializing|Initializing|The instance is being initialized.|
|Insufficient Data|InsufficientData|The health status cannot be determined due to insufficient data.|
|No Status|NotApplicable|The instance health status is not applicable.|

## View the health status of an instance by using the ECS console

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance for which you want to view the health status and click the instance ID.

5.  In the upper-right corner of the **Instance Details** page, view the health status of the instance.


## View the health status of an instance by using Alibaba Cloud CLI

-   Run the following command to call the [DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md) and [DescribeInstancesFullStatus](/intl.en-US/API Reference/System event/DescribeInstancesFullStatus.md) operations to view the health status of a specific instance:

    ```
    aliyun ecs DescribeInstances --RegionId TheRegionId --output cols=InstanceId,InstanceName rows=Instances.Instance[]
    aliyun ecs DescribeInstancesFullStatus --RegionId TheRegionId --InstanceId.1 i-bp1afnc98r8k69\*\*\*\*\*\* --output cols=HealthStatus rows=InstanceFullStatusSet.InstanceFullStatusType[]
    ```

-   Run the following command to call the [DescribeInstancesFullStatus](/intl.en-US/API Reference/System event/DescribeInstancesFullStatus.md) operation to view the health status of all instances in a specific region. For more information about region IDs, see [Regions and zones]().

    ```
    aliyun ecs DescribeInstancesFullStatus --RegionId TheRegionId --output cols=HealthStatus rows=InstanceFullStatusSet.InstanceFullStatusType[]
    ```


After you submit a health check request, Alibaba Cloud returns the health check result for each instance included in the request.

-   If the health check succeeds, Ok is returned.
-   If the health check fails, other metrics are returned.

**Related topics**  


[DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md)

[DescribeInstancesFullStatus](/intl.en-US/API Reference/System event/DescribeInstancesFullStatus.md)

