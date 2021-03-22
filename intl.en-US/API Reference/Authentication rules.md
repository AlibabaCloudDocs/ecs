# Authentication rules

This topic lists the values of Action and Resource parameters that are used to implement RAM authentication. You can use the ECS console or call ECS API operations to authenticate team or department members, RAM users, and RAM roles, as well as implement authorization across cloud services. These parameters are suitable for scenarios where custom policies need to be created to implement fine-grained access control.

## Background information

**Note:** If you can access resources without authorization, skip this topic.

You can use your Alibaba Cloud account or a RAM user to manage your ECS resources by using the ECS console or by calling API operations. Specific permissions are required in the following scenarios:

-   A RAM user has no permissions to manage the ECS resources that belong to your Alibaba Cloud account.
-   You want to access ECS resources from other Alibaba Cloud services, or access other Alibaba Cloud services from ECS.
-   Before you can manage a resource, you must be granted the required permissions on the resource and the relevant API operations by the resource owner.

When an Alibaba Cloud account requests access to ECS resources in your Alibaba Cloud account by calling ECS API operations, Alibaba Cloud ECS instructs RAM to perform a permission check to ensure that the account is granted the required permissions. ECS determines which resources require a permission check based on the requested resources and API operation syntax. For more information, see [What is RAM?](/intl.en-US/Product Introduction/What is RAM?.md) and [List of operations by function](/intl.en-US/API Reference/API Reference (RAM)/List of operations by function.md).

## Custom policies

You can use the RAM console or call the [CreatePolicy](/intl.en-US/API Reference/API Reference (RAM)/Policy management APIs/CreatePolicy.md) API operation to create a custom policy. If you select **Script** for Configuration Mode, you must set the parameters in the **PolicyDocument** section based on the JSON template. You need to specify the values of Action and Resource parameters based on the authentication list in the following section. For more information, see [Implement access control by using RAM](/intl.en-US/Security/Implement access control by using RAM.md) and [Policy elements](/intl.en-US/Policy Management/Policy language/Policy elements.md).

```
{
    "Version": "1",
    "Statement": [
        {
            "Action": [
                "ecs:[ECS RAM Action]",
                "ecs:DescribeInstances"
            ],
            "Resource": [
                "[ECS RAM Action Resource]",
                "acs:ecs:$regionid:15619224785*****:instance/i-bp1bzvz55uz27hf*****"
            ],
            "Effect": "Allow"
        }
    ]
}
```

## Authentication list

**Note:** For more information about the format of the Resource, see [Terms](/intl.en-US/Product Introduction/Terms.md).

|Action|Resource|Description|
|:-----|:-------|-----------|
|AllocatePublicIpAddress|acs:ecs:$regionid:$accountid:instance/$instanceId|Assigns a public IP address to an ECS instance.|
|ApplyAutoSnapshotPolicy|acs:ecs:\*:$accountid:snapshot/\*|Applies an automatic snapshot policy to one or more cloud disks or replace the existing automatic snapshot policy of the cloud disks.|
|AttachClassicLinkVpc|acs:ecs:$regionid:$accountid:instance/$instanceId|Establishes a ClassicLink connection between a classic network-type ECS instance and a VPC to allow the instance to communicate with resources in the VPC over the internal network.|
|AttachDisk|-   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:instance/$diskId

|Attaches a pay-as-you-go data disk to an ECS instance.|
|AttachKeyPair|-   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:keypair/$keypairName

|Attaches an SSH key pair to one or more Linux ECS instances.|
|AuthorizeSecurityGroup|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|Configures an inbound rule for a security group.|
|AuthorizeSecurityGroupEgress|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|Configures an outbound rule for a security group.|
|CancelAutoSnapshotPolicy|acs:ecs:\*:$accountid:snapshot/\*|Detaches an automatic snapshot policy from one or more cloud disks.|
|CancelCopyImage|acs:ecs:$regionid:$accountid:image/$imageNo|Cancels an ongoing image copy task.|
|CopyImage|-   acs:ecs:$fromRegionid:$accountid:image/$imageNo
-   acs:ecs:$toRegionid:$accountid:image/\*

|Copies a custom image from one region to another.|
|ConvertNatPublicIpToEip|acs:ecs:$regionid:$accountid:instance/$instanceId|Converts the public IP address of a VPC-type ECS instance to an EIP.|
|CreateAutoSnapshotPolicy|acs:ecs:\*:$accountid:snapshot/\*|Creates an automatic snapshot policy.|
|CreateDisk|-   acs:ecs:$regionid:$accountid:disk/\*
-   acs:ecs:$regionid:$accountid:snapshot/$snapshotId

|Creates a pay-as-you-go or subscription data disk.|
|CreateImage|-   acs:ecs:$regionid:$accountid:image/\*
-   acs:ecs:$regionid:$accountid:snapshot/$snapshotId
-   acs:ecs:$regionid:$accountid:instance/$instanceId

|Creates a custom image.|
|CreateInstance|-   acs:ecs:$regionid:$accountid:instance/\*
-   acs:ecs:$regionid:$accountid:image/$imageNo
-   acs:ecs:$regionid:$accountid:securitygroup/$groupNo
-   acs:ecs:$regionid:$accountid:snapshot/$snapshotId
-   \(Optional\) acs:ecs:$regionid:$accountid:keypair/$keyPairName
-   acs:vpc:$regionid:$accountid:vswitch/$vswitchId
-   acs:vpc:$regionid:$accountid:vpc/$vpcId

|Creates a subscription or pay-as-you-go ECS instance.|
|CreateKeyPair|acs:ecs:$regionid:$accountid:keypair/\*|Creates an SSH key pair.|
|CreateSecurityGroup|acs:ecs:$regionid:$accountid:securitygroup/\*|Creates a security group. For a new security group, only instances in the security group can access each other by default. Access requests to the security group from outside are denied. If you want to receive requests from the Internet or requests from instances in other security groups, you can call the AuthorizeSecurityGroup operation to allow the requests.|
|CreateSnapshot|-   acs:ecs:$regionid:$accountid:snapshot/\*
-   acs:ecs:$regionid:$accountid:disk/$diskId
-   acs:ecs:$regionid:$accountid:volume/$volumeId

|Creates a snapshot for a cloud disk.|
|DeleteAutoSnapshotPolicy|acs:ecs:\*:$accountid:snapshot/\*|Deletes an automatic snapshot policy.|
|DeleteDisk|acs:ecs:$regionid:$accountid:disk/$diskId|Releases a pay-as-you-go data disk.|
|DeleteImage|acs:ecs:$regionid:$accountid:image/$imageNo|Deletes a custom image.|
|DeleteInstance|acs:ecs:$regionid:$accountid:instance/$instanceId|Releases a pay-as-you-go instance or an expired subscription instance.|
|DeleteKeyPairs|acs:ecs:$regionid:$accountid:keypair/$keyPairName|Deletes one or more SSH key pairs.|
|DeleteSecurityGroup|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|Deletes a security group.|
|DeleteSnapshot|acs:ecs:$regionid:$accountid:snapshot/$snapshotId|Deletes a specified snapshot.|
|DescribeClassicLinkInstances|acs:ecs:$regionid:$accountid:instance/\*|Queries one or multiple classic network-type instances that have established ClassicLink connections with VPCs.|
|DescribeDiskMonitorData|acs:ecs:$regionid:$accountid:disk/$diskId|Queries the monitoring data of a cloud disk within a specified period of time.|
|DescribeDisks|-   acs:ecs:$regionid:$accountid:disk/$diskId
-   acs:ecs:$regionid:$accountid:disk/\*

|Queries one or more cloud disks and local disks that you have created.|
|DescribeImages|-   acs:ecs:$regionid:$accountid:image/$imageNo
-   acs:ecs:$regionid:$accountid:image/\*

|Queries available image resources.|
|DescribeInstanceMonitorData|acs:ecs:$regionid:$accountid:instance/$instanceId|Queries the monitoring information of an ECS instance.|
|DescribeInstances|-   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:instance/\*

|Queries the details of one or more ECS instances.|
|DescribeInstanceStatus|acs:ecs:$regionid:$accountid:instance/\*|Queries the status of one or more ECS instances.|
|DescribeInstanceVncUrl|acs:ecs:$regionid:$accountid:instance/$instanceId|Queries the web management terminal URL of an ECS instance.|
|DescribeKeyPairs|-   acs:ecs:$regionid:$accountid:keypair/$keyPairName
-   acs:ecs:$regionid:$accountid:keypair/\*

|Queries one or more SSH key pairs.|
|DescribePrice|acs:ecs:\*:$accountid:\*|Queries the latest prices of ECS resources.|
|DescribeRenewalPrice|acs:ecs:$regionid:$accountid:instance/$instanceId|Queries the renewal prices of ECS resources. You can call this operation to query only the renewal prices of subscription resources.|
|DescribeSecurityGroupAttribute|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|Query the security group rules of a security group.|
|DescribeSecurityGroups|-   acs:ecs:$regionid:$accountid:securitygroup/$groupNo
-   acs:ecs:$regionid:$accountid:securitygroup/\*

|Queries the basic information of the security groups that you create.|
|DescribeSnapshotLinks|-   acs:ecs:$regionid:$accountid:disk/$diskId
-   acs:ecs:$regionid:$accountid:disk/\*

|Queries the snapshot chains of one or more cloud disks.|
|DescribeSnapshotMonitorData|acs:ecs:\*:$accountid:snapshot/\*|Queries the monitoring data on snapshot capacity changes in the last 30 days in a region.|
|DescribeSnapshots|-   acs:ecs:$regionid:$accountid:snapshot/$snapshotId
-   acs:ecs:$regionid:$accountid:snapshot/\*

|Queries all the snapshots of an ECS instance or a cloud disk.|
|DetachClassicLinkVpc|acs:ecs:$regionid:$accountid:instance/$instanceId|Removes the ClassicLink connection between a classic network-type instance and a VPC.|
|DetachDisk|-   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:disk/$diskId

|Detaches a pay-as-you-go disk from an ECS instance.|
|DetachKeyPair|-   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:keypair/$keypairName

|Unbinds an SSH key pair from one or more Linux instances.|
|ExportImage|acs:ecs:$regionid:$accountid:image/$imageNo|Exports a custom image to an OSS bucket in the same region as the custom image.|
|ImportImage|acs:ecs:$regionid:$accountid:image/\*|Imports your local image files to Alibaba Cloud ECS. Such images appear in the corresponding regions as custom images.|
|ImportKeyPair|acs:ecs:$regionid:$accountid:keypair/\*|Imports the public key of an RSA-encrypted key pair that is created by using a third-party tool. After the key pair is imported, the public key is stored in Alibaba Cloud. You must securely lock the private key away on your own.|
|JoinSecurityGroup|-   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:securitygroup/$groupNo

|Adds an ECS instance to a specified security group.|
|LeaveSecurityGroup|-   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:securitygroup/$groupNo

|Removes an ECS instance from a security group.|
|ListTagResources|acs:ecs:$regionid:$accountid:$resourceType/$resourceId|Queries tags that are bound to one or more ECS resources.|
|ModifyDiskAttribute|acs:ecs:$regionid:$accountid:disk/$diskId|Modifies the attributes of a disk.|
|ModifyImageAttribute|acs:ecs:$regionid:$accountid:image/$imageNo|Modifies the name and description of a custom image.|
|ModifyInstanceAttribute|acs:ecs:$regionid:$accountid:instance/$instanceId|Modifies the information of an ECS instance, such as the password, name, description, hostname, and user data. For a burstable instance, you can also change its performance mode.|
|ModifyInstanceAutoReleaseTime|acs:ecs:$regionid:$accountid:instance/$instanceId|Sets or cancels the automatic release time for a pay-as-you-go ECS instance. Exercise caution when you set the automatic release time because the instance will be automatically released upon expiration.|
|ModifyInstanceChargeType|acs:ecs:$regionid:$accountid:instance/$instanceId|Changes the billing method for one or more instances. You can change the billing method of instances between pay-as-you-go and subscription, or change the billing method of all cloud disks attached to an instance from pay-as-you-go to subscription.|
|ModifyInstanceNetworkSpec|acs:ecs:$regionid:$accountid:instance/$instanceId|Modifies the bandwidth configurations of an instance.|
|ModifyInstanceVncPasswd|acs:ecs:$regionid:$accountid:instance/$instanceId|Modifies the web management terminal password of an ECS instance.|
|ModifyInstanceVpcAttribute|-   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:vswitch/$vSwitchId

|Modifies the VPC attributes of an ECS instance.|
|ModifySecurityGroupAttribute|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|Modifies the name or description of a security group.|
|ModifySecurityGroupEgressRule|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|Modifies the outbound rules of a security group.|
|ModifySecurityGroupRule|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|Modifies the inbound rules for a security group.|
|ModifyPrepayInstanceSpec|acs:ecs:$regionid:$accountid:|Change the instance type of your subscription instance. The new instance type takes effect for the remaining lifecycle of the instance.|
|ModifySnapshotAttribute|acs:ecs:$regionid:$accountid:snapshot/$snapshotId|Modifies the name or description of a snapshot.|
|RebootInstance|acs:ecs:$regionid:$accountid:instance/$instanceId|Restarts an ECS instance that is in the Running state.|
|ReInitDisk|acs:ecs:$regionid:$accountid:disk/$diskId|Resets a cloud disk to its initial state.|
|RenewInstance|acs:ecs:$regionid:$accountid:instance/$instanceId|Renews a subscription ECS instance.|
|ReplaceSystemDisk|-   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:image/$imageNo

|Replaces the system disk or the operating system of an ECS instance.|
|ResetDisk|acs:ecs:$regionid:$accountid:disk/$diskId|Rolls back a disk to a specified state by using a disk snapshot.|
|ResizeDisk|acs:ecs:$regionid:$accountid:disk/$diskId|Resizes a cloud disk. You can resize a system disk or a data disk.|
|RevokeSecurityGroup|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|Deletes an inbound rule for a security group. This revokes inbound permissions of the security group.|
|RevokeSecurityGroupEgress|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|Deletes an outbound rule of a security group. After the rule is deleted, the access control implemented by the rule is removed.|
|RunInstances|-   acs:ecs:$regionid:$accountid:instance/\*
-   acs:ecs:$regionid:$accountid:image/$imageNo
-   acs:ecs:$regionid:$accountid:securitygroup/$groupNo
-   acs:ecs:$regionid:$accountid:snapshot/$snapshotId
-   acs:ecs:$regionid:$accountid:keypair/$keyPairName

|Creates one or more pay-as-you-go or subscription ECS instances.|
|StartInstance|acs:ecs:$regionid:$accountid:instance/$instanceId|Starts an instance.|
|StopInstance|acs:ecs:$regionid:$accountid:instance/$instanceId|Stops an instance.|
|TagResources|acs:ecs:$regionid:$accountid:$resourceType/$resourceId|Creates tags and binds the tags to a specified group of ECS instances.|
|UntagResources|acs:ecs:$regionid:$accountid:$resourceType/$resourceId|Unbinds tags from a specified group of ECS instances and deletes the tags.|

