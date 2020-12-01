# Managed security groups

If you use cloud services that require security groups, security groups are created in managed mode. These security groups are called managed security groups. Managed security groups can ensure service availability and prevent you from performing unexpected operations on resources. This topic describes managed security groups and permissions that are related to them.

## Background information

Managed security groups are used to control the operation permissions on security groups for some cloud services, such as Cloud Firewall and NAT Gateway. Managed security groups are managed by cloud service systems. You can view the security groups, but you cannot perform operations on these groups. The following descriptions are applicable to managed security groups:

**Note:** Alibaba Cloud services use Security Token Service \(STS\) to grant permissions to RAM roles in your account to create managed security groups. For more information, see [What is STS?](/intl.en-US/API Reference/API Reference (STS)/What is STS?.md)

-   In a cloud service console, you cannot perform operations on managed security groups, but you can view the information about managed security groups.
-   When you use OpenAPI to access managed security groups, you can call only API operations for query purposes. If you call API operations for operation purposes, you are prompted that the security groups are managed by the cloud service systems and you cannot perform operations on the security groups. An error message that contains the `InvalidOperation.ResourceManagedByCloudProduct` error code is returned. For more information, see [Permissions of API operations related to managed security groups](#section_7ii_37r_4kx).

You can call the [DescribeSecurityGroups](/intl.en-US/API Reference/Security groups/DescribeSecurityGroups.md) operation and view the `ServiceManaged` and `ServiceId` response parameters to check whether a security group is a managed security group.

## Permissions of API operations related to managed security groups

|API operation|Description|Whether the operation can be performed by your Alibaba Cloud account|Whether the operation can be performed by the cloud service system for which the managed security group is created|
|-------------|-----------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
|AuthorizeSecurityGroup|-   Adds an inbound rule to a security group.
-   Controls inbound access to a managed security group.

|No|Yes|
|AuthorizeSecurityGroupEgress|-   Adds an outbound rule to a security group.
-   Controls outbound access to a managed security group.

|No|Yes|
|RevokeSecurityGroup|Deletes an inbound rule from a security group.|No|Yes|
|RevokeSecurityGroupEgress|Deletes an outbound rule from a security group.|No|Yes|
|JoinSecurityGroup|Adds cloud services to a security group.|No|Yes|
|LeaveSecurityGroup|Removes cloud services from a security group.|No|Yes|
|DeleteSecurityGroup|Deletes a security group.|No|Yes|
|ModifySecurityGroupAttribute|Modifies a security group.|No|Yes|
|ModifySecurityGroupRule|Modifies the description of an inbound security group rule.|No|Yes|
|ModifySecurityGroupEgressRule|Modifies the description of an outbound security group rule.|No|Yes|
|ModifySecurityGroupPolicy|Modifies a security group policy.|No|Yes|
|DescribeSecurityGroupAttribute|Queries a security group rule.|Yes|Yes|
|DescribeSecurityGroups|Queries security groups.|Yes|Yes|
|DescribeSecurityGroupReferences|Queries whether a security group is referenced by other security groups.|Yes|Yes|
|CreateNetworkInterface|Creates an elastic network interface \(ENI\).|No|Yes|
|ModifyNetworkInterfaceAttribute|Modifies an ENI.|No|Yes|
|RunInstances|Creates one or more instances.|No|Yes|
|CreateInstance|Creates an instance.|No|Yes|
|ModifyInstanceAttribute|Modifies the security group to which an instance belongs.|No|Yes|

