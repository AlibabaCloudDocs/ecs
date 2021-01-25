---
keyword: Restore security group rules
---

# Restore security group rules

This topic describes how to restore rules from one security group to another. For example, if you want to apply new security group rules to an ECS instance that is running an online application, you can clone the security group to make a backup, and then modify the rules. If the new security group rules affect the online application, you can perform a complete or partial restoration of the security group rules.

-   The security group whose rules are to be restored \(source security group\) and the security group based on which rules in the source security group are to be restored \(destination security group\) must be in the same region.
-   The source security group and the destination security group must be of the same network type.

When you restore security group rules, you fully or partially restore the rules from the destination security group to the source security group.

-   **Completely Restore**: deletes the rules that do not exist in the destination security group from the source security group, and adds the rules that exist only in the destination security group to the source security group. After the restoration is complete, the source security group has the same rules as the destination security group.
-   **Partially Restore**: adds the rules that exist only in the destination security group to the source security group, and ignores the rules that exist only in the source security group.

**Note:**

Restoring security group rules has the following limits: If system-level security group rules with a priority of 110 exist in the destination security group, these rules cannot be created during restoration. Rules in the source security group after restoration may not be as expected. If you need the system-level security group rules, you must manually create them and set their priority to 100.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.

3.  In the top navigation bar, select a region.

4.  On the Security Groups page, find the security group whose rules you want to restore and click **Restore Rules** in the **Actions** column.

5.  In the Restore Rules dialog box, perform the following operations:

    1.  Set **Destination Security Group**. The specified destination security group must have rules different from those in the source security group.

    2.  Set **Restoration Type**.

        -   If you want the source security group to have the same rules as the destination security group, select **Completely Restore**.
        -   If you want to add the rules that exist only in the destination security group to the source security group, select **Partially Restore**.
    3.  Preview the restoration result.

        -   The rules highlighted in green exist only in the destination security group. These rules are added to the source security group regardless of whether you select **Completely Restore** or **Partially Restore**.
        -   The rules highlighted in red do not exist in the destination security group.
            -   If you select **Completely Restore**, these rules are removed from the source security group.
            -   If you select **Partially Restore**, these rules are retained in the source security group.
    4.  Click **OK**.

        After the rules are restored, the Restore Rules dialog box is closed.


On the **Security Groups** page, find the source security group, and then click **Add Rules** in the **Actions** column. On the Security Group Rules page, you can view the updated security group rules.

