# Change the logon password of an instance by connecting to the instance

You can change the logon password of an instance without going to the console when you perform operations on the instance. The change takes effect immediately and you do not need to restart the instance. This topic describes how to change the logon passwords of a Linux instance and a Windows instance by connecting to the instances. Windows and CentOS are used in the examples.

## Change the logon password of a Linux instance

An instance that runs CentOS 7.6 is used in this example. Perform the following operations to change the logon password of the Linux instance:

1.  Log on to the instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the passwd <username\> command. Example: passwd root.

3.  Enter a new password.

4.  Enter the new password again to confirm the password.


## Change the logon password of a Windows instance

An instance that runs Windows Server 2012 is used in this example. Perform the following operations to change the logon password of the Windows instance:

1.  Log on to the instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Choose **Start** \> **Run**, enter compmgmt.msc, and then press the Enter key.

3.  In the Computer Management window, choose **System Tools** \> **Local Users and Groups** \> **Users**.

4.  Right-click the username for which you want to change the password. Example: **Administrator**.

5.  Select **Set Password**.

6.  In the Set Password for Administrator dialog box, click **Proceed**. In the dialog box that appears, enter a new password in the **New password** and **Confirm password** fields, and then click **OK**.


[Reboot the instance](/intl.en-US/Instance/Manage instance status/Restart an instance.md)

[RebootInstance](/intl.en-US/API Reference/Instances/RebootInstance.md)

