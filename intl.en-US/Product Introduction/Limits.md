---
keyword: [quota, ECS quotas, insufficient ECS quotas, quota, ECS quota, upper limits for ECS resources, ECS usage limits, ECS limits, ECS resource quotas]
---

# Limits

This topic describes the limits on ECS and how to apply for extensions on some limits.

## Overview

ECS has the following limits:

-   You cannot install virtualization software such as VMware Workstation or use ECS instances for secondary virtualization. Only ECS bare metal instances and Super Computing Clusters \(SCCs\) support secondary virtualization.
-   ECS does not support sound card applications.
-   External hardware devices such as hardware dongles, USB flash drives, external hard disks, and hardware tokens cannot be directly attached to ECS instances. Software verification methods such as two-factor authentication and dynamic passwords can be used.
-   ECS does not support multicast protocols. We recommend that you use unicast protocols instead.
-   Log Service does not support 32-bit Linux ECS instances.

    For information about the ECS instances that support Log Service, see [Logtail overview](/intl.en-US/Data Collection/Logtail collection/Overview/Logtail overview.md).

-   To apply for ICP filings for websites that are deployed on your ECS instance, make sure that the instance meets ICP filing requirements. You can apply for a limited number of ICP filing service numbers for each ECS instance. For more information, see [Prepare and check the instance and access information]().

## Instance limits

|Limited item|Limit|Adjustable|
|:-----------|:----|:---------|
|Permissions to create an ECS instance|To create an ECS instance within a region in mainland China, you must first complete real-name verification.|None|
|Instance types that can be used to create pay-as-you-go instances|Instance types that have less than 16 vCPUs.|[Submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).|
|Quota for instances that have specific instance type, billing method, and network type configurations within a specific zone|You can view the instance quota in the ECS console. For more information, see [View and increase instance quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase instance quotas.md).|Apply for a quota increase in the ECS console. For more information, see [View and increase instance quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase instance quotas.md).|
|Maximum number of subscription instances that you can purchase at a time|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|None|
|Quota for instance launch templates per region in an account|30|None|
|Quota for versions of an instance launch template|30|None|
|Permissions to change the billing method from pay-as-you-go to subscription|You cannot change the billing method to subscription for instances of the retired instance types. For more information, see [Retired instance types](/intl.en-US/Instance/Retired instance types.md).|None|
|Permissions to change the billing method from subscription to pay-as-you-go|-   Depends on your ECS usage.
-   5,000 vCPUs × Number of hours per month.
-   The billing method change from subscription to pay-as-you-go may result in a refund. Each account is limited to a maximum monthly refund amount. The actual refund details are displayed on the Switch to Pay-As-You-Go page in the ECS console.

|None|

## Reserved instance limits

|Limited item|Limit|Adjustable|
|------------|-----|----------|
|Quota for regional reserved instances in an account|20|[Submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).|
|Quota for zonal reserved instances per zone in an account|20|[Submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).|
|Instance types that support reserved instances|The following list shows instance families that support reserved instances:-   General purpose instance families: g6e, g6, g5, and sn2ne
-   Compute optimized instance families: c6e, c6, c5, ic5, and sn1ne
-   Memory optimized instance families: r6e, r6, r5, and se1ne
-   Big data instance family: d2s
-   Instance families with local SSDs: i2 and i2g
-   Instance families with high clock speed: hfc6, hfc5, hfg6, hfg5, and hfr6
-   GPU-accelerated compute optimized instance families: gn6i and gn6e
-   ECS Bare Metal Instance families: ebmc6, ebmg6, ebmr6, ebmhfc6, ebmhfg6, and ebmhfr6
-   Burstable instance families: t6 and t5

|None|

**Note:** For more information, see the "Limits" section of the [Reserved instance overview](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Reserved instance overview.md) topic.

## Savings plan limits

|Limited item|Limit|Adjustable|
|------------|-----|----------|
|Quota for savings plans in an account|40|None|
|Instance types that support savings plans|Savings plans cannot be applied to instances of retired Generation I instance families, which include t1, s1, s2, s3, m1, m2, c1, and c2.|None|

## Elastic Block Storage \(EBS\) limits

|Limited item|Limit|Adjustable|
|:-----------|:----|:---------|
|Permissions to create a pay-as-you-go disk|You must complete real-name verification before you can create a disk within a region in mainland China.|None|
|Quota for pay-as-you-go disks|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|None|
|Quota for system disks on an instance|1|None|
|Quota for data disks on an instance|16|None|
|Total capacity of all pay-as-you-go ultra disks in an account|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|None|
|Total capacity of all pay-as-you-go standard SSDs in an account|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|None|
|Total capacity of all pay-as-you-go enhanced SSDs \(ESSDs\) in an account|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|None|
|Capacity of a basic disk|5 GiB to 2,000 GiB|None|
|Capacity of a standard SSD|20 GiB to 32,768 GiB|None|
|Capacity of an ultra disk|20 GiB to 32,768 GiB|None|
|Capacity of an ESSD|20 GiB to 32,768 GiB|None|
|Capacity of a local SSD|5 GiB to 800 GiB|None|
|Total capacity of all local SSDs on an instance|1,024 GiB|None|
|Capacity of a system disk|-   Windows Server: 40 GiB to 500 GiB
-   Red Hat: 40 GiB to 500 GiB
-   CoreOS and FreeBSD: 30 GiB to 500 GiB
-   Linux systems excluding CoreOS: 20 GiB to 500 GiB

|None|
|Permissions to attach new local disks to instances that are equipped with local disks|Not allowed.|None|
|Permissions to change configurations of instances that are equipped with local disks|Only bandwidth configurations of instances that are equipped with local disks can be changed.|None|
|Mount points of system disks|/dev/vda|None|
|Mount points of data disks|/dev/vd\[b-z\]|None|

**Note:** EBS device capacity is measured in binary units. In binary units, 1 KiB equals 1,024 bytes. Example: 1 GiB = 1,024 MiB.

## Storage capacity unit \(SCU\) limits

|Limited item|Limit|How to apply for an extension on the limit|
|------------|-----|------------------------------------------|
|Maximum capacity that you can purchase for an SCU|50 TiB|[Submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).|
|Quota for SCUs that you can purchase within a region|100|None|
|Resource types that support SCUs|-   ESSDs, standard SSDs, ultra disks, and basic disks
-   NAS Capacity and NAS Performance
-   Normal snapshots
-   OSS Standard, Infrequent Access, and Archive storage classes

|None|

## Snapshot limits

|Limited item|Limit|Adjustable|
|:-----------|:----|:---------|
|Quota for manual snapshots that can be retained for each disk|256|None|
|Quota for automatic snapshots that can be retained for each disk|1,000|None|
|Quota for automatic snapshot policies that can be created per region in an account|100|None|

## Image limits

|Limited item|Limit|Adjustable|
|:-----------|:----|:---------|
|Quota for images in the current account|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|Apply for a quota increase in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|
|Quota for users to whom a single image can be shared|50|[Submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).|
|Support of instance types for images|Instance types that have 4 GiB or larger memory do not support 32-bit images.|None|

## SSH key pair limits

|Limited item|Limit|Adjustable|
|:-----------|:----|:---------|
|Quota for SSH key pairs per region in an account|500|None|
|Instance types that support SSH key pairs|Non-I/O optimized instances of Generation I instance families do not support SSH key pairs.|None|
|Images that support SSH key pairs|Only Linux images.|None|

## Public bandwidth limits

As of November 27, 2020, the maximum bandwidth available for you to create ECS instances or change the configurations of ECS instances is subject to throttling policies in your account. If you need to raise the maximum bandwidth,[submit a ticket](https://workorder-intl.console.aliyun.com/console.htm). The following throttling policies apply:

-   In a single region, the sum of actual peak bandwidths of all ECS instances that use the pay-by-traffic billing method for network usage cannot exceed 5 Gbit/s.
-   In a single region, the sum of actual peak bandwidths of all ECS instances that use the pay-by-bandwidth billing method for network usage cannot exceed 50 Gbit/s.

|Limited item|Limit|Adjustable|
|:-----------|:----|:---------|
|Maximum inbound bandwidth|-   If the purchased maximum outbound bandwidth is less than or equal to 10 Mbit/s, Alibaba Cloud allocates an inbound bandwidth of 10 Mbit/s.
-   If the purchased maximum outbound bandwidth is greater than 10 Mbit/s, Alibaba Cloud allocates an inbound bandwidth that is equal to the purchased maximum outbound bandwidth.

|None|
|Maximum outbound bandwidth|-   Subscription instance: 200 Mbit/s
-   Pay-as-you-go instance: 100 Mbit/s

|None|
|Change in the assigned public IP address of an instance|The public IP address of an instance can be changed within six hours after the instance is created, and can be changed a maximum of three times.|None|

**Note:** When the **pay-by-traffic** billing method is used, the maximum inbound and outbound bandwidths are both the upper limits of bandwidths and for reference only. In the event of resource contention, these maximum bandwidths cannot be guaranteed. If you want guaranteed bandwidths for your instance, use the **pay-by-bandwidth** billing method.

## Security group limits

|Limited item|Basic security group|Advanced security group|
|------------|--------------------|-----------------------|
|Quota for security groups of an instance|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|Same as the limit on basic security groups.|
|Quota for classic network-type ECS instances that can be contained in a classic network-type security group|1,000 ①|The classic network is not supported.|
|Quota for VPC-type ECS instances that can be contained in a VPC-type security group|Depends on the number of private IP addresses that can be contained in the VPC-type security group.|No limits.|
|Quota for security groups to which an ECS instance can belong|5.You can submit a ticket to raise the limit to 10 or 16 security groups.

|Same as the limit on basic security groups.|
|Quota for security groups to which an elastic network interface \(ENI\) of an ECS instance can belong|
|Quota for both inbound and outbound rules in a security group|200 ②|Same as the limit on basic security groups.|
|Quota for both inbound and outbound rules in all security groups to which an ENI belongs|1,000|Same as the limit on basic security groups.|
|Quota for private IP addresses that can be contained in a VPC-type security group|2,000 ③|65,536|
|Internet access port|The default SMTP port for outbound traffic is port 25, which is disabled by default. It cannot be enabled by configuring security group rules.|Same as the limit on basic security groups.|

-   ① The following regions share the quota for security groups that can be created in each account: China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\), China \(Beijing\), China \(Shenzhen\), China \(Hong Kong\), US \(Silicon Valley\), and Singapore \(Singapore\). A maximum of 100 security groups can be created in all of these regions in an account.
-   ② If more than 1,000 classic network-type instances need mutual access over the internal network, you can assign them to multiple security groups and authorize mutual access among these security groups.
-   ③ If you increase the quota for security groups to which an ECS instance can belong, the quota for rules in each security group decreases. The product of the quota for security groups to which an ECS instance belongs and the quota for rules in each security group cannot exceed 1,000. For example, if the quota for security groups to which the ECS instance can belong is 5, 10, or 16, the corresponding quota for rules in each security group is 200, 100, or 60, which are verified by using the following formulas: 5 × 200 = 1000, 10 × 100 = 1000, and 16 × 60 ≤ 1000.
-   ④ If more than 2,000 private IP addresses need mutual access over the internal network, you can distribute the ECS instances of these private IP addresses to multiple security groups and authorize mutual access among these security groups.

## Deployment set limits

|Limited item|Limit|Adjustable|
|:-----------|:----|:---------|
|Quota for deployment sets in an account|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|Apply for a quota increase in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|
|Quota for instances that can be contained in a deployment set|A maximum of seven instances are allowed in each zone. The number of instances allowed in a deployment set within a region is calculated by using the following formula: 7 × Number of zones in the region.|None|
|Instance types that support deployment sets|-   c6、g6、r6、c5、g5、ic5、r5
-   hfc6、hfg6、hfr6、hfc5、hfg5
-   d2、d2s、d2c、d1、d1ne
-   i2、i2g、i1
-   se1ne、sn1ne、sn2ne

|None|

## Cloud Assistant limits

|Limited item|Limit|Adjustable|
|:-----------|:----|:---------|
|Quota for Cloud Assistant commands in an account|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|None|
|Quota for Cloud Assistant commands that can be executed per day|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|None|
|Maximum size of a Cloud Assistant command output|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|None|
|Retaining period of a Cloud Assistant command output|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|None|

## ENI limits

|Limited item|Limit|Adjustable|
|:-----------|:----|:---------|
|Quota for secondary ENIs that you can create|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|None|

## Tag limits

|Limited item|Limit|Adjustable|
|:-----------|:----|:---------|
|Quota for tags that can be bound to an instance|20|None|

## API limits

|Limited item|Limit|Adjustable|
|:-----------|:----|:---------|
|Quota for calls to the CreateInstance operation|200 calls per minute|[Submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).|

**Note:** For more information about the limits on VPCs, see [Limits](/intl.en-US/Product Introduction/Limits.md).

