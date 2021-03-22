---
keyword: [security group, network access control, Alibaba Cloud, ECS, advanced security group]
---

# Overview

Security groups function as virtual firewalls that provide Stateful Packet Inspection \(SPI\) and packet filtering capabilities to isolate security domains on the cloud. You can configure security group rules to control the inbound and outbound traffic of ECS instances in security groups.

## Definition and characteristics

A security group is a logically isolated, mutually accessible group of instances within the same region that have the same security requirements.

Security groups have the following characteristics:

-   Each ECS instance must belong to at least one security group and can belong to multiple security groups at the same time.
-   A security group can manage multiple ECS instances within the same region.
-   ECS instances in different security groups cannot communicate with each other over the internal network. However, you can configure security group rules to allow access between the security groups.
-   Security groups are stateful. The maximum session timeout period for a security group is 910 seconds. By default, a security group allows traffic in all directions within the same session. For example, if request traffic during a session is allowed to flow in, response traffic is also allowed to flow out.

## Security group types

Security groups are classified into basic security groups and advanced security groups. The following table compares the features of the two types.

|Feature|Basic security group|Advanced security group|
|-------|--------------------|-----------------------|
|Support all instance types|Yes.|No. The instances must be of the VPC type.|
|Network type|Supports VPCs and the classic network.|Supports VPCs only.|
|Access policy when no rules are added|-   Inbound: denies all access requests.
-   Outbound: allows all access requests.

|-   Inbound: denies all access requests.
-   Outbound: denies all access requests. |
|Manually add rules|Supports both allow and forbid policies.|Supports only allow policies.|
|Set rule priorities|The default value is 1 and can be modified.|The value is fixed to 1 and cannot be modified.|
|Allow access to or from other security groups|Supports access to or from other security groups.|Does not support access to or from other security groups.|
|Bind ENIs to instances of all instance types|No. The instances must be of the VPC type.|No. The instances must be of the VPC type.|
|Maximum number of private IP addresses|2,000|65,536|
|Mutual access between instances within the same security group|Allows mutual access between instances over the internal network by default.|By default, instances are isolated from each other over the internal network. You must manually add security group rules to allow access between the instances.|
|Scenario|Scenarios that require fine-grained network control, multiple ECS instance types, and moderate network connections.|Scenarios that have high requirements for O&M efficiency, ECS instance types, and compute nodes.|

## Security group rules

Before a connection for data communication is established, the security group matches access requests against all rules to determine whether to allow the requests. A security group rule is defined by attributes such as rule direction, action, protocol type, port range, and authorization object. The following table describes these attributes.

|Attribute|Description|
|---------|-----------|
|NIC type|The NIC type depends on the network type of instances. -   If the network type of instances is VPC, the system automatically sets the NIC type of the rule to Internal.
-   If the network type of instances is classic network, you can set the NICType parameter to Internal or Internet. |
|Rule direction|Both inbound and outbound security group rules are allowed.|
|Authorization policy|Both allow and forbid rules are supported. **Note:** For advanced security groups, you can set only allow rules. |
|Protocol type|Application layer protocols such as SSH, ICMP, and RDP.|
|Port range|Ports enabled for applications or protocols. For more information, see [Common ports used by applications](/intl.en-US/Security/Security groups/Typical applications of commonly used ports.md).|
|Priority|The priority of a security group rule. The priority can range from 1 to 100. A smaller value indicates a higher priority.

For security group rules of the same type, the rule that has the highest priority takes effect. If an ECS instance belongs to multiple security groups, the security group rules of these security groups are applied to the instance in descending order of priority. Security group rules are applied based on the following principles:

-   If two security group rules are different only in the authorization policy, the forbid policy takes effect and the allow policy does not.
-   If two security group rules are different only in priorities, the rule with the higher priority takes effect.

**Note:** For rules of advanced security groups, the priority is set to 1 by default and cannot be modified. |
|Authorization type|CIDR blocks and security groups are supported as authorization types. **Note:** For rules of advanced security groups, security groups are not supported as authorization types. |
|Authorization object|You can specify CIDR blocks or security group IDs as authorization objects.**Note:** For rules of advanced security groups, you cannot specify security group IDs as authorization objects. |

You must configure different attributes for security group rules based on communication scenarios. For example, when you log on to a Linux ECS instance by using an Xshell client, a security group detects an SSH request from the Internet or internal network. The security group then matches the request against each inbound rule to check whether the rule contains the IP address of the request sender, whether the rule has the highest priority among the rules of the same type, whether the authorization policy is allow, and whether SSH port 22 is enabled. The connection for data communication is not established until an inbound rule that allows the request is matched. The following figure shows how the security group matches its rules to control the access request for a Linux ECS instance.

![Match security group rules](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5534129951/p71372.png)

For information about examples of rule configuration, see [Scenarios for security groups](/intl.en-US/Security/Security groups/Scenarios for security groups.md).

## Default security groups

When you create an ECS instance in a region by using the ECS console, a **Default Security Group** is created if no security group has been created in the current account in this region. The default security group is a basic security group and is of the same network type as the ECS instance.

![Default security group](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4534129951/p48516.png)

By default, the default security group has the following security group rules:

-   Inbound:
    -   ICMP traffic and traffic over SSH port 22 and RDP port 3389 is allowed. The authorization object is 0.0.0.0/0.
    -   You can also allow traffic over HTTP port 80 and HTTPS port 443.
    -   The rule priority is 100.

        **Note:** By default, the priority of security group rules created before May 27, 2020 is 110. 110 indicates the lowest priority of security group rules.

-   Outbound: All access requests are allowed.

## Limits

ECS instances and elastic network interfaces \(ENIs\) have the following requirements for their security group types:

-   The primary ENI of an instance cannot belong to both a basic and an advanced security group at the same time.
-   An ENI cannot belong to both a basic and an advanced security group at the same time.

For more information about the limits and quotas of security groups, see the "Security group limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md).

## Best practices

For information about the workflow of a security group, see [Manage security groups](/intl.en-US/Security/Security groups/Manage security groups.md). The following section provides some practical suggestions.

When you use security groups, we recommend that you adhere to the following best practices:

-   Use security groups as a whitelist when only a few requests are allowed to access ECS instances in the security groups. Configure deny rules for all security groups and then add allow rules one by one to allow access requests.
-   Do not use a security group to manage all applications because isolation requirements are different at different layers.
-   Add instances that have the same security requirements to the same security group. Do not create a separate security group for each instance.

When you add security group rules, we recommend that you adhere to the following best practices:

-   Configure simple security group rules. If you add an ECS instance to multiple security groups, hundreds of rules may apply to the instance. A change to these rules may cause connection errors.
-   If you want to modify the rules of a security group in the production environment, we recommend that you first test the modification on a cloned security group to avoid potential impacts on online applications. For more information, see [Clone a security group](/intl.en-US/Security/Security groups/Manage security groups/Clone a security group.md).
-   Follow the least privilege principle when you configure inbound or outbound rules for applications. For example, we recommend that you adhere to the following best practices:
    -   Select a specific port over which to allow traffic, such as 80/80. Do not set a range of ports, such as 1/80.
    -   When you add security group rules, do not grant access permissions to the 0.0.0.0/0 CIDR block unless necessary.

