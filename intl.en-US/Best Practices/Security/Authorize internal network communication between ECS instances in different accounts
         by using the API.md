# Authorize internal network communication between ECS instances in different accounts by using the API

This topic describes how to authorize internal network communication between ECS instances that are in the same region but belong to different accounts.

Alibaba Cloud Command-Line Interface \(CLI\) is installed for the ECS instance. For more information about how to install Alibaba Cloud CLI in different operating systems, see the following topics:

-   [Windows]()
-   [Linux]()
-   [MacOS]()

You can authorize internal network communication in one of the following modes:

-   [Authorize internal network communication between ECS instances](#section_bpp_qvf_ip5). You can authorize internal communication between two ECS instances that belong to the same account.
-   [Authorize internal network communication between accounts](#section_003_ysx_s54). You can authorize internal network communication between ECS instances in two security groups that belong to two different accounts within the same region, including those to be purchased after the authorization is complete.

    **Note:** To enable internal network communication between different accounts, you need to authorize communication between security groups in each account. These ECS instances can then communicate over the internal network. If you modify the configurations of a security group, all instances in the security group as well as the services running on these instances are affected. Use caution when you perform this operation.


Security groups are virtual firewalls for ECS instances. Security groups do not provide communication and networking capabilities. After you authorize internal network communication between instances that belong to different security groups, ensure that the instances can establish internal network connection.

-   If all instances are of the classic network type, they must be in the same region to communicate with each other.
-   VPCs are isolated by default. If all instances are of the VPC type, these instances cannot communicate with each other. We recommend that you allow ECS instances to communicate over a public network or through Express Connect, VPN Gateway, or Cloud Enterprise Network \(CEN\). For more information, see [Express Connect](/intl.en-US/Product Introduction/What is Express Connect?.md), [VPN Gateway](/intl.en-US/Product Overview/What is VPN Gateway.md), and [CEN]().
-   If instances are of different network types, establish a ClassicLink connection to allow communication between these instances. For more information, see [Connect a classic network to a VPC](/intl.en-US/Network/Connect a classic network to a VPC.md).
-   If instances are in different regions, we recommend that you allow ECS instances to communicate over a public network or through Express Connect, VPN Gateway, or CEN. For more information, see [Express Connect](/intl.en-US/Product Introduction/What is Express Connect?.md), [VPN Gateway](/intl.en-US/Product Overview/What is VPN Gateway.md), and [CEN]().

## Authorize internal network communication between ECS instances

1.  Query internal IP addresses and security group IDs of the two ECS instances.

    You can use the console or call the DescribeInstances operation to obtain security group IDs of the instances. The following table lists the information of the two ECS instances.

    |Instance|IP address|Security group|Security group ID|
    |--------|----------|--------------|-----------------|
    |Instance A|10.0.0.1|sg1|sg-bp1azkttqpldxgte\*\*\*\*|
    |Instance B|10.0.0.2|sg2|sg-bp15ed6xe1yxeycg\*\*\*\*|

2.  Add a rule to sg1 to allow inbound traffic from 10.0.0.2.

    ```
    aliyun ecs AuthorizeSecurityGroup --SecurityGroupId sg-bp1azkttqpldxgte**** --RegionId cn-qingdao --IpProtocol all  --PortRange=-1/-1 --SourceCidrIp 10.0.0.2 --NicType intranet
    ```

3.  Add a rule to sg2 to allow inbound traffic from 10.0.0.1.

    ```
    aliyun ecs AuthorizeSecurityGroup --SecurityGroupId sg-bp15ed6xe1yxeycg**** --RegionId cn-qingdao --IpProtocol all  --PortRange=-1/-1 --SourceCidrIp 10.0.0.1 --NicType intranet
    ```

    **Note:**

    -   In the preceding commands, the region ID cn-qingdao is for reference only. Replace it with your actual region ID.
    -   In the preceding commands, the AuthorizeSecurityGroup operation is called to add inbound rules to security groups. Specify the SecurityGroupId and SourceCidrIp parameters.
4.  After a few minutes, run the ping command to check whether the two ECS instances can communicate with each other over the internal network.


## Authorize internal network communication between accounts

1.  Query names and security group IDs of the two accounts.

    You can use the console or call the DescribeInstances operation to obtain security group IDs of the ECS instances. The following table lists the information of two accounts.

    |Account|Account ID|Security group|Security group ID|
    |-------|----------|--------------|-----------------|
    |Account A|a@aliyun.com|sg1|sg-bp1azkttqpldxgte\*\*\*\*|
    |Account B|b@aliyun.com|sg2|sg-bp15ed6xe1yxeycg\*\*\*\*|

2.  Add a rule to sg1 to allow inbound traffic from sg2.

    ```
    aliyun ecs AuthorizeSecurityGroup --SecurityGroupId sg-bp1azkttqpldxgte**** --RegionId cn-qingdao --IpProtocol all  --PortRange=-1/-1 --SourceGroupId sg-bp15ed6xe1yxeycg7XXX --SourceGroupOwnerAccount b@aliyun.com --NicType intranet
    ```

3.  Add a rule to sg2 to allow inbound traffic from sg1.

    ```
    aliyun ecs AuthorizeSecurityGroup --SecurityGroupId sg-bp15ed6xe1yxeycg**** --RegionId cn-qingdao --IpProtocol all  --PortRange=-1/-1 --SourceGroupId sg-bp1azkttqpldxgtedXXX --SourceGroupOwnerAccount a@aliyun.com --NicType intranet
    ```

    **Note:**

    -   In the preceding commands, the region ID cn-qingdao is for reference only. Replace it with your actual region ID.
    -   In the preceding commands, the AuthorizeSecurityGroup operation is called to add inbound rules to security groups. Specify the SecurityGroupId, SourceGroupId, and SourceGroupOwnerAccount parameters.
4.  After a few minutes, run the ping command to check whether the ECS instances can communicate with each other over the internal network.


