# Remove an instance from a security group

You can remove instances from security groups. When an ECS instance is removed from a security group, the instance is isolated from all the other ECS instances in the security group. We recommend that you perform tests in advance to ensure that services can continue to run properly after the instance is removed from the security group.

The instance is added to two or more security groups.

You can use one of the following methods to remove instances from a security group:

-   For information about how to remove a single instance from a security group, see [Remove a single instance](#section_phz_eik_vpz).
-   For information about how to remove multiple instances from a security group, see [Remove multiple instances](#section_3ru_84y_ves).

## Remove a single instance

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  On the Instances page, find the instance to be removed from a security group, and click **Manage** in the **Actions** column.

5.  The Instance Details tab appears. Click the **Security Groups** tab.

6.  Find the security group from which you want to remove the instance, and click **Remove** in the **Actions** column.

7.  Click **OK**.


## Remove multiple instances

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.

3.  In the top navigation bar, select a region.

4.  On the Security Groups page, find the security group from which you want to remove instances, and click the security group ID.

5.  In the left-side navigation pane, click **Instances in Security Group**.

6.  Select one or more instances, and click **Remove from Security Group**.

7.  Click **OK**.


**Related topics**  


[ModifyInstanceAttribute](/intl.en-US/API Reference/Instances/ModifyInstanceAttribute.md)

[ModifyNetworkInterfaceAttribute](/intl.en-US/API Reference/Elastic network interfaces/ModifyNetworkInterfaceAttribute.md)

