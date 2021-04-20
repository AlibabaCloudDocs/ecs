---
keyword: [itemized billing, batch, retrieve, tag, ECS]
---

# Overview

Tags can be used to identify resources. Tags allow enterprises and individuals to categorize their ECS resources and simplify the search and management of resources.

## Scenarios

Tags can make your search more efficient and allow you to perform batch operations on resources. For example:

-   You can bind different tags to environments such as production and test environments, operating systems such as Windows and Linux, and mobile platforms such as iOS and Android. For example, create the `Test:Server-Windows` tag and bind this tag to all the Windows ECS instances that are in the test environment. You can find these instances based on the tag and perform batch operations on these instances.

    ![Example 2 of tag usage scenarios](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7727948951/p76664.png)

    Examples of batch operations:

    -   Replace the image to deploy applications.
    -   Upgrade patches.
    -   Create security group rules to control access.
    -   Use Operation Orchestration Service \(OOS\) to batch start, stop, or restart ECS instances.
    -   Use Cloud Assistant to run an O&M script on multiple ECS instances.
-   In team or project management, you can add tags such as `CostCenter:aliyun` to groups, projects, or departments. Then, you can categorize the objects, and implement itemized billing and cross authorization based on tags on the Billing Management page of the ECS console.

    ![Example of tag usage scenarios](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7727948951/p76662.png)

    For more information, see the following topics:

    -   [Create a resource with a specific tag](/intl.en-US/Tag & Resource/Tags/Create a resource with a specific tag.md)
    -   [Control access to resources by using tags](/intl.en-US/Tag & Resource/Tags/Control access to resources by using tags.md)
    -   [Use tags to grant access to a group of ECS instances](/intl.en-US/Tutorials/Use tags to grant access to a group of ECS instances.md)

## Precautions

-   Each tag consists of a key-value pair.
-   A tag must have a unique tag key.

    For example, an ECS instance is bound to the `city:shanghai` tag. If the instance is subsequently bound to the `city:newyork` tag, the `city:shanghai` tag is automatically unbound from the instance.

-   Tag information is not shared across regions. For example, tags created in the China \(Hangzhou\) region are not visible to the China \(Shanghai\) region.
-   Tags are deleted when they are not bound to any resources.
-   For more information about the best practices for tag design, see [Best practices for tag design](/intl.en-US/Best Practices/Best practices for tag design.md).

## Limits

For more information about limits and quotas of tags, see the "Tag limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md).

## Services that support tags

The following table lists Alibaba Cloud services and resources that support tags.

|Service|Resource|API operation|
|-------|--------|-------------|
|Elastic Compute Service \(ECS\)|-   ECS instance
-   Reserved instance
-   Elastic Block Storage \(EBS\)
-   Snapshot
-   Automatic snapshot policy
-   Image
-   Security group
-   Elastic network interface \(ENI\)
-   Dedicated host
-   SSH key pair
-   Launch template

|-   Bind a tag: [TagResources](/intl.en-US/API Reference/Tags/TagResources.md)
-   Unbind a tag: [UntagResources](/intl.en-US/API Reference/Tags/UntagResources.md)
-   Search for resources based on tags: [ListTagResources](/intl.en-US/API Reference/Tags/ListTagResources.md) |
|Auto Scaling|Scaling group|-   Bind a tag: [TagResources](/intl.en-US/API Reference/Tag management/TagResources.md)
-   Unbind a tag: [UntagResources](/intl.en-US/API Reference/Tag management/UntagResources.md)
-   Search for resources based on tags: [ListTagResources](/intl.en-US/API Reference/Tag management/ListTagResources.md) |
|Virtual Private Cloud \(VPC\)|-   VPC
-   VSwitch
-   Route table
-   Elastic IP address \(EIP\)

|-   Bind a tag: [TagResources](/intl.en-US/API reference/Tags/TagResources.md)
-   Unbind a tag: [UnTagResources](/intl.en-US/API reference/Tags/UnTagResources.md)
-   Search for resources based on tags: [ListTagResources](/intl.en-US/API reference/Tags/ListTagResources.md) |
|ApsaraDB for Redis|ApsaraDB for Redis instance|-   Bind a tag: [TagResources](/intl.en-US/API Reference/Tags/TagResources.md)
-   Unbind a tag: [UntagResources](/intl.en-US/API Reference/Tags/UntagResources.md)
-   Search for resources based on tags: [ListTagResources](/intl.en-US/API Reference/Tags/ListTagResources.md) |
|Alibaba Cloud Content Delivery Network \(CDN\)|Domain name|-   Bind a tag: [TagResources](/intl.en-US/New API Reference/Tag management operations/TagResources.md)
-   Unbind a tag: [UntagResources](/intl.en-US/New API Reference/Tag management operations/UntagResources.md)
-   Query the tags of the current user: [DescribeUserTags](/intl.en-US/New API Reference/Tag management operations/DescribeUserTags.md)
-   Search for resources based on tags: [DescribeTagResources](/intl.en-US/New API Reference/Tag management operations/DescribeTagResources.md) |
|Key Management Service \(KMS\)|Customer master key \(CMK\)|-   Bind a tag: [TagResource](/intl.en-US/API Reference/Tag/TagResource.md)
-   Unbind a tag: [UntagResource](/intl.en-US/API Reference/Tag/UntagResource.md)
-   Search for resources based on tags: [ListResourceTags](/intl.en-US/API Reference/Tag/ListResourceTags.md) |
|Apsara PolarDB|Cluster|-   Bind a tag: [TagResources](/intl.en-US/API Reference/Tag management/TagResources.md)
-   Unbind a tag: [UntagResources](/intl.en-US/API Reference/Tag management/UntagResources.md) |
|Object Storage Service \(OSS\)|Bucket|Add, delete, modify, or query tags for a bucket: [bucket-tagging](/intl.en-US/Tools/ossutil/Common commands/bucket-tagging.md)|
|ApsaraDB for RDS|ApsaraDB for RDS instance|-   Bind a tag: [Create and bind tags](/intl.en-US/API Reference/Tag management/Create and bind tags.md)
-   Unbind a tag: [Unbind tags](/intl.en-US/API Reference/Tag management/Unbind tags.md)
-   Search for resources based on tags: [Query tags](/intl.en-US/API Reference/Tag management/Query tags.md) |
|AnalyticDB for PostgreSQL|AnalyticDB for PostgreSQL instance|Query resources based on tags: [DescribeDBInstances](/intl.en-US/API Reference/Instance management/DescribeDBInstances.md)|
|Cloud Enterprise Network \(CEN\)|CEN instance|-   Bind a tag: [TagResources]()
-   Unbind a tag: [UntagResources]()
-   Search for resources based on tags: [DescribeCens]() |
|Smart Access Gateway \(SAG\)|Cloud Connect Network \(CCN\)|Query resources based on tags: [DescribeCloudConnectNetworks](/intl.en-US/API Reference/Cloud Connect Network/DescribeCloudConnectNetworks.md)|
|Operation Orchestration Service \(OOS\)|-   OOS template
-   OOS operation tasks

|-   Bind a tag: [TagResources]()
-   Unbind a tag: [UntagResources]()
-   Search for resources based on tags: [ListTagResources]() |

