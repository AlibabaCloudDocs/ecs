---
keyword: [quota, ECS quotas, insufficient ECS quotas, quota, ECS quota, upper limits for ECS resources, ECS usage limits, ECS limits, ECS resource quotas]
---

# Limits

This topic describes the limits on Elastic Compute Service \(ECS\) and how to apply for extensions on the limits.

## Overview

ECS has the following limits:

-   You cannot install virtualization software such as VMware Workstation or use ECS instances for secondary virtualization. Only ECS bare metal instances and Super Computing Clusters \(SCCs\) support secondary virtualization.
-   ECS does not support sound card applications.
-   External hardware devices such as hardware dongles, USB flash drives, external hard disks, and hardware tokens cannot be directly attached to ECS instances. Software verification methods such as two-factor authentication and dynamic passwords can be used.
-   ECS does not support multicast protocols. We recommend that you use unicast protocols instead.
-   Log Service does not support 32-bit Linux ECS instances.

    For more information about the ECS instances that support Log Service, see [Logtail overview](/intl.en-US/Data Collection/Logtail collection/Overview/Logtail overview.md).

-   To apply for ICP filings for websites that are deployed on your ECS instance, make sure that the instance meets ICP filing requirements. You can apply for only a limited number of ICP filing service numbers for each ECS instance. For more information, see [Prepare and check the instance and access information]().

## Instance limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Permissions to create ECS instances|To create ECS instances within mainland China regions, you must first complete real-name verification.|N/A|
|Instance types that can be used to create pay-as-you-go instances|Instance types that have less than 16 vCPUs.|[Submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).|
|Instances that have specific instance type, billing method, and network type configurations within a specific zone|You can view the instance quota in the ECS console. For more information, see [View and increase instance quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase instance quotas.md).|Apply for a quota increase in the ECS console. For more information, see [View and increase instance quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase instance quotas.md).|
|Maximum number of subscription instances that you can purchase at a time|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|N/A|
|Quota for launch templates per region within an account|30|N/A|
|Versions of a single launch template|30|N/A|
|Permissions to change the billing method from pay-as-you-go to subscription|You cannot change the billing method from pay-as-you-go to subscription for instances of retired instance types. For more information, see [Retired instance types](/intl.en-US/Instance/Instance type families/Retired instance types.md).|N/A|
|Permissions to change the billing method from subscription to pay-as-you-go|-   This depends on your ECS usage.
-   5,000 vCPUs × Number of hours per month.
-   The billing method change from subscription to pay-as-you-go may result in a refund. Each account has a maximum monthly refund amount. The actual refund details are displayed on the Switch to Pay-As-You-Go page in the ECS console.

|N/A|

## Reserved instance limits

|Item|Limit|Adjustable|
|----|-----|----------|
|Regional reserved instances within an account|20|[Submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).|
|Zonal reserved instances per zone within an account|20|[Submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).|
|Instance types that support reserved instances|The following list shows instance families that support reserved instances:-   General purpose instance families: g7, g6e, g6, g5, g5ne, and sn2ne
-   Compute optimized instance families: c7, c6e, c6, c5, ic5, and sn1ne
-   Memory optimized instance families: r7, r6e, r6, r5, re6, re4, and se1ne
-   Big data instance family: d2s
-   Instance families with local SSDs: i2 and i2g
-   Instance families with high clock speeds: hfc6, hfc5, hfg6, hfg5, and hfr6
-   GPU-accelerated compute optimized instance families: gn6i, gn6e, and gn6v
-   ECS Bare Metal Instance families: ebmc6, ebmg6, ebmr6, ebmhfc6, ebmhfg6, and ebmhfr6
-   Burstable instance families: t6 and t5

|N/A|

**Note:** For more information, see the "Limits" section in [Reserved instance overview](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Overview.md).

## Savings plan limits

|Item|Limit|Adjustable|
|----|-----|----------|
|Savings plans within an account|40|N/A|
|Instance types that support savings plans|Savings plans cannot be applied to instances of retired Generation I instance families, which include t1, s1, s2, s3, m1, m2, c1, and c2.|N/A|

## Elastic Block Storage \(EBS\) limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Permissions to create pay-as-you-go disks|To create disks within in mainland China regions, you must first complete real-name verification.|N/A|
|Pay-as-you-go disks|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|N/A|
|System disks on an instance|1|N/A|
|Data disks on an instance|You can attach up to 64 data disks to a g6se instance and up to 16 data disks to an instance of other instance families.|N/A|
|Total capacity of all pay-as-you-go ultra disks within an account|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|N/A|
|Total capacity of all pay-as-you-go standard SSDs within an account|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|N/A|
|Total capacity of all pay-as-you-go enhanced SSDs \(ESSDs\) within an account|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|N/A|
|Capacity of a single basic disk|5 GiB to 2,000 GiB|N/A|
|Capacity of a single standard SSD|20 GiB to 32,768 GiB|N/A|
|Capacity of a single ultra disk|20 GiB to 32,768 GiB|N/A|
|Capacity of a single ESSD|20 GiB to 32,768 GiB|N/A|
|Capacity of a single local SSD|5 GiB to 800 GiB|N/A|
|Total capacity of all local SSDs on an instance|1,024 GiB|N/A|
|Capacity of a single system disk|-   Windows Server: 40 GiB to 500 GiB
-   Red Hat: 40 GiB to 500 GiB
-   CoreOS and FreeBSD: 30 GiB to 500 GiB
-   Linux systems excluding CoreOS: 20 GiB to 500 GiB

|N/A|
|Permissions to attach new local disks to instances that are equipped with local disks|You cannot attach new local disks to instances that are already equipped with local disks.|N/A|
|Permissions to change configurations of instances that are equipped with local disks|Only bandwidth configurations of instances that are equipped with local disks can be changed.|N/A|
|Mount points of system disks|/dev/vda|N/A|
|Mount points of data disks|/dev/vd\[b-z\]|N/A|

**Note:** The capacity of EBS devices is measured in binary units. In binary units, 1 KiB equals 1,024 bytes. Example: 1 GiB = 1,024 MiB.

## Storage capacity unit \(SCU\) limits

|Item|Limit|Adjustable|
|----|-----|----------|
|Maximum capacity that you can purchase for an SCU|50 TiB|[Submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).|
|SCUs that you can purchase within a region|100|N/A|
|Resource types that support SCUs|-   ESSDs, standard SSDs, ultra disks, and basic disks
-   NAS Capacity and NAS Performance
-   Normal snapshots
-   OSS Standard, Infrequent Access, and Archive storage classes
-   Hybrid Backup Recovery \(HBR\) backup storage capacity

|N/A|

## Snapshot limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Manual snapshots that can be retained for each disk|256|N/A|
|Automatic snapshots that can be retained for each disk|1,000|N/A|
|Automatic snapshot policies that can be created per region within an account|100|N/A|

## Image limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Images within the current account|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|Apply for a quota increase in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|
|Users to whom a single image can be shared|50|[Submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).|
|Support of instance types for images|Instance types that have 4 GiB or larger memory do not support 32-bit images.|N/A|

## SSH key pair limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|SSH key pairs per region within an account|500|N/A|
|Instance types that support SSH key pairs|Non-I/O optimized instances of Generation I instance families do not support SSH key pairs.|N/A|
|Images that support SSH key pairs|Only Linux images.|N/A|

## Public bandwidth limits

Starting from November 27, 2020, the maximum bandwidth available for you to create ECS instances or change the configurations of ECS instances is subject to throttling policies within your account. If you want to raise the maximum bandwidth, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm). The following throttling policies apply:

-   Within a single region, the sum of actual peak bandwidths of all ECS instances that use the pay-by-traffic billing method for network usage cannot exceed 5 Gbit/s.
-   Within a single region, the sum of actual peak bandwidths of all ECS instances that use the pay-by-bandwidth billing method for network usage cannot exceed 50 Gbit/s.

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Maximum inbound bandwidth per instance|-   If the purchased maximum outbound bandwidth is less than or equal to 10 Mbit/s, Alibaba Cloud allocates an inbound bandwidth of 10 Mbit/s.
-   If the purchased maximum outbound bandwidth is greater than 10 Mbit/s, Alibaba Cloud allocates an inbound bandwidth that is equal to the purchased maximum outbound bandwidth.

|N/A|
|Maximum outbound bandwidth per instance|-   Subscription instance: 200 Mbit/s
-   Pay-as-you-go instance: 100 Mbit/s

|N/A|
|Changes to the assigned public IP address of an instance|The public IP address of an instance can be changed within 6 hours after the instance is created, and can be changed a maximum of three times.|N/A|

**Note:** When the **pay-by-traffic** billing method for network usage is used, the maximum inbound and outbound bandwidths are both the upper limits of bandwidths and for reference only. In scenarios where demands exceed resource supplies, the peak bandwidth values may be limited. If you want guaranteed bandwidths for your instance, use the **pay-by-bandwidth** billing method for network usage.

## Security group limits

|Item|Limit on basic security groups|Limit on advanced security groups|
|----|------------------------------|---------------------------------|
|Security groups of an instance|You can view the resource quota in the ECS console1. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|The limit is the same as that on basic security groups.|
|Classic network-type ECS instances that can be contained in a classic network-type security group|1,000②|The classic network is not supported.|
|VPC-type ECS instances that can be contained in a VPC-type security group|It depends on the number of private IP addresses that can be contained in the VPC-type security group.|No limits apply.|
|Security groups to which an ECS instance can belong|5 You can submit a ticket to raise the limit to 10 or 16 security groups.

|The limit is the same as that on basic security groups.|
|Security groups to which an elastic network interface \(ENI\) of an ECS instance can belong|
|Inbound and outbound rules in a security group|200③|The limit is the same as that on basic security groups.|
|Inbound and outbound rules in all security groups to which an ENI belongs|1,000|The limit is the same as that on basic security groups.|
|Private IP addresses that can be contained in a VPC-type security group|2,000④|65,536|
|Internet access port|The default SMTP port for outbound traffic is Port 25 and is disabled by default. The port cannot be enabled by configuring security group rules.|The limit is the same as that on basic security groups.|

-   ① The following regions share the quota for security groups that can be created within each account: China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\), China \(Beijing\), China \(Shenzhen\), China \(Hong Kong\), US \(Silicon Valley\), and Singapore \(Singapore\). A maximum of 100 security groups can be created in all of these regions within an account.
-   ② If more than 1,000 classic network-type instances need mutual access over the internal network, you can assign them to multiple security groups and authorize mutual access among these security groups.
-   ③ If you increase the quota for security groups to which an ECS instance can belong, the quota for rules in each security group decreases. The product of the quota for security groups to which an ECS instance can belong and the quota for rules in each security group cannot exceed 1,000. For example, if the quota for security groups to which the ECS instance can belong is 5, 10, or 16, the corresponding quota for rules in each security group is 200, 100, or 60, as verified by using the following formulas: 5 × 200 = 1000, 10 × 100 = 1000, and 16 × 60 ≤ 1000.

    If prefix lists are referenced in security group rules, the maximum entry capacity of the prefix lists counts towards the quota for security group rules. For example, the maximum number of entries that a prefix list can support is 100. If the prefix list is referenced in a security group, the prefix list counts as 100 rules for the security group regardless of the number of existing entries in the prefix list.

-   ④ If more than 2,000 private IP addresses need mutual access over the internal network, you can distribute the ECS instances of these private IP addresses to multiple security groups and authorize mutual access among these security groups.

## Prefix list limits

|Item|Limit|Adjustable|
|----|-----|----------|
|Prefix lists per region within an account|100|N/A|
|Entries in a single prefix list|200|N/A|
|Associated resources of a prefix list|1,000|N/A|

## Deployment set limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Deployment sets within an account|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|Apply for a quota increase in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|
|Instances that can be contained in a single deployment set|A maximum of seven instances are allowed in each zone. The number of instances allowed in a deployment set within a region is calculated by using the following formula: 7 × Number of zones in the region.|N/A|
|Instance types that support deployment sets|-   c6, g6, r6, c5, g5, ic5, and r5
-   hfc6, hfg6, hfr6, hfc5, and hfg5
-   d2, d2s, d2c, d1, and d1ne
-   i2, i2g, and i1
-   se1ne, sn1ne, and sn2ne

|N/A|

## Cloud Assistant limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Cloud Assistant commands within an account|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|N/A|
|Cloud Assistant commands that can be executed per day|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|N/A|
|Maximum size of a Cloud Assistant command output|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|N/A|
|Retention period of a Cloud Assistant command output|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|N/A|

## Elastic network interface \(ENI\) limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Secondary ENIs that you can create|You can view the resource quota in the ECS console. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|N/A|

## Tag limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Quota for tags that can be bound to a single instance|20|N/A|

## API limits

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Calls to the CreateInstance operation|200 calls per minute|[Submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).|

**Note:** For more information about the limits on VPCs, see [Limits](/intl.en-US/Product Introduction/Limits/Limits.md).

