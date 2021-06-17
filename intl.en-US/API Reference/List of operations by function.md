# List of operations by function

The following tables list the API operations available for use in Elastic Compute Service \(ECS\).

## Instances

|Operation|Description|
|---------|-----------|
|[RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md)|Creates one or more pay-as-you-go or subscription instances.|
|[CreateInstance](/intl.en-US/API Reference/Instances/CreateInstance.md)|Creates a subscription or pay-as-you-go instance.|
|[StartInstance](/intl.en-US/API Reference/Instances/StartInstance.md)|Starts an instance.|
|[StopInstance](/intl.en-US/API Reference/Instances/StopInstance.md)|Stops an instance.|
|[RebootInstance](/intl.en-US/API Reference/Instances/RebootInstance.md)|Restarts an instance that is in the Running state.|
|[DeleteInstance](/intl.en-US/API Reference/Instances/DeleteInstance.md)|Releases a pay-as-you-go instance or an expired subscription instance.|
|[StartInstances](/intl.en-US/API Reference/Instances/StartInstances.md)|Starts one or more instances that are in the Stopped state.|
|[RebootInstances](/intl.en-US/API Reference/Instances/RebootInstances.md)|Restarts one or more instances that are in the Running state.|
|[StopInstances](/intl.en-US/API Reference/Instances/StopInstances.md)|Stops one or more instances that are in the Running state.|
|[AttachInstanceRamRole](/intl.en-US/API Reference/Instances/AttachInstanceRamRole.md)|Attaches an instance Resource Access Management \(RAM\) role to one or more instances. An instance can have only one instance RAM role. If an instance already has an instance RAM role, an error is returned when you attach another instance RAM role to the instance.|
|[DetachInstanceRamRole](/intl.en-US/API Reference/Instances/DetachInstanceRamRole.md)|Detaches an instance RAM role from one or more instances.|
|[DescribeInstanceStatus](/intl.en-US/API Reference/Instances/DescribeInstanceStatus.md)|Queries the status information of one or more instances.|
|[DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md)|Queries the details about one or more instances.|
|[DescribeInstanceVncUrl](/intl.en-US/API Reference/Instances/DescribeInstanceVncUrl.md)|Queries the Virtual Network Computing \(VNC\) URL of an instance.|
|[DescribeUserData](/intl.en-US/API Reference/Instances/DescribeUserData.md)|Queries the user data of an instance.|
|[DescribeInstanceAutoRenewAttribute](/intl.en-US/API Reference/Instances/DescribeInstanceAutoRenewAttribute.md)|Queries the auto-renewal status of one or more subscription instances.|
|[DescribeInstanceRamRole](/intl.en-US/API Reference/Instances/DescribeInstanceRamRole.md)|Queries instance RAM roles attached to one or more instances.|
|[DescribeSpotPriceHistory](/intl.en-US/API Reference/Instances/DescribeSpotPriceHistory.md)|Queries the price history of a preemptible instance over the last 30 days.|
|[DescribeSpotAdvice](/intl.en-US/API Reference/Instances/DescribeSpotAdvice.md)|Queries information such as the average release rate and discount rate of a preemptible instance in a specified region over the last 30 days.|
|[DescribeInstanceTypeFamilies](/intl.en-US/API Reference/Instances/DescribeInstanceTypeFamilies.md)|Queries instance families provided by ECS.|
|[DescribeInstanceTypes](/intl.en-US/API Reference/Instances/DescribeInstanceTypes.md)|Queries instance types provided by ECS.|
|[ModifyInstanceAttribute](/intl.en-US/API Reference/Instances/ModifyInstanceAttribute.md)|Modifies information about an instance, such as the password, name, description, hostname, and user data. For a burstable instance, you can also change its performance mode.|
|[ModifyInstanceVncPasswd](/intl.en-US/API Reference/Instances/ModifyInstanceVncPasswd.md)|Modifies the VNC password of an instance.|
|[ModifyInstanceAutoReleaseTime](/intl.en-US/API Reference/Instances/ModifyInstanceAutoReleaseTime.md)|Sets or cancels the automatic release time for a pay-as-you-go instance. If you set the automatic release time for an instance, the instance is automatically released at the specified time. Proceed with caution when you perform this operation.|
|[ModifyInstanceAutoRenewAttribute](/intl.en-US/API Reference/Instances/ModifyInstanceAutoRenewAttribute.md)|Configures auto-renewal for one or more subscription instances. To reduce the maintenance workloads when instances expire, you can configure auto-renewal for subscription instances.|
|[ModifyInstanceChargeType](/intl.en-US/API Reference/Instances/ModifyInstanceChargeType.md)|Changes the billing method of one or more ECS instances. You can change the billing methods of instances between pay-as-you-go and subscription, or change the billing method of all data disks attached to an instance from pay-as-you-go to subscription.|
|[ModifyInstanceSpec](/intl.en-US/API Reference/Instances/ModifyInstanceSpec.md)|Changes the instance type and public bandwidth of a pay-as-you-go instance.|
|[ModifyPrepayInstanceSpec](/intl.en-US/API Reference/Instances/ModifyPrepayInstanceSpec.md)|Upgrades or downgrades the instance type of a subscription instance. The new instance type takes effect for the entire lifecycle of the instance.|
|[ModifyInstanceMetadataOptions](/intl.en-US/API Reference/Instances/ModifyInstanceMetadataOptions.md)|Modifies the metadata of an instance.|
|[RenewInstance](/intl.en-US/API Reference/Instances/RenewInstance.md)|Renews a subscription instance.|
|[ReactivateInstances](/intl.en-US/API Reference/Instances/ReActivateInstances.md)|Reactivates a pay-as-you-go instance that is in the Expired state or in the Overdue and Being Recycled state.|
|[DeleteInstances](/intl.en-US/API Reference/Instances/DeleteInstances.md)|Releases one or more pay-as-you-go instances or expired subscription instances.|

## Dedicated hosts

|Operation|Description|
|---------|-----------|
|[AllocateDedicatedHosts](/intl.en-US/API Reference/Dedicated hosts/AllocateDedicatedHosts.md)|Creates one or more pay-as-you-go or subscription dedicated hosts. A dedicated host is a physical server dedicated to a single tenant. You can create ECS instances on a dedicated host and view the properties of the dedicated host.|
|[CreateDedicatedHostCluster](/intl.en-US/API Reference/Dedicated hosts/CreateDedicatedHostCluster.md)|Creates a dedicated host cluster.|
|[DescribeDedicatedHostClusters](/intl.en-US/API Reference/Dedicated hosts/DescribeDedicatedHostClusters.md)|Queries the details about one or more dedicated host clusters.|
|[ModifyDedicatedHostClusterAttribute](/intl.en-US/API Reference/Dedicated hosts/ModifyDedicatedHostClusterAttribute.md)|Modifies some properties of a dedicated host cluster, such as its name and description.|
|[DeleteDedicatedHostCluster](/intl.en-US/API Reference/Dedicated hosts/DeleteDedicatedHostCluster.md)|Deletes a dedicated host cluster.|
|[RenewDedicatedHosts](/intl.en-US/API Reference/Dedicated hosts/RenewDedicatedHosts.md)|Renews one or more subscription dedicated hosts.|
|[ReleaseDedicatedHost](/intl.en-US/API Reference/Dedicated hosts/ReleaseDedicatedHost.md)|Releases a pay-as-you-go dedicated host.|
|[RedeployDedicatedHost](/intl.en-US/API Reference/Dedicated hosts/RedeployDedicatedHost.md)|Migrates instances from a failed dedicated host.|
|[DescribeDedicatedHosts](/intl.en-US/API Reference/Dedicated hosts/DescribeDedicatedHosts.md)|Queries the details about one or more dedicated hosts, including the physical performance specifications, machine codes, service status, and a list of ECS instances that are created on the dedicated hosts.|
|[DescribeDedicatedHostTypes](/intl.en-US/API Reference/Dedicated hosts/DescribeDedicatedHostTypes.md)|Queries the details about dedicated host types supported in a region, or the ECS instance families supported by a specific dedicated host type.|
|[DescribeDedicatedHostAutoRenew](/intl.en-US/API Reference/Dedicated hosts/DescribeDedicatedHostAutoRenew.md)|Queries the auto-renewal status of one or more subscription dedicated hosts.|
|[ModifyInstanceDeployment](/intl.en-US/API Reference/Dedicated hosts/ModifyInstanceDeployment.md)|Modifies the deployment set of an instance or migrates an instance to a dedicated host. The instance and the destination dedicated host must be in the same region.|
|[ModifyDedicatedHostAttribute](/intl.en-US/API Reference/Dedicated hosts/ModifyDedicatedHostAttribute.md)|Modifies information of a dedicated host, such as the name, description, and instance migration policy applied when the dedicated host fails.|
|[ModifyDedicatedHostAutoReleaseTime](/intl.en-US/API Reference/Dedicated hosts/ModifyDedicatedHostAutoReleaseTime.md)|Sets or cancels the automatic release time for a pay-as-you-go dedicated host.|
|[ModifyDedicatedHostAutoRenewAttribute](/intl.en-US/API Reference/Dedicated hosts/ModifyDedicatedHostAutoRenewAttribute.md)|Enables or disables auto-renewal for one or more subscription dedicated hosts.|
|[ModifyDedicatedHostsChargeType](/intl.en-US/API Reference/Dedicated hosts/ModifyDedicatedHostsChargeType.md)|Changes the billing method of dedicated hosts.|

## Launch templates

|Operation|Description|
|---------|-----------|
|[CreateLaunchTemplate](/intl.en-US/API Reference/Launch templates/CreateLaunchTemplate.md)|Creates a launch template. A launch template eliminates the needs to configure a large number of parameters each time you create an instance.|
|[CreateLaunchTemplateVersion](/intl.en-US/API Reference/Launch templates/CreateLaunchTemplateVersion.md)|Creates a version for a specific launch template.|
|[DeleteLaunchTemplate](/intl.en-US/API Reference/Launch templates/DeleteLaunchTemplate.md)|Deletes a launch template.|
|[DeleteLaunchTemplateVersion](/intl.en-US/API Reference/Launch templates/DeleteLaunchTemplateVersion.md)|Deletes a version of a specific launch template. This operation does not delete the default version. To delete the default version, you must call the DeleteLaunchTemplate operation.|
|[DescribeLaunchTemplates](/intl.en-US/API Reference/Launch templates/DescribeLaunchTemplates.md)|Queries one or more available launch templates.|
|[DescribeLaunchTemplateVersions](/intl.en-US/API Reference/Launch templates/DescribeLaunchTemplateVersions.md)|Queries versions of launch templates.|
|[ModifyLaunchTemplateDefaultVersion](/intl.en-US/API Reference/Launch templates/ModifyLaunchTemplateDefaultVersion.md)|Modifies the default version of a launch template. If you do not specify a template version number when you create an ECS instance \(RunInstances\), the default version is used.|

## Auto provisioning groups

|Operation|Description|
|---------|-----------|
|[CreateAutoProvisioningGroup](/intl.en-US/API Reference/Auto provisioning group/CreateAutoProvisioningGroup.md)|Creates an auto provisioning group.|
|[ModifyAutoProvisioningGroup](/intl.en-US/API Reference/Auto provisioning group/ModifyAutoProvisioningGroup.md)|Modifies the configurations of an auto provisioning group.|
|[DeleteAutoProvisioningGroup](/intl.en-US/API Reference/Auto provisioning group/DeleteAutoProvisioningGroup.md)|Deletes an auto provisioning group.|
|[DescribeAutoProvisioningGroupInstances](/intl.en-US/API Reference/Auto provisioning group/DescribeAutoProvisioningGroupInstances.md)|Queries instances in an auto provisioning group.|
|[DescribeAutoProvisioningGroups](/intl.en-US/API Reference/Auto provisioning group/DescribeAutoProvisioningGroups.md)|Queries information of auto provisioning groups.|
|[DescribeAutoProvisioningGroupHistory](/intl.en-US/API Reference/Auto provisioning group/DescribeAutoProvisioningGroupHistory.md)|Queries the scheduling tasks of an auto provisioning group.|

## Elastic Block Storage \(EBS\) devices

|Operation|Description|
|---------|-----------|
|[CreateDisk](/intl.en-US/API Reference/Disk/CreateDisk.md)|Creates a pay-as-you-go or subscription data disk. The data disk can be a basic disk, an ultra disk, a standard SSD, or an enhanced SSD \(ESSD\).|
|[DeleteDisk](/intl.en-US/API Reference/Disk/DeleteDisk.md)|Releases a pay-as-you-go data disk. The data disk can be a basic disk, an ultra disk, a standard SSD, or an ESSD.|
|[DescribeDisks](/intl.en-US/API Reference/Disk/DescribeDisks.md)|Queries one or more EBS devices that you have created, including cloud disks and local disks.|
|[AttachDisk](/intl.en-US/API Reference/Disk/AttachDisk.md)|Attaches a pay-as-you-go disk to an instance.|
|[DetachDisk](/intl.en-US/API Reference/Disk/DetachDisk.md)|Detaches a pay-as-you-go disk from an instance. The disk can be a basic disk, an ultra disk, or a standard SSD.|
|[ModifyDiskAttribute](/intl.en-US/API Reference/Disk/ModifyDiskAttribute.md)|Modifies the properties of one or more disks.|
|[ReplaceSystemDisk](/intl.en-US/API Reference/Disk/ReplaceSystemDisk.md)|Replaces the system disk or operating system of an instance.|
|[ReInitDisk](/intl.en-US/API Reference/Disk/ReInitDisk.md)|Re-initializes a disk to restore it to the status when it was created.|
|[ResetDisk](/intl.en-US/API Reference/Disk/ResetDisk.md)|Rolls back a disk to a specific state based on a snapshot of the disk.|
|[ResizeDisk](/intl.en-US/API Reference/Disk/ResizeDisk.md)|Resizes a system disk or data disk.|
|[ModifyDiskChargeType](/intl.en-US/API Reference/Disk/ModifyDiskChargeType.md)|Changes the billing methods of up to 16 disks attached to an instance.|
|[ModifyDiskSpec](/intl.en-US/API Reference/Disk/ModifyDiskSpec.md)|Upgrades the performance level of an ESSD.|

## Reserved instances

|Operation|Description|
|---------|-----------|
|[PurchaseReservedInstancesOffering](/intl.en-US/API Reference/Reserved Instances/PurchaseReservedInstancesOffering.md)|Purchases a reserved instance. Reserved instances can be applied to automatically offset the bills of pay-as-you-go instances.|
|[DescribeReservedInstances](/intl.en-US/API Reference/Reserved Instances/DescribeReservedInstances.md)|Queries purchased reserved instances.|
|[ModifyReservedInstances](/intl.en-US/API Reference/Reserved Instances/ModifyReservedInstances.md)|Modifies reserved instances.|

## Storage capacity units \(SCUs\)

|Operation|Description|
|---------|-----------|
|[PurchaseStorageCapacityUnit](/intl.en-US/API Reference/Storage Capacity Units/PurchaseStorageCapacityUnit.md)|Purchases one or more SCUs.|
|[ModifyStorageCapacityUnitAttribute](/intl.en-US/API Reference/Storage Capacity Units/ModifyStorageCapacityUnitAttribute.md)|Modifies the name or description of an SCU.|
|[DescribeStorageCapacityUnits](/intl.en-US/API Reference/Storage Capacity Units/DescribeStorageCapacityUnits.md)|Queries the details about one or more SCUs.|

## Images

|Operation|Description|
|---------|-----------|
|[CreateImage](/intl.en-US/API Reference/Images/CreateImage.md)|Creates a custom image. You can use the created image to create ECS instances \(RunInstances\) or replace system disks of ECS instances \(ReplaceSystemDisk\).|
|[ImportImage](/intl.en-US/API Reference/Images/ImportImage.md)|Imports an image to ECS. The imported image appears as a custom image in the corresponding region.|
|[ExportImage](/intl.en-US/API Reference/Images/ExportImage.md)|Exports a custom image to an Object Storage Service \(OSS\) bucket in the same region.|
|[CopyImage](/intl.en-US/API Reference/Images/CopyImage.md)|Copies a custom image from one region to another. You can deploy or copy instances across regions by copying images.|
|[CancelCopyImage](/intl.en-US/API Reference/Images/CancelCopyImage.md)|Cancels an ongoing image copy \(CopyImage\) task.|
|[DescribeImages](/intl.en-US/API Reference/Images/DescribeImages.md)|Queries available images.|
|[DeleteImage](/intl.en-US/API Reference/Images/DeleteImage.md)|Deletes a custom image.|
|[DescribeImageSharePermission](/intl.en-US/API Reference/Images/DescribeImageSharePermission.md)|Queries the accounts to which a custom image is shared. The response can be displayed by page. By default, ten entries are displayed on each page.|
|[ModifyImageAttribute](/intl.en-US/API Reference/Images/ModifyImageAttribute.md)|Modifies the name or description of a custom image.|
|[ModifyImageSharePermission](/intl.en-US/API Reference/Images/ModifyImageSharePermission.md)|Manages the share permission on a custom image. After you share a custom image to another Alibaba Cloud account, the account can use the shared image to create ECS instances \(RunInstances\) or replace system disks of ECS instances \(ReplaceSystemDisk\).|
|[DescribeImageSupportInstanceTypes](/intl.en-US/API Reference/Images/DescribeImageSupportInstanceTypes.md)|Queries the instance types supported by an image.|
|[DescribeImageFromFamily](/intl.en-US/API Reference/Images/DescribeImageFromFamily.md)|Queries available custom images that are newly created in a specific image family.|

## Snapshots

|Operation|Description|
|---------|-----------|
|[CreateSnapshot](/intl.en-US/API Reference/Snapshots/CreateSnapshot.md)|Creates a snapshot for a disk.|
|[CreateAutoSnapshotPolicy](/intl.en-US/API Reference/Snapshots/CreateAutoSnapshotPolicy.md)|Creates an automatic snapshot policy.|
|[ApplyAutoSnapshotPolicy](/intl.en-US/API Reference/Snapshots/ApplyAutoSnapshotPolicy.md)|Applies an automatic snapshot policy to one or more disks. If you apply an automatic snapshot policy to a disk that already has an automatic snapshot policy, the new policy replaces the original policy to take effect on the disk.|
|[CopySnapshot](/intl.en-US/API Reference/Snapshots/CopySnapshot.md)|Copies a normal snapshot from one region to another.|
|[DeleteSnapshot](/intl.en-US/API Reference/Snapshots/DeleteSnapshot.md)|Deletes a snapshot. If you call this operation to delete a snapshot that is being created, the snapshot creation task is canceled.|
|[CancelAutoSnapshotPolicy](/intl.en-US/API Reference/Snapshots/CancelAutoSnapshotPolicy.md)|Disables the automatic snapshot policy for one or more disks.|
|[DeleteAutoSnapshotPolicy](/intl.en-US/API Reference/Snapshots/DeleteAutoSnapshotPolicy.md)|Deletes an automatic snapshot policy. After you delete an automatic snapshot policy, the policy is no longer applied to the disks on which it previously took effect.|
|[DescribeAutoSnapshotPolicyEX](/intl.en-US/API Reference/Snapshots/DescribeAutoSnapshotPolicyEX.md)|Queries the automatic snapshot policies that you have created.|
|[DescribeSnapshots](/intl.en-US/API Reference/Snapshots/DescribeSnapshots.md)|Queries all snapshots of an instance or a disk. You can specify multiple request parameters such as InstanceId, DiskId, and SnapshotIds to be queried. Specified parameters have logical AND relations. Only the specified parameters are included in the filter conditions.|
|[DescribeSnapshotLinks](/intl.en-US/API Reference/Snapshots/DescribeSnapshotLinks.md)|Queries the snapshot chains of one or more disks. A snapshot chain is a chain of all the snapshots created for a disk. A disk corresponds to a chain of snapshots.|
|[ModifyAutoSnapshotPolicyEx](/intl.en-US/API Reference/Snapshots/ModifyAutoSnapshotPolicyEx.md)|Modifies an automatic snapshot policy. After an automatic snapshot policy is modified, the modifications immediately take effect on the disks to which the policy is applied.|
|[DescribeSnapshotsUsage](/intl.en-US/API Reference/Snapshots/DescribeSnapshotsUsage.md)|Queries the number of snapshots that are stored in a region and the total size of the snapshots.|
|[ModifySnapshotAttribute](/intl.en-US/API Reference/Snapshots/ModifySnapshotAttribute.md)|Modifies the name or description of a snapshot.|

## Security groups

|Operation|Description|
|---------|-----------|
|[CreateSecurityGroup](/intl.en-US/API Reference/Security groups/CreateSecurityGroup.md)|Creates a security group. For a new security group, only instances in the security group can access each other by default. Access requests to the security group from outside are denied. If you want to allow requests from the Internet or requests from instances in other security groups, you can call the AuthorizeSecurityGroup operation.|
|[AuthorizeSecurityGroup](/intl.en-US/API Reference/Security groups/AuthorizeSecurityGroup.md)|Creates an inbound security group rule. This operation allows or denies inbound traffic from other devices to the instances in the security group.|
|[AuthorizeSecurityGroupEgress](/intl.en-US/API Reference/Security groups/AuthorizeSecurityGroupEgress.md)|Creates an outbound security group rule. This operation allows or denies outbound traffic from the instances in the security group to other devices.|
|[RevokeSecurityGroup](/intl.en-US/API Reference/Security groups/RevokeSecurityGroup.md)|Deletes an inbound security group rule. After the rule is deleted, the access control implemented by it is removed.|
|[RevokeSecurityGroupEgress](/intl.en-US/API Reference/Security groups/RevokeSecurityGroupEgress.md)|Deletes an outbound security group rule. After the rule is deleted, the access control implemented by it is removed.|
|[JoinSecurityGroup](/intl.en-US/API Reference/Security groups/JoinSecurityGroup.md)|Adds an instance to a security group.|
|[LeaveSecurityGroup](/intl.en-US/API Reference/Security groups/LeaveSecurityGroup.md)|Removes an instance from a security group.|
|[DeleteSecurityGroup](/intl.en-US/API Reference/Security groups/DeleteSecurityGroup.md)|Deletes a security group.|
|[DescribeSecurityGroupAttribute](/intl.en-US/API Reference/Security groups/DescribeSecurityGroupAttribute.md)|Queries the rules of a security group.|
|[DescribeSecurityGroups](/intl.en-US/API Reference/Security groups/DescribeSecurityGroups.md)|Queries the basic information of security groups, including their IDs and descriptions. Security groups are displayed in descending order of their IDs.|
|[DescribeSecurityGroupReferences](/intl.en-US/API Reference/Security groups/DescribeSecurityGroupReferences.md)|Queries whether a security group is referenced by other security groups.|
|[ModifySecurityGroupAttribute](/intl.en-US/API Reference/Security groups/ModifySecurityGroupAttribute.md)|Modifies the name or description of a security group.|
|[ModifySecurityGroupPolicy](/intl.en-US/API Reference/Security groups/ModifySecurityGroupPolicy.md)|Modifies the internal access control policy of a basic security group.|
|[ModifySecurityGroupRule](/intl.en-US/API Reference/Security groups/ModifySecurityGroupRule.md)|Modifies the descriptions of inbound rules of a security group. You can call the AuthorizeSecurityGroup operation to create an inbound security group rule.|
|[ModifySecurityGroupEgressRule](/intl.en-US/API Reference/Security groups/ModifySecurityGroupEgressRule.md)|Modifies the descriptions of outbound rules of a security group. You can call the AuthorizeSecurityGroupEgress operation to create an outbound security group rule.|

## Deployment sets

|Operation|Description|
|---------|-----------|
|[CreateDeploymentSet](/intl.en-US/API Reference/Deployment sets/CreateDeploymentSet.md)|Creates a deployment set in a specific region.|
|[DeleteDeploymentSet](/intl.en-US/API Reference/Deployment sets/DeleteDeploymentSet.md)|Deletes a deployment set.|
|[ModifyDeploymentSetAttribute](/intl.en-US/API Reference/Deployment sets/ModifyDeploymentSetAttribute.md)|Modifies the name and description of a deployment set.|
|[DescribeDeploymentSets](/intl.en-US/API Reference/Deployment sets/DescribeDeploymentSets.md)|Queries the properties of one or more deployment sets.|
|[DescribeDeploymentSetSupportedInstanceTypeFamily](/intl.en-US/API Reference/Deployment sets/DescribeDeploymentSetSupportedInstanceTypeFamily.md)|Queries the instance families that support deployment sets.|

## SSH key pairs

|Operation|Description|
|---------|-----------|
|[CreateKeyPair](/intl.en-US/API Reference/SSH key pairs/CreateKeyPair.md)|Creates an SSH key pair. Alibaba Cloud stores the public key and returns the unencrypted private key. The private key is PEM-encoded in the PKCS\#8 format. You must securely lock the private key away on your own.|
|[ImportKeyPair](/intl.en-US/API Reference/SSH key pairs/ImportKeyPair.md)|Imports the public key of an RSA-encrypted key pair that is generated by a third-party tool. After the key pair is imported, the public key is stored in Alibaba Cloud. You must securely lock the private key away on your own.|
|[AttachKeyPair](/intl.en-US/API Reference/SSH key pairs/AttachKeyPair.md)|Binds an SSH key pair to one or more Linux instances.|
|[DetachKeyPair](/intl.en-US/API Reference/SSH key pairs/DetachKeyPair.md)|Unbinds an SSH key pair from one or more Linux instances.|
|[DeleteKeyPairs](/intl.en-US/API Reference/SSH key pairs/DeleteKeyPairs.md)|Deletes one or more SSH key pairs. After an SSH key pair is deleted, the public key is no longer stored in Alibaba Cloud. However, the instance to which the SSH key pair is bound can still use the key pair, and the key pair name is still displayed on the instance details page.|
|[DescribeKeyPairs](/intl.en-US/API Reference/SSH key pairs/DescribeKeyPairs.md)|Queries one or more key pairs.|

## Network

|Operation|Description|
|---------|-----------|
|[ModifyInstanceVpcAttribute](/intl.en-US/API Reference/Networks/ModifyInstanceVpcAttribute.md)|Modifies the Virtual Private Cloud \(VPC\) properties of an instance.|
|[AllocatePublicIpAddress](/intl.en-US/API Reference/Networks/AllocatePublicIpAddress.md)|Assigns a public IP address to an instance.|
|[ConvertNatPublicIpToEip](/intl.en-US/API Reference/Networks/ConvertNatPublicIpToEip.md)|Converts the public IP address of a VPC-type instance to an elastic IP address \(EIP\).|
|[AttachClassicLinkVpc](/intl.en-US/API Reference/Networks/AttachClassicLinkVpc.md)|Links an instance of the classic network type to a VPC by establishing a ClassicLink connection between them. This way, the instance can communicate with cloud resources in the VPC over the internal network.|
|[DetachClassicLinkVpc](/intl.en-US/API Reference/Networks/DetachClassicLinkVpc.md)|Unlinks an instance of the classic network type from a VPC by removing the ClassicLink connection between them. After the instance is unlinked from the VPC, it can no longer communicate with the resources in the VPC.|
|[DescribeBandwidthLimitation](/intl.en-US/API Reference/Networks/DescribeBandwidthLimitation.md)|Queries available bandwidth resources.|
|[DescribeClassicLinkInstances](/intl.en-US/API Reference/Networks/DescribeClassicLinkInstances.md)|Queries one or more classic network-type instances that have established ClassicLink connections with VPCs.|
|[ModifyInstanceNetworkSpec](/intl.en-US/API Reference/Networks/ModifyInstanceNetworkSpec.md)|Modifies the bandwidth configurations of an instance. You can modify the bandwidth configurations of an instance to improve network performance.|

## Elastic network interfaces \(ENIs\)

|Operation|Description|
|---------|-----------|
|[CreateNetworkInterface](/intl.en-US/API Reference/Elastic network interfaces/CreateNetworkInterface.md)|Creates an ENI.|
|[AttachNetworkInterface](/intl.en-US/API Reference/Elastic network interfaces/AttachNetworkInterface.md)|Binds an ENI to an instance of the VPC type.|
|[DetachNetworkInterface](/intl.en-US/API Reference/Elastic network interfaces/DetachNetworkInterface.md)|Unbinds an ENI from an instance.|
|[DeleteNetworkInterface](/intl.en-US/API Reference/Elastic network interfaces/DeleteNetworkInterface.md)|Deletes an ENI.|
|[DescribeNetworkInterfaces](/intl.en-US/API Reference/Elastic network interfaces/DescribeNetworkInterfaces.md)|Queries one or more ENIs.|
|[ModifyNetworkInterfaceAttribute](/intl.en-US/API Reference/Elastic network interfaces/ModifyNetworkInterfaceAttribute.md)|Modifies the properties such as the name, description, and security group of an ENI.|
|[AssignPrivateIpAddresses](/intl.en-US/API Reference/Elastic network interfaces/AssignPrivateIpAddresses.md)|Assigns one or more secondary private IP addresses to an ENI. You can specify available private IP addresses within the CIDR block of the vSwitch that is associated with the ENI. Alternatively, you can specify a number of private IP addresses for ECS to automatically assign them.|
|[UnassignPrivateIpAddresses](/intl.en-US/API Reference/Elastic network interfaces/UnassignPrivateIpAddresses.md)|Unassigns one or more secondary private IP addresses from an ENI.|

## System events

|Operation|Description|
|---------|-----------|
|[DescribeDisksFullStatus](/intl.en-US/API Reference/System event/DescribeDisksFullStatus.md)|Queries the full status information of one or more EBS devices.|
|[DescribeInstancesFullStatus](/intl.en-US/API Reference/System event/DescribeInstancesFullStatus.md)|Queries the full status information of one or more instances. The full status information includes the instance status and the status of instance system events. The instance status is the lifecycle status of an instance. The status of instance system events is the health status of maintenance events.|
|[DescribeInstanceHistoryEvents](/intl.en-US/API Reference/System event/DescribeInstanceHistoryEvents.md)|Queries the system events of an instance. By default, system events that are in the Executed, Avoided, Canceled, or Failed state are queried.|
|[CancelSimulatedSystemEvents](/intl.en-US/API Reference/System event/CancelSimulatedSystemEvents.md)|Cancels one or more simulated system events that are in the Scheduled or Executing state. After you cancel a simulated system event, the simulated event enters the Canceled state.|
|[CreateSimulatedSystemEvents](/intl.en-US/API Reference/System event/CreateSimulatedSystemEvents.md)|Schedules simulated system events for one or more instances. The simulated system events do not actually occur on or affect ECS instances.|
|[AcceptInquiredSystemEvent](/intl.en-US/API Reference/System event/AcceptInquiredSystemEvent.md)|Accepts the default operation for a system event in the Inquiring state and authorizes the system to perform the default operation.|

## HPC clusters

|Operation|Description|
|---------|-----------|
|[DeleteHpcCluster](/intl.en-US/API Reference/HPC clusters/DeleteHpcCluster.md)|Deletes an HPC cluster.|
|[CreateHpcCluster](/intl.en-US/API Reference/HPC clusters/CreateHpcCluster.md)|Creates an HPC cluster.|
|[DescribeHpcClusters](/intl.en-US/API Reference/HPC clusters/DescribeHpcClusters.md)|Queries available HPC clusters. You can specify multiple request parameters to be queried. Specified parameters have logical AND relations. Only the specified parameters are included in the filter conditions.|
|[ModifyHpcClusterAttribute](/intl.en-US/API Reference/HPC clusters/ModifyHpcClusterAttribute.md)|Modifies the description of an HPC cluster.|

## O&M and monitoring

|Operation|Description|
|---------|-----------|
|[GetInstanceScreenshot](/intl.en-US/API Reference/Operations and monitoring/GetInstanceScreenshot.md)|Obtains the screenshots of an instance.|
|[GetInstanceConsoleOutput](/intl.en-US/API Reference/Operations and monitoring/GetInstanceConsoleOutput.md)|Obtains the command output of an instance. The returned command output is encoded in Base64.|
|[DescribeDiskMonitorData](/intl.en-US/API Reference/Operations and monitoring/DescribeDiskMonitorData.md)|Queries the monitoring data of a disk over a specific period of time.|
|[DescribeInstanceMonitorData](/intl.en-US/API Reference/Operations and monitoring/DescribeInstanceMonitorData.md)|Queries the monitoring data of an instance. The returned monitoring data about an ECS instance includes the vCPU utilization, CPU credits of the burstable instance, received data traffic, sent data traffic, and average bandwidth.|
|[DescribeEniMonitorData](/intl.en-US/API Reference/Operations and monitoring/DescribeEniMonitorData.md)|Queries the monitoring data of a secondary ENI over a specific period of time.|
|[DescribeSnapshotMonitorData](/intl.en-US/API Reference/Operations and monitoring/DescribeSnapshotMonitorData.md)|Queries the monitoring data of changes in snapshot sizes in a region over the last 30 days.|
|[DescribeInstanceMaintenanceAttributes](/intl.en-US/API Reference/Operations and monitoring/DescribeInstanceMaintenanceAttributes.md)|Queries the maintenance properties of an instance.|
|[ModifyInstanceMaintenanceAttributes](/intl.en-US/API Reference/Operations and monitoring/ModifyInstanceMaintenanceAttributes.md)|Modifies the maintenance properties of an instance.|
|[RedeployInstance](/intl.en-US/API Reference/Operations and monitoring/RedeployInstance.md)|Redeploys an instance when the instance receives an event notification.|
|[ReportInstancesStatus](/intl.en-US/API Reference/Operations and monitoring/ReportInstancesStatus.md)|Reports an exception on one or more ECS instances. You can report the same exception on multiple ECS instances or on multiple disks of an ECS instance.|

## Cloud Assistant

|Operation|Description|
|---------|-----------|
|[CreateCommand](/intl.en-US/API Reference/Cloud assistant/CreateCommand.md)|Creates a Cloud Assistant command.|
|[InvokeCommand](/intl.en-US/API Reference/Cloud assistant/InvokeCommand.md)|Triggers a Cloud Assistant command for one or more instances.|
|[StopInvocation](/intl.en-US/API Reference/Cloud assistant/StopInvocation.md)|Stops the process of a running Cloud Assistant command on one or more instances.|
|[DeleteCommand](/intl.en-US/API Reference/Cloud assistant/DeleteCommand.md)|Deletes a Cloud Assistant command.|
|[DescribeCommands](/intl.en-US/API Reference/Cloud assistant/DescribeCommands.md)|Queries Cloud Assistant commands that you have created. If you specify only the Action and RegionId parameters, all available commands are queried.|
|[DescribeInvocations](/intl.en-US/API Reference/Cloud assistant/DescribeInvocations.md)|Queries the execution list and status of Cloud Assistant commands over the last two weeks.|
|[DescribeInvocationResults](/intl.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md)|Queries the execution results of Cloud Assistant commands on instances.|
|[DescribeCloudAssistantStatus](/intl.en-US/API Reference/Cloud assistant/DescribeCloudAssistantStatus.md)|Queries whether the Cloud Assistant client is installed on one or more instances.|
|[InstallCloudAssistant](/intl.en-US/API Reference/Cloud assistant/InstallCloudAssistant.md)|Installs the Cloud Assistant client on one or more instances.|
|[RunCommand](/intl.en-US/API Reference/Cloud assistant/RunCommand.md)|Creates a Cloud Assistant command of the shell, PowerShell, or batch type, and then runs the command on one or more instances.|
|[SendFile](/intl.en-US/API Reference/Cloud assistant/SendFile.md)|Sends a remote file to one or more ECS instances.|
|[DescribeSendFileResults](/intl.en-US/API Reference/Cloud assistant/DescribeSendFileResults.md)|Queries the files sent by Cloud Assistant and their status.|

## Tags

|Operation|Description|
|---------|-----------|
|[TagResources](/intl.en-US/API Reference/Tags/TagResources.md)|Adds tags to specified ECS resources.|
|[ListTagResources](/intl.en-US/API Reference/Tags/ListTagResources.md)|Queries tags that are added to one or more ECS resources.|
|[UntagResources](/intl.en-US/API Reference/Tags/UntagResources.md)|Removes tags from specified ECS resources.|

## Regions

|Operation|Description|
|---------|-----------|
|[DescribeRegions](/intl.en-US/API Reference/Regions/DescribeRegions.md)|Queries available Alibaba Cloud regions.|
|[DescribeZones](/intl.en-US/API Reference/Regions/DescribeZones.md)|Queries the zones in a specific region.|
|[DescribeAvailableResource](/intl.en-US/API Reference/Regions/DescribeAvailableResource.md)|Queries resources in a specific zone. For example, you can query the most recent resource list before you create instances \(RunInstances\) or modify instance specifications \(ModifyInstanceSpec\) in a zone.|
|[DescribeResourcesModification](/intl.en-US/API Reference/Regions/DescribeResourcesModification.md)|Queries available resources in a specific zone when you upgrade or downgrade instance types or replace system disks.|

## Inquiry

|Operation|Description|
|---------|-----------|
|[DescribePrice](/intl.en-US/API Reference/Pricing/DescribePrice.md)|Queries the most recent prices of ECS resources.|
|[DescribeRenewalPrice](/intl.en-US/API Reference/Pricing/DescribeRenewalPrice.md)|Queries the renewal prices of subscription ECS resources. Renewal prices of only subscription resources can be queried.|

## Other operations

|Operation|Description|
|---------|-----------|
|[CancelTask](/intl.en-US/API Reference/Others/CancelTask.md)|Cancels a running task. You can cancel the running tasks generated by the ImportImage or ExportImage operation.|
|[DescribeTasks](/intl.en-US/API Reference/Others/DescribeTasks.md)|Queries the progress of one or more asynchronous requests.|
|[DescribeTaskAttribute](/intl.en-US/API Reference/Others/DescribeTaskAttribute.md)|Queries the details about an asynchronous task. You can query the asynchronous tasks generated by the ImportImage or ExportImage operation.|
|[DescribeAccountAttributes](/intl.en-US/API Reference/Others/DescribeAccountAttributes.md)|Queries the quotas of ECS resources that you can create in an Alibaba Cloud region. You can query the maximum numbers of security groups, ENIs, vCPUs for pay-as-you-go instances, vCPUs for preemptible instances, and dedicated hosts that you can create in a region. You can also query the information such as the network type or whether an account has passed real-name verification.|
|[JoinResourceGroup](/intl.en-US/API Reference/Others/JoinResourceGroup.md)|Adds an ECS resource or service to a resource group.|
|[DescribeDemands](/intl.en-US/API Reference/Others/DescribeDemands.md)|Queries the delivery and usage status of filed resources.|

