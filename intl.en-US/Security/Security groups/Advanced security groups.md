---
keyword: [security group, network access control, advanced security group]
---

# Advanced security groups

Compared with basic security groups, advanced security groups can contain more Elastic Compute Service \(ECS\) instances, elastic network interfaces \(ENIs\), and private IP addresses. Advanced security groups also simplify the configuration policies of security group rules. Advanced security groups can be used in scenarios that have higher requirements for O&M efficiency, ECS instance specifications, and compute nodes.

## Comparison of features

The following table compares the features of basic and advanced security groups. For more information about basic security groups, see [Overview](/intl.en-US/Security/Security groups/Overview.md).

|Feature|Basic security group|Advanced security group|
|-------|--------------------|-----------------------|
|Supports all instance types|Yes.|No. The instance must be of the virtual private cloud \(VPC\) type.|
|Supports VPCs|Yes.|Yes.|
|Supports the classic network|Yes.|No.|
|Allows you to configure rule priorities|Yes.|Yes.|
|Allows access from other security groups|Yes.|No.|
|Allows you to manually configure security group rules|Yes.|Yes.|
|Default outbound policy without security group rules|By default, ECS instances in a security group allow outbound traffic.|By default, ECS instances in a security group do not allow outbound traffic. **Note:** When you create an advanced security group, the system creates a security group rule to allow outbound traffic for ECS instances in the security group. If you want to deny outbound traffic for the instances, you can delete this rule. |
|Allows you to bind ENIs to instances of all instance types|No. The instance must be of the VPC type.|No. The instance must be of the VPC type.|
|Maximum number of private IP addresses|2,000|65,536|
|Allows mutual access between ECS instances within the same security group by default|Yes.|No. To allow mutual access between ECS instances within the same security group, you must add security group rules.|

## Billing

You are not charged extra fees when you use advanced security groups.

## Limits

For the limits and quotas of advanced security groups, see the "Security group limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md).

In addition to the preceding limits, ECS instances must also meet the following requirements before they can be added to advanced security groups:

-   The ECS instances must be of the VPC type.
-   ECS instances and ENIs have the following requirements for their security group types:
    -   The primary ENI of an instance cannot belong to both a basic and an advanced security group at the same time.
    -   A secondary ENI cannot belong to both a basic and an advanced security group at the same time.

## Workflow

You can perform the steps in the following workflows to use advanced security groups:

-   Use advanced security groups to manage instances.

    ![Workflow - instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9798984061/p73073.png)

-   Use advanced security groups to manage ENIs.

    ![Workflow - ENIs](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9798984061/p73074.png)


**Note:** When you create an advanced security group by using the ECS console or calling an API operation, you can configure outbound rules by adhering to the following guidelines:

-   When you create the security group by using the ECS console, a security group rule is automatically added to allow all outbound traffic. We recommend that you keep the default setting to avoid network connectivity issues.
-   When you create the security group by calling an API operation, no security group rules are automatically added. All outbound traffic is denied by default. We recommend that you manually add security group rules.

## Procedure in the console

The following table describes the operations that you can perform in the ECS console to manage advanced security groups.

|Operation in the ECS console|Description|References|
|----------------------------|-----------|----------|
|Create an advanced security group|When you create an advanced security group, set **Security Group Type** to **Advanced Security Group**.|[Create a security group](/intl.en-US/Security/Security groups/Create a security group.md)|
|Add a security group rule|An advanced security group functions the same as an access whitelist. You must add rules that allow access from other security groups. Authorization objects can only be CIDR blocks.|[Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md)|
|Add an ECS instance to an advanced security group|An ECS instance cannot belong to both a basic and an advanced security group at the same time. If the instance belongs to a basic security group, you can replace the basic security group with an advanced security group.|-   [Add an ECS instance to a security group](/intl.en-US/Security/Security groups/Add an ECS instance to a security group.md)
-   [Replace security groups of an ECS instance](/intl.en-US/Security/Security groups/Replace security groups of an ECS instance.md) |
|Add an ENI to an advanced security group|If the ENI belongs to a basic security group, you can modify the ENI to add it to an advanced security group.|[Modify an ENI](/intl.en-US/Network/Elastic Network Interfaces/Modify an ENI.md)|
|Bind an ENI to an ECS instance|After the ENI is bound to the instance, the security group rules immediately take affect.|[Bind an ENI](/intl.en-US/Network/Elastic Network Interfaces/Bind an ENI.md)|
|Manage advanced security groups|The operations include adding tags, modifying names and descriptions, and managing instances in the advanced security groups.|-   [Query security groups](/intl.en-US/Security/Security groups/Manage security groups/Query security groups.md)
-   [Clone a security group](/intl.en-US/Security/Security groups/Manage security groups/Clone a security group.md)
-   [Remove an instance from a security group](/intl.en-US/Security/Security groups/Manage security groups/Remove an instance from a security group.md) |
|Manage rules for advanced security groups|You can modify security group rules during application operation to suit your needs.|-   [Modify security group rules](/intl.en-US/Security/Security groups/Manage security group rules/Modify security group rules.md)
-   [Delete a security group rule](/intl.en-US/Security/Security groups/Manage security group rules/Delete a security group rule.md)
-   [Query security group rules](/intl.en-US/Security/Security groups/Manage security group rules/Query security group rules.md) |

## API operations

The following table describes the API operations that you can use to manage advanced security groups.

|API|Description|
|---|-----------|
|[CreateSecurityGroup](/intl.en-US/API Reference/Security groups/CreateSecurityGroup.md)|When you call this operation, set the SecurityGroupType request parameter to enterprise. **Note:** Before you create an advanced security group, make sure that a VPC and a vSwitch are available. |
|[AuthorizeSecurityGroup](/intl.en-US/API Reference/Security groups/AuthorizeSecurityGroup.md)|You can call this operation to add a rule that allows inbound traffic to the advanced security group. Authorization objects can only be CIDR blocks. An advanced security group functions the same as an access whitelist. You can use the following parameters to configure security group rules:

-   Policy: the access control policy. Set the value to accept.
-   Priority: optional. The priority of the security group rule.
-   IpProtocol: required. The transport layer protocol.
-   PortRange: the range of destination ports relevant to the transport layer protocol.
-   SourcePortRange: optional. The range of source ports relevant to the transport layer protocol.
-   SourceCidrIp: the range of source IP addresses.
-   DestCiderIp: optional. The range of destination IP addresses. |
|[AuthorizeSecurityGroupEgress](/intl.en-US/API Reference/Security groups/AuthorizeSecurityGroupEgress.md)|You can call this operation to add an outbound rule to an advanced security group. **Note:** We recommend that you add a security group rule to allow all outbound traffic. |
|[JoinSecurityGroup](/intl.en-US/API Reference/Security groups/JoinSecurityGroup.md)|You can call this operation to add a VPC-type ECS instance to an advanced security group.|
|[ModifyInstanceAttribute](/intl.en-US/API Reference/Instances/ModifyInstanceAttribute.md)|If an instance belongs to a basic security group, you can call the ModifyInstanceAttribute operation to replace the security group with an advanced security group. **Note:** When you switch an ECS instance to a security group of a different type, you must understand the differences between the rule configurations of the two security group types to avoid affecting the instance network. |
|[ModifyNetworkInterfaceAttribute](/intl.en-US/API Reference/Elastic network interfaces/ModifyNetworkInterfaceAttribute.md)|If an ENI belongs to a basic security group, you can call the ModifyNetworkInterfaceAttribute operation to add the ENI to an advanced security group.|
|[AttachNetworkInterface](/intl.en-US/API Reference/Elastic network interfaces/AttachNetworkInterface.md)|You can call this operation to bind the ENI that is added to an advanced security group to an ECS instance.|
|[DescribeSecurityGroups](/intl.en-US/API Reference/Security groups/DescribeSecurityGroups.md)|You can call this operation to query the advanced security groups within the current region.|

