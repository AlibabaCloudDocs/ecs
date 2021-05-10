# Deploy SVN by using svnserve

This topic describes how to use svnserve to deploy Apache Subversion \(SVN\).

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   An Elastic Compute Service \(ECS\) instance of the ecs.g6.large instance type is created and runs a CentOS operating system. For more information about how to create an ECS instance, see [Creation method overview](/intl.en-US/Instance/Create an instance/Creation method overview.md).
-   Inbound rules are added to the security groups of the instance to allow traffic on port 3690, which is the default port of SVN. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

The following software versions are used in the example to manually deploy SVN. The operations may vary based on the versions of your software.

-   Operating system: CentOS 7.2 64-bit public image
-   SVN: 1.7.14

## Procedure

-   [Step 1: Install SVN](#section_h54_dqf_pyz)
-   [Step 2: Configure SVN](#section_qui_xbb_dke)
-   [Step 3: Use a Windows client to test the SVN service](#section_frq_nei_7ay)

## Step 1: Install SVN

1.  [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

2.  Run the following command to install SVN:

    ```
    yum install subversion
    ```

3.  Run the following command to check the SVN version:

    ```
    svnserve --version
    ```

    ![Check the SVN version](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9729919951/p12528.png)


## Step 2: Configure SVN

1.  Run the following command to create a root directory for an SVN repository:

    ```
    mkdir /var/svn
    ```

2.  Run the following commands in sequence to create an SVN repository.

    ```
    cd /var/svn
    ```

    ```
    svnadmin create /var/svn/svnrepos
    ```

3.  Run the following commands in sequence to check the files that are automatically generated in the SVN repository:

    ```
    cd svnrepos
    ```

    ```
    ls
    ```

    ![Check the files in the SVN repository](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1829919951/p12529.png)

    The following table describes the SVN directories.

    |Directory|Description|
    |---------|-----------|
    |db|Stores all version control data files.|
    |hooks|Stores hook scripts.|
    |locks|The client used to track access to the SVN repository.|
    |format|The text file that contains a single integer value which indicates the version number of the current SVN repository.|
    |conf|The configuration file of the SVN repository, which stores the usernames and permissions for accessing the repository.|

4.  Configure the username and password of the SVN repository.

    1.  Run the `cd conf/` command.

    2.  Run the `vi passwd` command to open the configuration file.

    3.  Press the `I` key to enter the edit mode.

    4.  Move the pointer to `[users]` and add the username and password.

        **Note:** You can add the username and password in the username = password format, such as userTest = passWDTest shown in the following figure. You must add a space before and after the equal sign \(=\).

        ![svn-3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7168260261/p101210.png)

    5.  Press the `Esc` key to exit the edit mode, and enter `:wq` to save and close the file.

5.  Configure the read and write permissions for the account.

    1.  Run the `vi authz` command to open the access control file.

    2.  Press the `I` key to enter the edit mode.

    3.  Move the pointer to the end of the file and add the following code. In the code, userTest specifies the username, r specifies the read permission, and w specifies the write permission.

        ```
        [/]
        userTest=rw
        ```

        ![svn-4](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7168260261/p101211.png)

    4.  Press the `Esc` key to exit the edit mode, and enter `:wq` to save and close the file.

6.  Modify the configurations of the SVN service.

    1.  Run the `vi svnserve.conf` command to open the configuration file of the SVN service.

    2.  Press the `I` key to enter the edit mode.

    3.  Move the pointer to the following lines and delete the number sign \(\#\) and space from the beginning of each line:

        **Note:** Each line cannot start with a space. You must add a space before and after the equal sign \(=\).

        ```
        anon-access = read #Grants read permissions to anonymous users. You can also set anon-access to none to deny access by anonymous users. If you set anon-access to none, the revision history of the SVN service can show dates properly.
        auth-access = write #Grants write permissions.
        password-db = passwd #Specifies the password database file.
        authz-db = authz #Specifies the file that stores the authorization rules for path-based access control.
        realm = /var/svn/svnrepos #Specifies the authentication realm of the repository.
        ```

        ![Modify the configurations of the SVN service](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1829919951/p12532.png)

    4.  Press the `Esc` key to exit the edit mode, and enter `:wq` to save and close the file.

7.  Run the following command to start the SVN repository:

    The absolute path to the SVN repository is specified in the following example command:

    ```
    svnserve -d -r /var/svn/svnrepos/
    ```

    **Note:** You can run the `killall svnserve` command to stop the SVN service.

8.  Run the `ps -ef |grep svn` command to check whether the SVN service is started.

    A command output similar to the following one indicates that the SVN service is started.

    ![Check the status of SVN service](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9040977161/p12533.png)


## Step 3: Use a Windows client to test the SVN service

1.  Download and install the [TortoiseSVN client](http://tortoisesvn.net/downloads.html) on your local computer.

2.  Right-click the blank area in the local project folder.

    In this example, the project folder is C:\\KDR.

3.  Select **SVN Checkout...** from the shortcut menu.

4.  Configure the following settings and click **OK**:

    -   In the **URL of repository:** field, enter the URL of the SVN repository from which to check out a working copy. In these examples, the SVN service is started by using the `svnrepos` repository and svnserve works only for the svnrepos repository. The URL of the SVN repository is in the format of svn://<Public IP address of the instance\>.
    -   In the **Checkout directory:** field, enter a directory to which to check out a working copy from the specified SVN repository. In this example, the directory is C:\\Test.
    **Note:** On you first logon, you must provide the username and password that you have configured in the passwd file.


