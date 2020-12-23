# Configure interconnection of instances in the classic network

A security group is similar to a firewall for an instance. To ensure security, you must follow the least privilege principle when you configure security group rules for instances. This topic describes four recommended methods to configure interconnection of instances in the classic network.

## Method 1: Authorize access to a single IP address

-   Scenario: This method is applicable to interconnection between a small number of instances over the internal network.
-   Advantages: This method involves simple and clear security group rules to authorize access to a single IP address.
-   Disadvantages: When you attempt to interconnect a large number of instances over the internal network, you are limited of the 200 security group rules and be burdened by a high maintenance workload.

To authorize access to a single IP address, perform the following steps:

1.  Find an instance to be interconnected and click the instance ID.

2.  On the **Instance Details** page, click the **Security Groups** tab.

3.  Find the security group to be configured and click **Add Rules** in the Actions column.

4.  Click the **Inbound** tab.

5.  Click **Add Security Group Rule**.

6.  Configure the following parameters for the security group rule:

    -   **Action**: Allow.
    -   **Priority**: Configure this parameter based on your actual needs. Default value: 1.
    -   **Protocol Type**: Select a protocol type from the drop-down list based on your actual needs.
    -   **Port Range**: Configure a port range based on your actual needs.
    -   **Authorization Object**: Enter the private IP address of the instance to be interconnected. The IP address must be in the a.b.c.d/32 format. The subnet mask must be /32.

        ![Authorize access to a single IP address](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1014488951/p12634.png)

7.  Click **OK**.


## Method 2: Add instances to the same security group

-   Scenario: If your application architecture is relatively simple, you can add all instances to the same basic security group. By default, instances in the same basic security group can access each other over the internal network.
-   Advantages: Security group rules are simple and clear.
-   Disadvantage: This method is applicable only to a simple network architecture. When the network architecture is adjusted, the authorization method must be modified accordingly.

For more information about the procedure, see [Add an ECS instance to a security group](/intl.en-US/Security/Security groups/Add an ECS instance to a security group.md).

## Method 3: Add instances to a security group created solely for interconnection

-   Scenario: You can add the instances to a dedicated basic security group for interconnection. This method is recommended for a network architecture that has multiple layers of applications.
-   Advantages: This method is easy to implement and allows you to quickly establish interconnection between instances. The method is applicable to complicated network architectures.
-   Disadvantages: The instances are added to multiple security groups and the security group rules may be complex.

To add instances to a security group created solely for interconnection, perform the following steps:

1.  Create a basic security group that has a name configured such as security group for interconnection. No rules are required for the new security group.

2.  Add the instances to be interconnected to the new security group. Instances in the same basic security group can communicate with each other.


## Method 4: Authorize security groups

-   Scenario: You can add the instances to a dedicated security group for interconnection. This method is recommended for a network architecture that has multiple layers of applications.
-   Advantages: This method is easy to implement and allows you to quickly establish interconnection between instances. The method is applicable to complicated network architectures.
-   Disadvantages: The instances are added to multiple security groups and the security group rules may be complex.

To authorize security groups, perform the following steps:

1.  Find an instance to be interconnected and click the instance ID.

2.  On the **Instance Details** page, click the **Security Groups** tab.

3.  Find the security group to be configured and click **Add Rules** in the Actions column.

4.  Click the **Inbound** tab.

5.  Click **Add Security Group Rule**.

6.  Configure the following parameters for the security group rule:

    -   **Action**: Allow.
    -   **Priority**: Configure this parameter based on your actual needs. Default value: 1.
    -   **Protocol Type**: Select a protocol type from the drop-down list based on your actual needs.
    -   **Port Range**: Configure a port range based on your actual needs.
    -   **Authorization Object**:
        -   Instance in the same account as the current instance: Enter the security group ID to which the instance to be interconnected belongs.
        -   Instance in a different account from the current instance: Enter the ID of the account and the ID of the security group to which the instance to be interconnected belongs. The IDs must be in the <Account ID/security group ID\> format.
7.  Click **OK**.


## Suggestions

If you determine that an inappropriate level of access has been granted by using the applied security group, we recommend that you downgrade the level of access by using the following procedure.

![Monitoring flowchart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1014488951/p12637.png)

In the preceding figure, **Delete 0.0.0.0** means deleting the original security group rule that allows inbound traffic from 0.0.0.0/0.

If one or more security group rules are improperly configured, the interconnection between your instances may be affected. We recommend that you back up security group rules before you change them so that you can easily recover the rules.

A security group maps the role of an instance in the overall application architecture. We recommend that you plan the firewall rules based on the application architecture. For example, in a common three-tier web application architecture, you can plan three security groups and add instances deployed with applications or databases to the corresponding security groups.

-   Web layer security group: allows port 80.
-   Application layer security group: allows port 8080.
-   Database layer security group: allows port 3306.

