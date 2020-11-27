---
keyword: [quota, ECS quotas, insufficient ECS quotas, quota, ECS quota, upper limits for ECS resources, ECS usage limits, ECS limits, ECS resource quotas]
---

# Limits

This topic describes the limits on ECS and how to apply for extensions on some limits.

## Overview

ECS has the following limits:

-   You cannot install virtualization software such as VMware Workstation or use ECS instances for secondary virtualization. Only ECS bare metal instances and Super Computing Clusters \(SCCs\) support secondary virtualization.
-   ECS does not support sound card applications.
-   External hardware devices such as hardware dongles, USB flash drives, external hard disks, and hardware tokens, cannot be directly attached to ECS instances. Software verification methods such as two-factor authentication and dynamic passwords can be used.
-   ECS does not support multicast protocols. We recommend that you use unicast protocols instead.
-   Log Service does not support 32-bit Linux ECS instances.

    For information about the ECS instances that support Log Service, see [Logtail overview](/intl.en-US/Data Collection/Logtail collection/Overview/Logtail overview.md).

-   To apply for ICP filings for websites that are deployed on your ECS instance, make sure that the instance meets ICP filing requirements. You can apply for a limited number of ICP filing service numbers for each ECS instance. For more information, see [Prepare and check the instance and access information]().

## View quotas

You can click **Privileges** on the **Overview** page of the ECS console, and select a region to view the resource usage and quotas in that region. If the quota for a resource type is insufficient, submit a ticket to request a quota increase. For more information about how to view privileges and quotas, see [View quotas \(old version\)](/intl.en-US/Tag & Resource/Resource/View quotas (old version).md) or [DescribeAccountAttributes](/intl.en-US/API Reference/Others/DescribeAccountAttributes.md).

## Instance limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Permissions to create an ECS instance|To create an ECS instance within a region in mainland China, you must first complete real-name verification.|None.|
|Instance types that can be used to create pay-as-you-go instances|Instance types that have less than 16 vCPUs.|Submit a ticket.|
|Quota for vCPUs available for pay-as-you-go instances per region in an account|50 vCPUs|Submit a ticket.|
|Quota for vCPUs available for preemptible instances per region in an account|Submit a ticket to apply for a quota of up to 50 vCPUs.|Submit a ticket.|
|Quota for instance launch templates per region in an account|30|None.|
|Quota for versions for an instance launch template|30|None.|
|Permissions to change the billing method from pay-as-you-go to subscription|The following instance types or families do not support billing method changes: t1, s1, s2, s3, c1, c2, m1, m2, n1, n2, and e3.|None.|
|Permissions to change the billing method from subscription to pay-as-you-go|-   Whether you have these permissions depends on your ECS usage.
-   5,000 vCPUs × Number of hours per month.
-   The billing method change from subscription to pay-as-you-go may result in a refund. Each account is limited to a maximum monthly refund amount. The actual refund details are displayed on the Switch to Pay-As-You-Go page in the ECS console.

|None.|

## Reserved instance limits

|Item|Limit|Adjustable|
|----|-----|----------|
|Quota for regional reserved instances in an account|20|Submit a ticket.|
|Quota for zonal reserved instances per zone in an account|20|Submit a ticket.|
|Instance families that support reserved instances|sn1ne, sn2ne, se1ne, ic5, c5, g5, r5, c6, g6, r6, i2, i2g, hfc5, hfg5, and t5 **Note:** The t5 instance family supports only zonal reserved instances.

|None.|

**Note:** For more information, see the "Limits" section in [Reserved instance overview](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Reserved instance overview.md).

## Elastic Block Storage limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Permissions to create a pay-as-you-go disk|You must complete real-name verification before you can create a disk within a region in mainland China.|None.|
|Quota for pay-as-you-go disks in all regions for an account|This quota is calculated by using the following formula: Number of ECS instances across all regions × 5. A minimum of ten pay-as-you-go disks can be created in each account.|Submit a ticket.|
|Quota for system disks on an instance|1|None.|
|Quota for data disks on an instance|16 \(including cloud disks and Shared Block Storage devices\)|None.|
|Quota for instances to which a Shared Block Storage device can be attached|8|None.|
|Quota for Shared Block Storage devices in all regions for an account|10|Submit a ticket.|
|Capacity of a basic disk|5 GiB to 2,000 GiB|None.|
|Capacity of a standard SSD|20 GiB to 32,768 GiB|None.|
|Capacity of an ultra disk|20 GiB to 32,768 GiB|None.|
|Capacity of an enhanced SSD \(ESSD\)|20 GiB to 32,768 GiB|None.|
|Capacity of a local SSD|5 GiB to 800 GiB|None.|
|Total capacity of all local SSDs on an instance|1,024 GiB|None.|
|Capacity of a local NVMe SSD|1,456 GiB|None.|
|Total capacity of all local NVMe SSDs on an instance|2,912 GiB|None.|
|Capacity of a local SATA HDD|5,500 GiB|None.|
|Total capacity of all local SATA HDDs on an instance|154, 000 GiB|None.|
|Capacity of a Shared SSD Block Storage device|32,768 GiB|None.|
|Total capacity of all Shared SSD Block Storage devices on an instance|128 TiB|None.|
|Capacity of a Shared Ultra Block Storage device|32, 768 GiB|None.|
|Total capacity of all Shared Ultra Block Storage devices on an instance|128 TiB|None.|
|Capacity of a system disk|-   Windows Server: 40 GiB to 500 GiB
-   CoreOS and FreeBSD: 30 GiB to 500 GiB
-   Linux systems excluding CoreOS: 20 GiB to 500 GiB

|None.|
|Permissions to attach new local disks to instances that are equipped with local disks|Not allowed.|None.|
|Permissions to change configurations of instances that are equipped with local disks|Only bandwidth configurations of instances that are equipped with local disks can be changed.|None.|
|Mount points of system disks|/dev/vda|None.|
|Mount points of data disks|/dev/vd\[b-z\]|None.|

**Note:** Block storage capacity is measured in binary units. In binary units, 1 KiB equals 1,024 bytes. Example: 1 GiB = 1,024 MiB.

## Snapshot limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Quota for user-created snapshots \(also called manual snapshots\) that can be created for each disk or Shared Block Storage device|256|None.|
|Quota for automatic snapshots that can be created for each disk or Shared Block Storage device|1,000|None.|
|Quota for automatic snapshot policies that can be created per region in an account|100|None.|

## Image limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Quota for custom images that can be created per region in an account|100|Submit a ticket.|
|Quota for users to whom a single image can be shared|50|Submit a ticket.|
|Support of instance types for images|Instance types that have 4 GiB or larger memory do not support 32-bit images.|None.|

## SSH key pair limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Quota for SSH key pairs per region in an account|500|None.|
|Instance types that support SSH key pairs|Non-I/O optimized instance types of Generation I instance families do not support SSH key pairs|None.|
|Images that support SSH key pairs|Only Linux images|None.|

## Public bandwidth limits

As of November 27, 2020, the peak bandwidth available for you to create ECS instances or change the configurations of ECS instances is subject to throttling policies in your account. To increase the peak bandwidth, submit a ticket. The following throttling policies apply:

-   In a single region, the sum of actual peak bandwidths of all ECS instances that use the pay-by-traffic billing method for network usage cannot exceed 5 Gbit/s.
-   In a single region, the sum of actual peak bandwidths of all ECS instances that use the pay-by-bandwidth billing method for network usage cannot exceed 50 Gbit/s.

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Peak inbound bandwidth|-   If the purchased peak outbound bandwidth is less than or equal to 10 Mbit/s, Alibaba Cloud allocates an inbound bandwidth of 10 Mbit/s.
-   If the purchased peak outbound bandwidth is greater than 10 Mbit/s, Alibaba Cloud allocates an inbound bandwidth that is equal to the purchased peak outbound bandwidth.

|None.|
|Peak outbound bandwidth|-   Subscription instance: 200 Mbit/s
-   Pay-as-you-go instance: 100 Mbit/s

|None.|
|Change to the public IP address of an instance|The public IP address of an instance can be changed within six hours after the instance is created, and can be changed a maximum of three times.|None.|

**Note:** When the **pay-by-traffic** billing method is used, the peak inbound and outbound bandwidths are both the upper limits of bandwidths and for reference only. In the event of resource contention, these peak bandwidths cannot be guaranteed. If you want guaranteed bandwidths for your instance, use the **pay-by-bandwidth** billing method.

## Security group limits

|Item|Basic security group|Advanced security group|
|----|--------------------|-----------------------|
|Quota for security groups that can be created per region in an account|100|Same as the limit on basic security groups.|
|Quota for classic network-type ECS instances that can be contained in a classic network-type security group|1,000[\*](#ClassicNetwork)|The classic network is not supported.|
|Quota for VPC-type ECS instances that can be contained in a VPC-type security group|Depends on the number of private IP addresses that can be contained in the VPC-type security group.|No limits.|
|Quota for security groups to which an ECS instance can belong|5 You can submit a ticket to raise the limit to 10 or 16 security groups.

|Same as the limit on basic security groups.|
|Quota for security groups to which an elastic network interface \(ENI\) of an ECS instance can belong|
|Quota for rules \(including inbound and outbound rules\) in a security group|200[\*\*\*](#SecurityGroupRulesQuota)|Same as the limit on basic security group|
|Quota for rules \(both inbound and outbound rules\) in all security groups to which an ENI belongs|1,000|Same as the limit on basic security groups.|
|Quota for private IP addresses that can be contained in a VPC-type security group|2,000[\*\*](#CVPCIPAddressQuota)|65536|
|Internet access port|The default STMP port for outbound traffic is port 25, which is disabled by default. It cannot be enabled by security group rules.|Same as the limit on basic security groups.|

\* If more than 1,000 classic network-type instances need mutual access over the internal network, you can assign them to multiple security groups and authorize mutual access among these security groups.

\*\* If more than 2,000 private IP addresses need mutual access over the internal network, you can distribute the ECS instances of these IP addresses to multiple security groups and authorize mutual access among these security groups.

\*\*\* If you increase the quota for security groups to which an ECS instance can belong, the quota for rules in each security group decreases. The product of the quota for security groups to which an ECS instance belongs and the quota for rules in each security group cannot exceed 1,000. For example, if the quota for security groups to which the ECS instance can belong is 5, 10, or 16, the corresponding quota for rules in each security group is 200, 100, or 60, which are verified by using the following formulas: 5 × 200 = 1,000, 10 × 100 = 1,000, and 16 × 60 ≤ 1,000.

## Deployment set limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Quota for deployment sets per region in an account|2|None.|
|Quota for instances that can be contained in a deployment set|A maximum of seven instances are allowed in each zone. The number of instances allowed in a deployment set within a region is calculated by using the following formula: 7 × Number of zones in the region.|None.|
|Instance families that support deployment sets|c5, d1, d1ne, g5, hfc5, hfg5, i2, ic5, r5, se1ne, sn1ne, and sn2ne|None.|

## Cloud Assistant limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Quota for Cloud Assistant commands that can be created per region in an account|100|Submit a ticket.|
|Quota for Cloud Assistant commands that can be run each day by an account within a region|5,000|Submit a ticket.|

## ENI limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Quota for ENIs per region in an account|100|Submit a ticket.|

## Tag limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Quota for tags that can be bound to an instance|20|None.|

## API

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Quota for calls to the CreateInstance operation|200 calls per minute|Submit a ticket.|

**Note:** For more information about the limits on VPCs, see [Limits](/intl.en-US/Product Introduction/Limits.md).

