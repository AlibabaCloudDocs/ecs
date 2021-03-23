---
keyword: [quick start, ECS, starter, user guide, Alibaba Cloud, Alibaba Cloud Linux]
---

# Quick reference

This guide offers solutions for issues such as how to connect to ECS instances, change operating systems, resize cloud disks, upgrade or downgrade the configurations of ECS instances, and use snapshots or images.

## Limits

-   For information about the considerations of ECS instances, see [Usage notes](/intl.en-US/Product Introduction/Usage notes.md).
-   For information about the limits of ECS resources, see [Limits](/intl.en-US/Product Introduction/Limits.md) and [View and increase instance quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase instance quotas.md).
-   To apply for ICP filings for websites that are deployed on your ECS instance, make sure that the instance meets ICP filing requirements. You can apply for a limited number of ICP filing service numbers for each ECS instance. For more information, see [Prepare and check the instance and access information]().

## Create and manage ECS instances

-   You can perform the following steps to manage the lifecycle of an ECS instance:
    1.  [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md)
    2.  [Connect to an ECS instance](/intl.en-US/Instance/Connect to instances/Overview.md)
    3.  [Stop an instance](/intl.en-US/Instance/Manage instances/Stop an instance.md)
    4.  [Release an instance](/intl.en-US/Instance/Manage instances/Release an instance.md)
-   If the instance type or network configuration of your instance is unsuitable for your business, you can change the instance type, IP address, and maximum public bandwidth:
    -   Subscription instances:
        -   [Upgrade the instance types of subscription instances](/intl.en-US/Instance/Change configurations/Change instance types/Upgrade the instance types of subscription instances.md)
        -   [Downgrade the configurations of an instance during renewal](/intl.en-US/Pricing/Renew instances/Downgrade the configurations of an instance during renewal.md)
    -   Pay-as-you-go instances:
        -   [Change the instance type of a pay-as-you-go instance](/intl.en-US/Instance/Change configurations/Change instance types/Change the instance type of a pay-as-you-go instance.md)
        -   [Modify the bandwidth configurations of pay-as-you-go instances](/intl.en-US/Instance/Change configurations/Modify bandwidth configurations/Modify the bandwidth configurations of pay-as-you-go instances.md)
    -   IP addresses of ECS instances:
        -   [Change the public IP address of an ECS instance](/intl.en-US/Network/Change IPv4 addresses/Change the public IP address of an ECS instance.md)
        -   [Convert the public IP address of a VPC-type instance to an Elastic IP address](/intl.en-US/Network/Change IPv4 addresses/Convert the public IP address of a VPC-type instance to an Elastic IP address.md)
-   If the operating system of your instance is unsuitable for your business, you can change the operating system. For more information, see [Change the operating system](/intl.en-US/Images/Change the operating system.md).
-   You can use the following features to manage ECS instances in a fine-grained manner:
    -   [User data](/intl.en-US/Instance/Manage instances/User data/Prepare user data.md)
    -   [Instance metadata](/intl.en-US/Instance/Manage instances/Metadata/Overview of instance metadata.md)
    -   [Instance identity](/intl.en-US/Instance/Manage instances/Instance identity.md)
    -   [Instance RAM roles](/intl.en-US/Security/Instance RAM roles/Overview.md)

## Manage the billing method

-   Subscription instances:

    You can use one of the following methods to renew subscription instances:

    -   [Manually renew an instance](/intl.en-US/Pricing/Renew instances/Manually renew an instance.md)
    -   [Enable auto-renewal for an instance](/intl.en-US/Pricing/Renew instances/Enable auto-renewal for an instance.md)
    -   [Downgrade the configurations of an instance during renewal](/intl.en-US/Pricing/Renew instances/Downgrade the configurations of an instance during renewal.md)
-   Pay-as-you-go instances:

    You can enable the No Fees for Stopped Instances \(VPC-Connected\) feature for pay-as-you-go instances. For more information, see [No Fees for Stopped Instances \(VPC-Connected\)](/intl.en-US/Pricing/Billing methods/No Fees for Stopped Instances (VPC-Connected).md).

-   Change the billing method of ECS instances:
    -   [Change the billing method of an instance from pay-as-you-go to subscription](/intl.en-US/Pricing/Change the billing method/Change the billing method of an instance from pay-as-you-go to subscription.md)
    -   [Change the billing method of an instance from subscription to pay-as-you-go](/intl.en-US/Pricing/Change the billing method/Change the billing method of an instance from subscription to pay-as-you-go.md)

## Improve cost-effectiveness

-   You can purchase preemptible instances to reduce costs and implement automatic scaling by combining preemptible instances with auto provisioning. For more information, see [Create an auto provisioning group](/intl.en-US/Elasticity/Manage auto provisioning groups/Create an auto provisioning group.md) and [Create a preemptible instance](/intl.en-US/Instance/Instance purchasing options/Preemptible instances/Create a preemptible instance.md).
-   You can purchase reserved instances to improve the flexibility of paying for instances and reduce costs. For more information, see [Purchase reserved instances](/intl.en-US/Instance/Instance purchasing options/Reserved Instances/Purchase reserved instances.md).

## Create and manage cloud disks

If you want to use a cloud disk as a data disk, you can perform the following steps:

1.  [Create a disk](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk.md).
2.  [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md).
3.  [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md) or [Format a data disk for a Windows ECS instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Windows ECS instance.md).
4.  Create a snapshot to back up data. For more information, see [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).
5.  If the capacity of an existing cloud disk cannot meet your requirements, resize the disk. For more information, see the following topics:
    -   [Resize disks online for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Linux instances.md)
    -   [Resize disks offline for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks offline for Linux instances.md)
    -   [Resize disks online for Windows instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Windows instances.md)
    -   [Resize disks offline for Windows instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks offline for Windows instances.md)
6.  If a data error occurs on a cloud disk, use a snapshot from a specified point in time to roll back the cloud disk. For more information, see [Roll back a disk by using a snapshot](/intl.en-US/Block Storage/Cloud disks/Roll back a disk by using a snapshot.md).
7.  If you want to restore a cloud disk to its initial status, reinitialize the cloud disk. For more information, see [Re-initialize a data disk](/intl.en-US/Block Storage/Cloud disks/Reinitialize a cloud disk/Re-initialize a data disk.md).
8.  [Detach a data disk](/intl.en-US/Block Storage/Cloud disks/Detach a data disk.md).
9.  [Release a disk](/intl.en-US/Block Storage/Cloud disks/Release a disk.md).

## Create and manage snapshots

You can perform the following steps to use a snapshot:

1.  Create a snapshot. You can use one of the following methods to manually or automatically create a snapshot:
    -   [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).
    -   Use an automatic snapshot policy to automatically create snapshots on a regular basis. For more information, see [Apply or disable an automatic snapshot policy](/intl.en-US/Snapshots/Automatic snapshot policies/Apply or disable an automatic snapshot policy.md).
2.  [View the snapshot size](/intl.en-US/Snapshots/Use snapshots/View the snapshot size.md).
3.  Delete unnecessary snapshots to save storage space. For more information, see [Reduce snapshot fees](/intl.en-US/Snapshots/Use snapshots/Reduce snapshot fees.md).

The following section describes the common scenarios of snapshots:

-   To copy or back up data, you can use a snapshot to create or roll back a cloud disk. For more information, see [Create a disk from a snapshot](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk from a snapshot.md) and [Roll back a disk by using a snapshot](/intl.en-US/Block Storage/Cloud disks/Roll back a disk by using a snapshot.md).
-   To deploy an environment, you can use a system disk snapshot to create a custom image and use the custom image to create instances. For more information, see [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md) and [Create an ECS instance by using a custom image](/intl.en-US/Instance/Create an instance/Create an ECS instance by using a custom image.md).

## Create and manage custom images

Only custom images can be managed in the ECS console. You can use a custom image to deploy a business environment. You can use one of the following methods to obtain a custom image.

-   [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md).
-   [Create a custom image from an instance](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from an instance.md).
-   [Create a custom image by using Packer](/intl.en-US/Images/Custom image/Create custom image/Create a custom image by using Packer.md).
-   Copy custom images across regions. For more information, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md).
-   Share custom images across accounts. For more information, see [Share custom images](/intl.en-US/Images/Custom image/Share or unshare custom images.md).
-   [Import custom images](/intl.en-US/Images/Custom image/Import images/Import custom images.md).
-   [Create and import on-premises images by using Packer](/intl.en-US/Images/Custom image/Create custom image/Create and import an on-premises image by using Packer.md).

You can export custom images to back up environments. For more information, see [Export custom images](/intl.en-US/Images/Custom image/Export a custom image.md).

## Create and manage security groups

You can perform the following steps to create and manage a security group.

![Process](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1634129951/p39612.png)

1.  [Create a security group](/intl.en-US/Security/Security groups/Create a security group.md).
2.  [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).
3.  [Add an ECS instance to a security group](/intl.en-US/Security/Security groups/Add an ECS instance to a security group.md).
4.  [Delete a security group rule](/intl.en-US/Security/Security groups/Manage security group rules/Delete a security group rule.md).
5.  [Delete security groups](/intl.en-US/Security/Security groups/Manage security groups/Delete security groups.md).

You can clone a security group across regions and network types to simplify business deployment. For more information, see [Clone a security group](/intl.en-US/Security/Security groups/Manage security groups/Clone a security group.md).

If new security group rules disrupt your online business, you can restore all or some of the security group rules. For more information, see [Restore security group rules](/intl.en-US/Security/Security groups/Manage security group rules/Restore security group rules.md).

## Create and bind instance RAM roles

You can perform the following steps to create and bind an instance RAM role.

1.  Optional. Authorize a RAM user to manage an instance RAM role. For more information, see [Authorize a RAM user to manage an instance RAM role](/intl.en-US/Security/Instance RAM roles/Manage an instance RAM role/Authorize a RAM user to manage an instance RAM role.md).
2.  Create and bind an instance RAM role. For more information, see [Bind an instance RAM role](/intl.en-US/Security/Instance RAM roles/Bind an instance RAM role.md).
3.  Replace the instance RAM role based on your needs. For more information, see [Replace an instance RAM role](/intl.en-US/Security/Instance RAM roles/Manage an instance RAM role/Replace an instance RAM role.md).

## Create and manage SSH key pairs

You can perform the following steps to create and manage an SSH key pair:

1.  [Create an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Create an SSH key pair.md) or [Import an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Import an SSH key pair.md).
2.  [Bind an SSH key pair to an instance](/intl.en-US/Security/Key pairs/Use an SSH key pair/Bind an SSH key pair to an instance.md).
3.  [Connect to a Linux instance by using an SSH key pair](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance by using an SSH key pair.md).
4.  [Unbind an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Unbind an SSH key pair.md).
5.  [Delete an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Delete an SSH key pair.md).

## Create and manage ENIs

You can perform the following steps to create and manage an elastic network interface \(ENI\).

![Workflow - ENIs](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9798984061/p73074.png)

1.  [Create an ENI](/intl.en-US/Network/Elastic Network Interfaces/Create an ENI.md).
2.  [Attach an ENI to an instance]() or [Attach an ENI when you create an instance](/intl.en-US/Network/Elastic Network Interfaces/Bind an ENI.md).
3.  Optional. [Configure an ENI](/intl.en-US/Network/Elastic Network Interfaces/Configure an ENI.md).
4.  [Assign secondary private IP addresses](/intl.en-US/Network/Elastic Network Interfaces/Assign secondary private IP addresses.md).
5.  [Unbind an ENI](/intl.en-US/Network/Elastic Network Interfaces/Unbind an ENI.md).
6.  [Delete an ENI](/intl.en-US/Network/Elastic Network Interfaces/Delete an ENI.md).

## Use tags

You can use tags to manage resources to enhance efficiency. You can perform the following steps to use a tag:

1.  [Create or bind a tag](/intl.en-US/Tag & Resource/Tags/Create or bind a tag.md).
2.  [Search for resources by tag](/intl.en-US/Tag & Resource/Tags/Search for resources by tag.md).
3.  [Delete or unbind a tag](/intl.en-US/Tag & Resource/Tags/Delete or unbind a tag.md).

## Create and manage launch templates

Launch templates help you create ECS instances that have the same configurations. You can perform the following steps to use a launch template:

1.  [Create a launch template](/intl.en-US/Elasticity/Launch template/Create a launch template.md).
2.  [Create a template version](/intl.en-US/Elasticity/Launch template/Create a template version.md).
3.  [Delete a launch template and a specified template version](/intl.en-US/Elasticity/Launch template/Delete a launch template and a specified template version.md).

## Create and manage deployment sets

Deployment sets help you implement high availability for underlying applications. You can perform the following steps to use a deployment set:

1.  [Create a deployment set](/intl.en-US/Elasticity/Deployment sets/Create a deployment set.md).
2.  [Create an ECS instance in a deployment set](/intl.en-US/Elasticity/Deployment sets/Create an ECS instance in a deployment set.md).
3.  [Change the deployment set of an instance](/intl.en-US/Elasticity/Deployment sets/Change the deployment set of an instance.md).
4.  [Delete a deployment set](/intl.en-US/Elasticity/Deployment sets/Delete a deployment set.md).

## Use Cloud Assistant

Cloud Assistant allows you to send remote commands to ECS instances without the need to configure jump servers. You can perform the following steps to use Cloud Assistant:

1.  Optional. Manually install and configure the Cloud Assistant client on some ECS instances. For more information, see [Install the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Install the Cloud Assistant client.md).
2.  [Create a command](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Create a command.md).
3.  [Run a command](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Run a command.md).
4.  [Query execution results and fix common problems](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Query execution results and fix common problems.md).

