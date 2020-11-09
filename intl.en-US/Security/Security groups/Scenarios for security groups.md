---
keyword: [security group, scenario, virtual firewall, access policy]
---

# Scenarios for security groups

This topic describes several typical scenarios in which security groups in VPCs and the classic network are used.

## Overview

You can configure security group rules to allow or deny ECS instances in security groups to connect to the Internet or internal network. For more information about how to create security groups and add security group rules, see [Create a security group](/intl.en-US/Security/Security groups/Create a security group.md) and [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md). The following section lists typical scenarios for configuring security group rules:

-   [Scenario 1: Allow instances that are within the same region and under the same account to communicate with each other by using an internal network](#section_i35_nll_ngb)

    If you need to copy resources between two ECS instances that are within the same region and under the same account, you can add security group rules to allow the instances to communicate with each other by using an internal network.

-   [Scenario 2: Allow instances that are within the same region but under different accounts to communicate with each other by using an internal network](#section_sfg_zll_ngb)

    If you need to copy resources between two ECS instances that are within the same region but under different accounts, you can add security group rules to allow the instances to communicate with each other by using an internal network.

-   [Scenario 3: Allow only specified IP addresses to connect to your instance](#specifyIpAccess)

    For security purposes, you can modify the port number for remote access to allow only specified IP addresses to connect to your ECS instance.

-   [Scenario 4: Allow your instance to connect to only specified public IP addresses](#specifyInstanceAccess)

    For security purposes, you can add security group rules to allow your instance to connect to only specified public IP addresses.

-   [Scenario 5: Deny your instance access to specified public IP addresses](#section_qtl_vhz_ngb)

    For security purposes, you can add security group rules to deny your instance access to specified public IP addresses.

-   [Scenario 6: Allow Internet access to your instance](#allowRemoteAccess)

    You can connect to your instance from the Internet.

-   [Scenario 7: Allow an ECS instance deployed in a security group that belongs to another account within the same internal network to connect to your instance](#section_tkx_fyq_ngb)

    You can connect to your instance from an ECS instance in a security group under another account within the same internal network.

-   [Scenario 8: Allow Internet access to your ECS instance over HTTP or HTTPS](#allowHttp)

    If you host a website on your instance, you can add security group rules to allow your users to connect to the website over HTTP or HTTPS.


**Note:**

-   For more information about commonly used ports, see [Typical applications of commonly used ports](/intl.en-US/Security/Security groups/Typical applications of commonly used ports.md).
-   In this topic, an IP address or a CIDR block is used to describe how to configure security group rules in different scenarios. Example: 12.1.1.1 or 13.1.1.1/25. Multiple IP addresses and CIDR blocks are separated by commas \(,\).

## Scenario 1: Allow instances within the same region in the same account to communicate with each other over the internal network

For two instances within the same region in the same account:

-   If the two instances belong to the same security group, they can communicate with each other over the internal network.
-   If the two instances belong to different security groups, they cannot communicate with each other over the internal network. You can add security group rules to both security groups to allow their instances to communicate with each other over the internal network. Security group rule settings vary with network types, as described in the following table.

    |Network type|Rule direction|Action|Protocol type|Port range|Priority|Authorization object|
    |:-----------|:-------------|:-----|:------------|:---------|:-------|:-------------------|
    |VPC|Inbound|Allow|Select an applicable protocol.|Specify a port range.|1|The ID of the security group to which the peer instance belongs.|
    |Classic network|Inbound|


**Note:**

For ECS instances in the same VPC, you can add security group rules to allow them to communicate with each other over the internal network. For ECS instances in different VPCs, you can use Cloud Enterprise Network \(CEN\) to allow them to communicate with each other, regardless of whether the instances belong to the same account or are located within the same region. For more information, see [Step 1: Network planning]() in *CEN documentation*.

## Scenario 2: Allow instances within the same region but in different accounts to communicate with each other over the internal network

**Note:** This scenario applies only to classic network-type ECS instances.

For example, assume that User A owns Instance A in the China \(Hangzhou\) region. The account ID of User A is 160998252992\*\*\*\*. Instance A is a classic network-type instance. This instance is assigned an internal IP address of A.A.A.A and belongs to Security Group A whose ID is sg-bp174yoe2ib1sqj5\*\*\*\*.

Assume that User B owns Instance B in the China \(Hangzhou\) region. The account ID of User B is 135652617028\*\*\*\*. Instance B is a classic network-type instance. This instance is assigned an internal IP address of B.B.B.B and belongs to Security Group B whose ID is sg-bp148p6ncq1rjuvr\*\*\*\*.

To allow Instance A and Instance B to communicate with each other over the internal network, you must add security group rules to both Security Group A and Security Group B.

-   Add the security group rule described in the following table to Security Group A.

    |Network type|Rule direction|Action|Protocol type|Port range|Authorization object|Priority|
    |:-----------|:-------------|:-----|:------------|:---------|:-------------------|:-------|
    |Classic network|Inbound|Allow|Select an applicable protocol.|Specify a port range.|Enter the account ID of User B and the ID of Security Group B in the format of account ID/security group ID. Example: 135652617028\*\*\*\*/sg-bp148p6ncq1rjuvr\*\*\*\*.

|1|

-   Add the security group rule described in the following table to Security Group B.

    |Network type|Rule direction|Action|Protocol type|Port range|Authorization object|Priority|
    |:-----------|:-------------|:-----|:------------|:---------|:-------------------|:-------|
    |Classic network|Inbound|Allow|Select an applicable protocol.|Specify a port range.|Enter the account ID of User A and the ID of Security Group A in the format of account ID/security group ID. Example: 160998252992\*\*\*\*/sg-bp174yoe2ib1sqj5\*\*\*\*

|1|

    **Note:** For security reasons, when you add an internal inbound security group rule of the classic network type, we recommend that you set Authorization Type to **Security Group**. If you set Authorization Type to **IPv4 CIDR Block**, you must specify single IP addresses in CIDR notation in the format of `a.b.c.d/32`. Note that the subnet mask must be /32.


## Scenario 3: Allow specific IP addresses access to your instance

To allow specific IP addresses access to your instance, add the security group rule described in one of the following tables to the security group to which your instance belongs.

-   Linux instance

    |Network type|Rule direction|Action|Protocol type|Port range|Authorization object|Priority|
    |:-----------|:-------------|:-----|:------------|:---------|:-------------------|:-------|
    |VPC|Inbound|Allow|Custom TCP|SSH \(22\)|The public CIDR block that you allow access to your instance. Example: 1.2.3.4/32 or 10.0.0.0/8.|1|
    |Classic network|Internet ingress|

-   Windows instance

    |Network type|Rule direction|Action|Protocol type|Port range|Authorization object|Priority|
    |:-----------|:-------------|:-----|:------------|:---------|:-------------------|:-------|
    |VPC|Inbound|Allow|Custom TCP|RDP \(3389\)|The public CIDR block that you allow access to your instance. Example: 1.2.3.4/32 or 10.0.0.0/8.|1|
    |Classic network|Internet ingress|


## Scenario 4: Allow your instance only access to specific public IP addresses

To allow your instance only access to specific IP addresses, add the following security group rules to the security group to which your instance belongs:

-   A security group rule that denies your instance access to all public IP addresses by using any protocols. Ensure that the priority of this deny rule is lower than the priority of the security group rule which allows your instance access to public IP addresses. In this example, the priority of the deny rule is set to 2. The following table describes the deny rule settings.

    |Network type|Rule direction|Action|Protocol type|Port range|Authorization object|Priority|
    |:-----------|:-------------|:-----|:------------|:---------|:-------------------|:-------|
    |VPC|Outbound|Forbid|All|-1/-1|0.0.0.0/0|2|
    |Classic network|Internet egress|

-   A security group rule that allows your instance access to specific public IP addresses. Ensure that the priority of this allow rule is higher than the priority of the preceding deny rule. In this example, the priority of the allow rule is set to 1. The following table describes the allow rule settings.

    |Network type|Rule direction|Action|Protocol type|Port range|Authorization object|Priority|
    |:-----------|:-------------|:-----|:------------|:---------|:-------------------|:-------|
    |VPC|Outbound|Allow|Select an applicable protocol.|Specify a port range.|The public CIDR block that you allow your instance to access. Example: 1.2.3.4/32 or 10.0.0.0/8.|1|
    |Classic network|Internet egress|


After you add the security group rules, connect to your instance and run the ping or telnet command to check whether the security group rules have taken effect. If your instance can access only the specified IP addresses, the security group rules have taken effect.

## Scenario 5: Deny your instance access to specific public IP addresses

To deny your instance access to specific public IP addresses, add the security group rule described in the following table to the security group to which your instance belongs.

|Network type|Rule direction|Action|Protocol type|Port range|Authorization object|Priority|
|:-----------|:-------------|:-----|:------------|:---------|:-------------------|:-------|
|VPC|Outbound|Forbid|All|-1/-1|The public CIDR block that you disallow your instance to access. Example: 1.2.3.4/32 or 10.0.0.0/8.|1|
|Classic network|Internet egress|

## Scenario 6: Allow Internet access to your instance

To allow Internet access to your instance, add the security group rule described in the following table to the security group to which your instance belongs.

|Network type|Rule direction|Action|Protocol type|Port range|Authorization object|Priority|
|:-----------|:-------------|:-----|:------------|:---------|:-------------------|:-------|
|VPC|Inbound|Allow|Custom TCP|RDP \(3389\)|To allow all public IP addresses access to your instance, enter 0.0.0.0/0. To allow specific public IP addresses access to your instance, follow the instructions in "Scenario 3: Allow specific IP addresses access to your instance."|1|
|SSH \(22\)|
|Specify a port range, such as 8080/8080.|
|Classic network|Internet ingress|Allow|Custom TCP|RDP \(3389\)|
|SSH \(22\)|
|Specify a port range, such as 8080/8080.|

For information about how to customize ports for remote access, see [Modify the default remote port of an instance](/intl.en-US/Best Practices/Security/Modify the default remote port of an instance.md).

## Scenario 7: Allow instances in a security group of another account to connect to your instance over the internal network

If an account \(Account A\) is located within the same region as your account and you want to allow one or more instances in a security group of Account A to connect to your instance over the internal network, perform the following steps:

-   To allow an instance of Account A to connect to your instance over the internal network, add the security group rule described in the following table to the security group to which your instance belongs. If both instances reside in VPCs, ensure that these instances can communicate with each other through a Cloud Enterprise Network \(CEN\) instance before you add the security group rule. For more information, see [Step 1: Network planning]() in *CEN documentation*.

    |Network type|Rule direction|Action|Protocol type|Port range|Authorization object|Priority|
    |:-----------|:-------------|:-----|:------------|:---------|:-------------------|:-------|
    |VPC|Inbound|Allow|Custom TCP|RDP \(3389\)|The private IP address of the peer instance.|1|
    |SSH \(22\)|
    |Specify a port range, such as 8080/8080.|
    |Classic network|Inbound|Allow|Custom TCP|RDP \(3389\)|The internal IP address of the peer instance. For security reasons, specify the IP address in the format of a.b.c.d/32.|1|
    |SSH \(22\)|
    |Specify a port range, such as 8080/8080.|

-   To allow all instances in a security group of Account A to connect to your instance over the internal network, add the security group rule described in the following table to the security group to which your instance belongs. For ECS instances in VPCs, ensure that the instances of the two accounts can communicate with each other through a Cloud Enterprise Network \(CEN\) instance before you add the security group rule. For more information, see [Step 1: Network planning]() in *CEN documentation*.

    |Network type|Rule direction|Action|Protocol type|Port range|Authorization object|Priority|
    |:-----------|:-------------|:-----|:------------|:---------|:-------------------|:-------|
    |VPC|Inbound|Allow|Custom TCP|RDP \(3389\)|Enter the ID of the peer account \(Account A\) and the ID of the peer security group in the format of account ID/security group ID.|1|
    |SSH \(22\)|
    |Specify a port range, such as 8080/8080.|
    |Classic network|Inbound|Allow|Custom TCP|RDP \(3389\)|
    |SSH \(22\)|
    |Specify a port range, such as 8080/8080.|


## Scenario 8: Allow Internet access to your instance over HTTP or HTTPS

If you host a website on your ECS instance, you can add a security group rule to allow users access to the website over HTTP or HTTPS.

-   To allow all public IP addresses access to your website, add the security group rule described in the following table to the security group to which your instance belongs.

    |Network type|Rule direction|Action|Protocol type|Port range|Authorization object|Priority|
    |:-----------|:-------------|:-----|:------------|:---------|:-------------------|:-------|
    |VPC|Inbound|Allow|Custom TCP|HTTP \(80\)|0.0.0.0/0|1|
    |HTTPS \(443\)|
    |Specify a port range, such as 8080/8080.|
    |Classic network|Internet ingress|Allow|Custom TCP|HTTP \(80\)|
    |HTTPS \(443\)|
    |Specify a port range, such as 8080/8080.|

-   To allow specific public IP addresses access to your website, add the security group rule described in the following table to the security group to which your instance belongs.

    |Network type|Rule direction|Action|Protocol type|Port range|Authorization object|Priority|
    |:-----------|:-------------|:-----|:------------|:---------|:-------------------|:-------|
    |VPC|Inbound|Allow|Custom TCP|HTTP \(80\)|Specify one or more public IP addresses that are allowed to access your website. Example: 1.2.3.4/32 or 10.0.0.0/8.|1|
    |HTTPS \(443\)|
    |Specify a port range, such as 8080/8080.|
    |Classic network|Internet ingress|Allow|Custom TCP|HTTP \(80\)|
    |HTTPS \(443\)|
    |Specify a port range, such as 8080/8080.|


**Note:**

-   If you cannot access your instance by using `http://<public IP address>`, [check whether TCP port 80 is working properly](https://www.alibabacloud.com/help/faq-detail/59367.htm).
-   Port 80 is the default HTTP port. To use another port \(for example, port 8080\) for HTTP, you must modify the listening port settings in the configuration file of the web server.

