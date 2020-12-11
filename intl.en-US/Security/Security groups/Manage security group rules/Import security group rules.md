# Import security group rules

Security group rules can be imported to security groups. You can export the rules of a security group to a file, and then import the file to other security groups or the original security group. This is a quick and easy way to create or restore security group rules.

You can import security group rules from different regions.

You can choose **Export Rules** \> **JSON Format** on the Security Group Rules page of a security group to download and save the security group rules to a local JSON file. You can modify the JSON file and add custom security group rules in the required format.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.

3.  In the top navigation bar, select a region.

4.  On the Security Groups page, find the security group to which you want to import rules and click **Add Rules** in the **Actions** column.

5.  Click **Import Rules** in the upper-right corner.

6.  In the **Import Security Group Rule** dialog box, click **Select a file** and then select the local JSON file that you want to import.

    The dialog box provides a preview of the rules in the file. The following information about the rules is displayed:

    -   The number of rules to be imported.
    -   The result of the import check. If any rules fail the import check, you can move the pointer over the warning icon for details.
    -   Details of the rules.
    **Note:** You can import a maximum of 200 security group rules to a security group. The newly imported rules do not overwrite the existing rules. Excess rules cannot be imported to the security group when the maximum number of rules in the security group is reached.

7.  Click **Start**.

8.  Check the import result, and click **Finish and Close**.


