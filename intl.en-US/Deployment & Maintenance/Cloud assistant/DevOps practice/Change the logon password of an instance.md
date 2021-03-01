---
keyword: [change instance password, no need to restart, reset instance password]
---

# Change the logon password of an instance

If you do not specify a password when you create an ECS instance or forget the password of an instance, you can use Cloud Assistant to change the password of the instance. You can also reset the password in the console. However, the password changed by using Cloud Assistant takes effect without the need to restart the instance.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Click the ID of the instance for which you want to run the Cloud Assistant command to go to the **Instance Details** page.

5.  Click the **Remote Commands/Files** tab and click **Send Command**.

6.  Configure parameters to change the instance password. The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Command Type**|The type of the command.    -   For Linux instances, **Shell** is selected by default.
    -   For Windows instances, select **Bat** or **PowerShell**. |
    |**Retain Command**|Specifies whether to save the command.After you save the command, you can use Cloud Assistant to view, modify, and run the command again. |
    |**Command Content**|The content of the command used to change the instance password. Run one of the following commands based on the operating system of your instance:    -   Linux:

        ```
echo "root:<yourPassword\>"|chpasswd
        ```

    -   Windows:

        ```
net user "Administrator" "<yourPassword\>"
        ```

**Note:**

    -   Replace <yourPassword\> with your new password.
    -   The password must be 8 to 30 characters in length. It must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. The password of a Windows instance cannot start with a forward slash \(/\). |

7.  Click **Run**.


If **Success** is displayed in the **Command Output** section, the password is changed. Then, you can check whether the new password can be used to log on to the instance. For more information about how to log on to the instance, see [Guidelines on instance connection](/intl.en-US/Instance/Connect to instances/Overview.md).

