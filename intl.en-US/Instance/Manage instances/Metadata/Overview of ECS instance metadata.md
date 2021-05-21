---
keyword: [metadata, ]
---

# Overview of ECS instance metadata

Elastic Compute Service \(ECS\) instance metadata contains the information of ECS instances in Alibaba Cloud. You can view the metadata of running instances and configure or manage the instances based on their metadata.

## Instance metadata types

The following table describes the types of instance metadata. For more information about the instance metadata items and their definitions, see [t2078137.md\#]().

|Type|Description|References|
|----|-----------|----------|
|Basic metadata|The basic metadata of an instance includes the following information:-   Basic information such as the instance ID, IP address, media access control \(MAC\) address of the network interface controller \(NIC\), and operating system.
-   System events, including underlying operations and maintenance \(O&M\) events or unexpected maintenance events. You can use system events to have a timely understanding of the running status of the instance.

|-   [Retrieve instance metadata](/intl.en-US/Instance/Manage instances/Metadata/Retrieve instance metadata.md)
-   [Overview](/intl.en-US/Deployment & Maintenance/System events/Overview.md) |
|Dynamic metadata|The dynamic metadata of an instance includes only the identifier of the instance. Each instance identifier consists of an instance identity document and an instance identity signature. Instance identifiers are generated in real time and are typically used to identify instances. This can provide an important trust foundation for application permission control and software activation. You can view the identifier of an instance based on the metadata of the instance.

|-   [Retrieve instance metadata](/intl.en-US/Instance/Manage instances/Metadata/Retrieve instance metadata.md)
-   [Instance identity](/intl.en-US/Instance/Manage instances/Metadata/Instance identity.md) |

You can also use the user data of instances to manage startups of the instances in a flexible manner. For more information, see [Prepare user data](/intl.en-US/Instance/Manage instances/User data/Prepare user data.md).

## Limits

The instance metadata feature is supported only for instances that reside in virtual private clouds \(VPCs\).

