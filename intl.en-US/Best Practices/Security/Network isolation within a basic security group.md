# Network isolation within a basic security group

Security groups are virtual firewalls that provide stateful packet inspection \(SPI\) and packet filtering. By default, ECS instances that belong to the same basic security group can access each other over all protocols and ports. Alibaba Cloud provides a variety of network communication policies to allow you to isolate ECS instances within a basic security group.

## Internal isolation rules of security groups

The default network communication policy of security groups contains the following items:

-   Instances within a basic security group can access each other over all protocols and ports. Instances within an advanced security group are isolated from each other.
-   Instances in different security groups are isolated from each other.

    **Note:** To allow ECS instances that belong to different security groups to access each other, you can use security group rules for authorization.


To isolate ECS instances within a basic security group from each other, you can modify the network communication policy for the basic security group. For more information, see [Modify a network communication policy](#section_tmy_scv_tfb).

When you configure internal isolation rules for security groups, take note of the following items:

-   Internal isolation rules are configured only for specified basic security groups. These isolation rules do not affect the effect of default network communication policies on advanced security groups and other basic security groups.
-   Internal isolation rules of security groups implements isolation between network interface controllers, instead of between ECS instances. If multiple elastic network interfaces \(ENIs\) are bound to an instance, you must configure internal isolation rules for the security group to which each ENI belongs.
-   Internal isolation rules have the lowest priority. When you configure an internal isolation rule to isolate ECS instances within a security group, make sure that no user-defined security group rules apply in the security group to allow communication between the ECS instances.

    In the following cases, ECS instances within a security group can still access each other:

    -   The ECS instances belong to multiple security groups, and no internal isolation rules are configured for one or more of the security groups.
    -   Internal isolation rules are configured for a security group, while an access control list \(ACL\) is configured to permit communication between ECS instances within the security group.

        **Note:** For more information about ACL, see [Overview](/intl.en-US/Network security/Network ACL/Overview.md).


## Modify a network communication policy

You can call the [ModifySecurityGroupPolicy](/intl.en-US/API Reference/Security groups/ModifySecurityGroupPolicy.md) operation to modify the network communication policy for a basic security group to isolate ECS instances within the security group.

**Note:** By default, ECS instances within an advanced security group are isolated from each other. You cannot modify network communication policies for advanced security groups.

## Case analysis

In this example, Group1 and Group2 are basic security groups. ECS1, ECS2, and ECS3 are ECS instances. The following figure shows the relationships between the ECS instances and the security groups:

![ECS Instances and the security groups to which the ECS instances belong](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6014488951/p31133.png)

-   Group1 contains ECS1 and ECS2 and is configured with internal isolation rules.
-   Group2 contains ECS2 and ECS3 and uses the default network communication policy.

The following table describes whether the ECS instances are isolated from each other.

|Instance|Isolated|Description|
|:-------|:-------|:----------|
|ECS1 and ECS2|Yes|ECS1 and ECS2 belong to Group1. Group1 is configured with internal isolation rules. Therefore, ECS1 and ECS2 are isolated from each other.|
|ECS2 and ECS3|No|ECS2 and ECS3 belong to Group2. Group2 uses the default network communication policy. Therefore, ECS2 and ECS3 can access each other.|
|ECS1 and ECS3|Yes|ECS1 and ECS3 belong to different security groups. By default, ECS instances within different security groups are isolated from each other. Therefore, ECS1 and ECS3 cannot access each other.|

