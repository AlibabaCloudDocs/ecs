---
keyword: [failure to access TCP port 25, cannot configure public security group rules, ping failed, the maximum number of rules has been reached, network isolation, maximum number of security groups, quota of security group rules, quota of security groups]
---

# Security FAQ

-   FAQ about security groups
    -   [What is a security group?](#section_kvb_jxz_lgb)
    -   [Why do I need to select a security group when I create an ECS instance?](#section_jym_lxz_lgb)
    -   [What do I do if I create an ECS instance before I create a security group?](#section_mkc_wxz_lgb)
    -   [When I attempt to add an instance to a security group, I am prompted that the maximum number of rules has been reached. Why?](#section_vgd_1zz_lgb)
    -   [If I adjust the maximum number of security groups to which an ECS instance of the VPC type can belong, does this adjustment take effect only on the security groups created after the number is adjusted?](#section_ftt_wyz_lgb)
    -   [In what scenarios are the default security group rules used?](#section_a9i_vt4_bmz)
-   FAQ about security group rules
    -   [In what scenarios do I need to add security group rules?](#section_rg8_hk4_oph)
    -   [Why am I unable to access TCP port 25?](#section_kmc_yxz_lgb)
    -   [Why am I unable to access TCP port 80?](#section_avg_cyz_lgb)
    -   [Why have several internal security group rules been automatically added to my security group?](#section_fxk_zxz_lgb)
    -   [What happens if a security group rule is incorrectly configured?](#section_qrf_nxz_lgb)
    -   [Are the inbound and outbound rules in a security group separately counted?](#section_bll_vyz_lgb)
    -   [Can I adjust the maximum number of rules that can be added to a security group?](#section_qnp_ryz_lgb)
    -   [How are my created security group rules prioritized?](#section_qpc_6ox_ss8)
-   FAQ about host penalty and unblocking
    -   [What can I do if I receive a notification that my website has been blocked due to illegal activities and must be rectified?](#section_kw5_58g_li3)
    -   [What can I do if I receive a notification that my website has been penalized for committing external attacks?](#section_owz_g37_ea9)
-   FAQ about quotas
    -   [How do I view resource quotas?](#section_til_tmr_0wh)

## What is a security group?

A security group is a virtual firewall that implements access control for one or more Elastic Compute Service \(ECS\) instances. Security groups logically isolate security domains in the cloud.

Each ECS instance must belong to at least one security group. When you create an ECS instance, you must specify a security group for it. Security groups are classified into basic and advanced security groups. For more information, see [Overview](/intl.en-US/Security/Security groups/Overview.md).

## Why do I need to select a security group when I create an ECS instance?

When you create ECS instances, you must select security groups to divide your application environment into security domains and configure security group rules to implement appropriate network isolation.

If you create an ECS instance within a region in which you have not created security groups, the instance is assigned to the default security group. We recommend that you create a security group and then move the instance from the default security group to the security group that you created.

## What do I do if I create an ECS instance before I create a security group?

If you have not created security groups before you create an ECS instance, you can select the default security group. The default security group allows traffic on common ports such as TCP port 22 and port 3389.

## When I attempt to add an instance to a security group, I am prompted that the maximum number of rules has been reached. Why?

You can use the following formula to calculate the maximum number of security group rules that can be associated with the primary elastic network interface \(ENI\) of an ECS instance: Maximum number of security groups to which the instance can belong × Maximum number of rules in each security group.

If you are prompted with the **Failed to join the security group. The number of security group rules that have acted on the instance has reached the upper limit** message, the maximum number of security group rules applied to the instance has been reached. We recommend that you select another security group.

## If I adjust the maximum number of security groups to which an ECS instance of the VPC type can belong, does this adjustment take effect only on the security groups created after the number is adjusted?

No, the adjustment takes effect on security groups to which all ECS instances of the VPC type belong, regardless of when the security groups are created.

## In what scenarios are the default security group rules used?

The default security group rules are used in the following scenarios:

-   If you have not created a security group when you create an ECS instance in a region for the first time in the ECS console, you can select the default security group created by the system. The default security group is a basic security group. The default security group uses the default security rules. The default security rules are inbound rules that have a priority of 100 and grant access to all CIDR blocks \(0.0.0.0/0\). These rules allow inbound Internet Control Message Protocol \(ICMP\) traffic on all ports and inbound TCP traffic on SSH port 22 and Remote Desktop Protocol \(RDP\) port 3389. You can also choose to allow inbound traffic over HTTP port 80 and HTTPS port 443. All outbound traffic is allowed.
-   When you create a security group in the ECS console, the system creates default security group rules in the security group. These rules are inbound rules that grant access to all CIDR blocks \(0.0.0.0/0\). These rules allow inbound ICMP traffic on all ports, and inbound TCP traffic on SSH port 22, RDP port 3389, HTTP port 80, and HTTPS port 443.

## In what scenarios do I need to add security group rules?

In the following scenarios, you must add security group rules to ensure that your ECS instance can be accessed:

-   The security group to which your ECS instance belongs does not contain custom or default security group rules. Your ECS instance needs to access the Internet or another ECS instance in a different security group within the same region.
-   The application deployed on your ECS instance uses a specified port or port range instead of the default port. In this case, you must allow the specified port or port range before you can check whether the application is connected. For example, you have deployed the NGINX service and want to set TCP port 8000 as the listening port but only port 80 is allowed in your security group. In this case, you must add a security rule to ensure that the NGINX service is accessible.
-   For information about other scenarios, see [Scenarios for security groups](/intl.en-US/Security/Security groups/Scenarios for security groups.md).

## Why am I unable to access TCP port 25?

TCP port 25 is the default email service port. For security reasons, TCP port 25 is disabled for ECS instances by default. We recommend that you use port 465 to send emails. For information about more application scenarios, see [Scenarios](/intl.en-US/Security/Security groups/Scenarios for security groups.md).

## Why am I unable to access TCP port 80?

If you are unable to access TCP port 80, solve the problem by following the instructions in [Check whether TCP port 80 is working properly](https://www.alibabacloud.com/help/faq-detail/59367.htm).

## Why have several internal security group rules been automatically added to my security group?

Rules may be automatically added to your security group in one of the following situations:

-   You have accessed Data Management.
-   You have migrated data by using Alibaba Cloud Data Transmission Service \(DTS\). The rules associated with the IP addresses of DTS servers are automatically added to your security group.

## What happens if a security group rule is incorrectly configured?

If a security group rule is incorrectly configured, the ECS instances associated with this rule are unable to communicate with other devices over the internal network or the Internet.

-   Linux ECS instances cannot be connected to by using SSH, and Windows ECS instances cannot be connected to by using the Remote Desktop Protocol \(RDP\).
-   The public IP addresses of ECS instances cannot be `pinged`.
-   The web services provided by the ECS instances cannot be accessed over HTTP or HTTPS.
-   ECS instances associated with this rule cannot communicate with other ECS instances over the internal network.

## Are the inbound and outbound rules in a security group separately counted?

No, the inbound and outbound rules in a security group are counted together. The total number of inbound and outbound rules in each security group cannot exceed 200. For more information about this issue, see [Limits](/intl.en-US/Product Introduction/Limits.md).

## Can I adjust the maximum number of rules that can be added to a security group?

No, you cannot adjust the maximum number of rules that can be added to a security group. Each security group can contain a maximum of 200 security group rules. Each ENI of an ECS instance can be added to up to five security groups. This allows each ENI of an ECS instance to be associated with up to 1,000 security group rules.

If the maximum number of rules in each security group has been reached but you want to add more security group rules, perform the following steps:

1.  Check whether redundant rules exist. You can also [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to ask Alibaba Cloud technical support personnel to check for you.
2.  If redundant rules exist, delete them. If no redundant rules exist, create more security groups.

If you have activated Cloud Firewall, you can configure access control policies on VPC firewalls to control traffic between VPCs. This way, fewer ECS security group rules are required. For more information about how to configure access control policies on VPC firewalls, see [Access control on VPC firewalls](/intl.en-US/Access Control/Access control on VPC firewalls.md).

## How are my created security group rules prioritized?

The priority of a security group rule. The value can range from 1 to 100. A smaller value indicates a higher priority.

For security group rules of the same type, the rule that has the highest priority is applied. If an ECS instance belongs to multiple security groups, the security group rules of these security groups are applied to the instance in descending order of priority. Security group rules are applied based on the following principles:

-   If two security group rules are different only in the authorization policy, the Forbid policy is applied and the Allow policy is not.
-   If two security group rules are different only in priorities, the rule with a higher priority is applied.

## What can I do if I receive a notification that my website has been blocked due to illegal activities and must be rectified?

You can check the records of harmful Internet information to view domain names or URLs that contain harmful information, penalty actions, reasons, and duration. When you are sure that the harmful information from your domain name or URL has been cleared or does not exist, you can apply to unblock the domain name or URL. For more information, see [View harmful Internet information](https://www.alibabacloud.com/help/doc-detail/84438.htm).

## What can I do if I receive a notification that my website has been penalized for committing external attacks?

You can check the penalty records to view the details about penalty actions, reasons, and duration. If you do not agree with the penalty, provide your feedback and file an appeal. After Alibaba Cloud receives your feedback on the penalty, Alibaba Cloud checks the penalty and determines whether the penalty is appropriate and whether to uphold or rescind the penalty. For more information, see [View the penalty list](https://www.alibabacloud.com/help/doc-detail/84434.htm).

## How can I view the resource quota?

For more information about how to view the limits and quotas of resources, see [Limits](/intl.en-US/Product Introduction/Limits.md).

