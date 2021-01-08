# Manually build an FTP site on a Windows instance

This topic describes how to build an FTP site on a Windows instance. This method is applicable to Windows Server 2008 and later. Windows Server 2012 R2 is used in this example.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).

-   An ECS instance is created. The following resources are used in this topic:
    -   Instance type: ecs.c6.large
    -   Operating system: Windows Server 2012 R2 64-bit

## Procedure

To build an FTP site on a Windows instance, perform the following operations:

1.  [Step 1: Add Internet Information Services \(IIS\) and FTP server roles](#section_qx9_w5k_gvc)
2.  [Step 2: Create an FTP username and password](#section_ztx_c4b_edr)
3.  [Step 3: Configure permissions on a shared file](#section_jd9_tsn_noi)
4.  [Step 4: Create and configure an FTP site](#section_0gy_5s5_oku)
5.  [Step 5: Configure security groups and the firewall](#section_ovb_r91_w7d)
6.  [Step 6: Test the client](#section_xex_vgd_epn)

## Step 1: Add Internet Information Services \(IIS\) and FTP server roles

You must install IIS and FTP services before you build an FTP site.

1.  Connect to the target Windows ECS instance. For more information, see [Connect to a Windows instance from a local client](/intl.en-US/Instance/Connect to instances/Connect to Windows instances/Connect to a Windows instance from a local client.md).

2.  In the taskbar, click the **Server Manager** icon.

    ![ftp0](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5529919951/p92900.png)

3.  In the top navigation bar, choose **Manage** \> **Add Roles and Features**.

4.  In the dialog box that appears, keep the default settings and click **Next** to go to the Select server roles step.

5.  Select **Web Server \(IIS\)**. In the message that appears, click **Add Features** and then click **Next**.

    ![ftp2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5529919951/p92895.png)

6.  In the Select role services step, select **IIS Management Console** and **FTP Server**, and then click **Next**.

    ![ftp3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5529919951/p92899.png)

7.  Click **Install**.


## Step 2: Create an FTP username and password

To create a username and password for FTP, perform the following operations. If you want to allow access to the site from anonymous users, skip this step.

1.  In the taskbar, click **Start**.

2.  Click **Administrative Tools** and double-click **Computer Management**.

3.  In the left-side navigation pane, choose **Local Users and Groups** \> **Users**.

    ![ftp4](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5529919951/p92902.png)

4.  Right-click anywhere in the blank space in the middle and select **New User...**

    The ftptest username is used in this example.

    **Note:** The password must contain uppercase letters, lowercase letters, and digits. Otherwise, the password is invalid.


## Step 3: Configure permissions on a shared file

You must configure the access and modification permissions on the folder shared to users on the FTP site.

1.  Create a folder for FTP on the server disk. Right-click the folder and select **Properties**.

    In this example, a folder named ftp is created on disk C.

2.  Click the **Security** tab and click **Edit**.

3.  Click **Add**.

4.  In the dialog box that appears, enter ftptest as the object name and click **OK**.

5.  In the **Group or user names** section, click the **ftptest** username, select permissions for **ftptest**, and then click **OK**.

    In this example, all permissions are granted.


## Step 4: Create and configure an FTP site

After you install FTP and configure permissions on the shared folder, perform the following operations to create an FTP site:

1.  In the taskbar, click the **Server Manager** icon.

2.  In the top navigation bar, choose **Administrative Tools** \> **Internet Information Services \(IIS\) Manager**.

3.  In the left-side navigation pane, right-click **Sites** and select **Add FTP Site...**.

    ![ftp9](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5529919951/p92920.png)

4.  In the dialog box that appears, enter the **FTP site name** and **Physical path** of the shared folder, and then click **Next**.

5.  Keep the default **All Assigned** selection for the **IP Address** field. You can configure a port number. The default FTP port is 21.

6.  Select one of the following options for the SSL field and click **Next**.

    -   **Allow SSL**: allows the FTP server to connect to the client in the both SSL encrypted and unencrypted states.
    -   **Require SSL**: requires SSL encryption for communication between the FTP server and the client.
    -   **No SSL**: does not require SSL encryption.
7.  Select one or more authentication methods.

    -   **Anonymous**: allows users that provide the **anonymous** or **ftp** username to access the content.
    -   **Basic**: requires users to provide valid usernames and passwords to access the content. Basic authentication transmits unencrypted passwords across the network. We recommend that you use basic authentication only when you are sure that the connection between the client and the FTP server is secure, such as when Secure Sockets Layer \(SSL\) encryption is used.
8.  Select one of the following options from the **Allow access to:** drop-down list:

    -   **All users**: All users, both anonymous and identified users, can access the relevant content.
    -   **Anonymous users**: Anonymous users can access the relevant content.
    -   **Specified roles or user groups**: Only specific roles or members of the specified user group can access the relevant content. Enter the role or user group in the corresponding field.
    -   **Specified users**: Only specified users can access the relevant content. Enter the usernames in the corresponding field.
9.  Select the **Read** and **Write** permissions for the authorized users. Click **Finish**.


After the preceding operations are complete, you can view information about the FTP site.

## Step 5: Configure security groups and the firewall

1.  After you build the FTP site, you must add inbound security group rules to allow traffic on port 21 and passive port 1024/65535 of the FTP server.

    For more information about the procedure, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md). For more information about the specific configurations, see [Scenarios for security groups](/intl.en-US/Security/Security groups/Scenarios for security groups.md) and [Common ports used by applications](/intl.en-US/Security/Security groups/Typical applications of commonly used ports.md).

2.  The server firewall is disabled by default. If your firewall is enabled, allow traffic on TCP ports 21 and ports from 1024 to 65535 for the FTP service.

    For more information about firewall configurations, visit [Build an FTP Site on IIS](https://technet.microsoft.com/zh-cn/library/hh831655(v=ws.11).aspx#Step4).


## Step 6: Test the client

FTP tools, Windows command-line tools, or browsers can be used to test FTP servers. Google Chrome is used in this example to describe how to access an FTP server.

1.  Open Google Chrome on the client to visit `ftp://<The public IP address of the instance>:<port number>` \(If no port is specified, port 21 is used by default\).

    **Note:** If an error occurs when you use a browser to access the FTP server, clear the browser cache and try again.

2.  In the dialog box that appears, enter the **ftptest** username and corresponding password to access the FTP site and perform authorized operations on the FTP file.

    If you use a browser to access the FTP server, you have the read-only permissions on FTP files. Therefore, we recommend that you use an FTP tool such as FileZilla to perform more operations on FTP files.

    **Note:** This step applies only to basic authentication. Anonymous users can log on to the FTP server without entering the username and password.


You can perform security enhancement on the FTP service. For more information, see [FTP anonymous logon and weak password vulnerabilities](https://www.alibabacloud.com/help/zh/doc-detail/37452.htm).

If you want to manage files stored on Object Storage Service \(OSS\) based on FTP, you can install ossftp. For more information, see [Quick installation of ossftp](/intl.en-US/Tools/ossftp/Use ossftp.md). After ossftp receives a common FTP request, ossftp will map operations on files and folders as operations on OSS.

