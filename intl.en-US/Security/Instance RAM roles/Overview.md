---
keyword: [sts, temporary credential, session persistence, ecs, access across cloud services]
---

# Overview

You can bind an instance RAM role to an ECS instance. Applications deployed on the ECS instance can then access the APIs of other Alibaba Cloud services based on a Security Token Service \(STS\) temporary credential. This ensures the security of your AccessKey pair and helps you implement fine-grained permission control and management by using RAM.

## Scenarios

Applications deployed on ECS instances can access the APIs of other Alibaba Cloud services such as Object Storage Service \(OSS\), Virtual Private Cloud \(VPC\), and ApsaraDB RDS by using an AccessKey pair of an Alibaba Cloud account or a RAM user. The AccessKey pair is configured in an ECS instance, such as writing the AccessKey pair to the configuration file, for easy management and quick calls. However, this method may cause problems such as information leaks and complex maintenance. It may also cause more permissions than necessary to be granted. Instance RAM roles can be used to avoid the preceding problems. For example, you can use an STS temporary credential to access other Alibaba Cloud services.

Instance RAM roles enable ECS instances to assume roles with certain access permissions. For more information about the roles, see [RAM role overview](/intl.en-US/RAM Role Management/RAM role overview.md).

## Benefits

You can use instance RAM roles to perform the following operations:

-   Bind a role to an ECS instance.
-   Access other Alibaba Cloud services by using an STS temporary credential.
-   Grant roles with different authorization policies to different instances so that these instances can have different access permissions on different cloud resources. This allows you to implement fine-grained access control.
-   Modify permissions by changing the authorization policy of a role rather than manually changing the AccessKey pair. This allows you to efficiently manage access permissions of an ECS instance.

## Billing

You are not billed for binding an instance RAM role.

## Limits

Instance RAM roles have the following limits:

-   The ECS instance must be a VPC-type instance.
-   Only one RAM role can be bound to an ECS instance at a time.

## References

-   For more information about the cloud services that support STS temporary credentials, see [Alibaba Cloud services that support RAM](/intl.en-US/Product Introduction/Alibaba Cloud services that support RAM.md).
-   For more information about how to access the APIs of other Alibaba Cloud services, see [Use RAM roles to access other Alibaba Cloud services](/intl.en-US/Best Practices/Use RAM roles to access other Alibaba Cloud services.md).
-   For more information about how to obtain a temporary authorization token, see [Obtain a temporary authorization token](/intl.en-US/Security/Instance RAM roles/Manage an instance RAM role/Obtain a temporary authorization token.md).

