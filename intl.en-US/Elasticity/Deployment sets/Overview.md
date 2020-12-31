# Overview

A deployment set is a policy that controls the distribution of ECS instances and implements disaster recovery and business availability when ECS instances are created.

## Deployment policy

You can use a deployment set to distribute your ECS instances to different physical servers to ensure high business availability and set up underlying disaster recovery. When you create ECS instances in a deployment set, Alibaba Cloud will start the ECS instances on different physical servers within the specified region based on the deployment policy that you configured.

Deployment sets support the high availability policy:

-   When you use the high availability policy, all the ECS instances within your deployment set are strictly distributed across different physical servers within the specified region. The high availability policy applies to application architectures where several ECS instances must be isolated from each other. The policy significantly reduces the chances of service unavailability.
-   When you use the high availability policy, you may not be able to create an ECS instance when there is a supply shortage in the specified region. Furthermore, if the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled, pay-as-you-go instances may fail to start after they are stopped. If this problem occurs, we recommend that you wait a while and then try again or create a new instance.

## Deployment example

The following figure shows a typical example on how to use a deployment set to improve business reliability. In the deployment set, four ECS instances are distributed to four different physical servers.

![Deployment set overview](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8432909951/p57239.png)

If you want to achieve low-latency communication between ECS instances, we recommend that you make sure the network types of the instances are the same. For example, select the same VPC for the ECS instances when you create them.

## Billing

Deployment sets are free of charge, but you will be charged for the usage of ECS instances, disks, snapshots, images, and public bandwidth in deployment sets. For more information, see [Billing overview](/intl.en-US/Pricing/Billing overview.md).

## Limits

Before you use deployment sets, note that:

-   Deployment sets cannot be merged.
-   You cannot create preemptible instances in deployment sets.
-   You cannot create dedicated hosts in deployment sets.
-   When you create ECS instances in a deployment set, you can create up to seven ECS instances in each zone. This limit varies with your ECS usage. You can use the following formula to calculate the number of ECS instances that can be created in an Alibaba Cloud region: 7 × Number of zones.
-   Instances in the following instance families can be created in deployment sets: c6, g6, r6, hfc6, hfg6, hfr6, d2, d2s, d2c, c5, d1, d1ne, g5, hfc5, hfg5, i2, i2g, i1, ic5, r5, se1ne, sn1ne, and sn2ne. For more information about instance types and their performance, see [Instance families](/intl.en-US/Instance/Instance families.md).
-   Supply shortage may result in a failure to create an instance or restart a pay-as-you-go instance that is in the No Fees for Stopped Instances \(VPC-Connected\) state in a deployment set. For more information, see [No Fees for Stopped Instances \(VPC-Connected\)](/intl.en-US/Pricing/Billing methods/No Fees for Stopped Instances (VPC-Connected).md).

For more information about the limits and quotas of deployment sets, see the "Deployment set limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md).

## Operations

-   [Create a deployment set](/intl.en-US/Elasticity/Deployment sets/Create a deployment set.md)
-   [Create an ECS instance in a deployment set](/intl.en-US/Elasticity/Deployment sets/Create an ECS instance in a deployment set.md)
-   [Change the deployment set of an instance](/intl.en-US/Elasticity/Deployment sets/Change the deployment set of an instance.md)
-   [Manage deployment sets](/intl.en-US/Elasticity/Deployment sets/Manage deployment sets.md)
-   [Delete a deployment set](/intl.en-US/Elasticity/Deployment sets/Delete a deployment set.md)

## API operation

-   Create a deployment set: [CreateDeploymentSet](/intl.en-US/API Reference/Deployment sets/CreateDeploymentSet.md)
-   Add an instance to a deployment set or migrate an instance from one deployment set to another: [ModifyInstanceDeployment](/intl.en-US/API Reference/Dedicated hosts/ModifyInstanceDeployment.md).
-   Query deployment sets: [DescribeDeploymentSets](/intl.en-US/API Reference/Deployment sets/DescribeDeploymentSets.md).
-   Modify the attributes of a deployment set: [ModifyDeploymentSetAttribute](/intl.en-US/API Reference/Deployment sets/ModifyDeploymentSetAttribute.md).
-   Delete a deployment set: [DeleteDeploymentSet](/intl.en-US/API Reference/Deployment sets/DeleteDeploymentSet.md).

