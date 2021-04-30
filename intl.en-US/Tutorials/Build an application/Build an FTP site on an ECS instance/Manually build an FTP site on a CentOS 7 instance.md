---
keyword: [build an FTP site, build an FTP site on a CentOS 7.2 instance, build an FTP site on a CentOS 7 instance]
---

# Manually build an FTP site on a CentOS 7 instance

Very secure FTP daemon \(vsftpd\) is a lightweight, safe, and easy-to-use FTP server software for Linux. This topic describes how to install and configure vsftpd on a Linux Elastic Compute Service \(ECS\) instance.

An ECS instance is created and assigned a public IP address. If no ECS instance is created, create an ECS instance. For more information, see [Creation method overview](/intl.en-US/Instance/Create an instance/Creation method overview.md).

FTP is a protocol used to transfer files. FTP is built on a client-server model architecture and supports the following working modes:

-   Active mode: The client sends port information to the FTP server, and the server establishes a connection to the port.
-   Passive mode: The FTP server enables a port and sends the port information to the client. The client initiates a connection to the port, and the server accepts the connection.

**Note:** Most FTP clients are located in LANs, have no independent public IP addresses, and are protected by firewalls. This makes it difficult for FTP servers in active mode to establish connections to the clients. We recommend that you use passive mode for the FTP server if you do not have special requirements.

FTP supports the following authentication modes:

-   Anonymous user mode: In this mode, users can log on to the FTP server without a username or password. This is the least secure authentication mode. In most cases, this mode is used to save unimportant public files. We recommend that you do not use this mode to save files in a production environment
-   Local user mode: This authentication mode requires users to have local Linux accounts. This mode is more secure than the anonymous user mode.
-   Virtual user mode: Virtual users are dedicated users of the FTP server. Virtual users can access only the FTP service that the Linux system provides. Virtual users cannot access other resources of the system. This way, the security of the FTP server is further enhanced.

In this topic, vsftpd is configured in passive and local user mode. For information about how to configure an FTP server to allow anonymous users to access the FTP server and information about how to use the tools on third-party FTP clients, see [FAQ](#section_q6i_wdk_m96).

The following resources are used in the procedure described in this topic:

-   Instance type: ecs.c6.large
-   Operating system: CentOS 7.2 64-bit
-   vsftpd: 3.0.2

The commands and parameters used in this topic may vary based on your resources.

## Step 1: Install vsftpd

1.  Connect to the Linux instance.

    For more information about how to connect to a Linux instance, see [Connection methods](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the following command to install vsftpd:

    ```
    yum install -y vsftpd
    ```

    If the page shown in the following figure appears, vsftpd is installed.

    ![install_vsftp_successfully](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2529919951/p12598.png)

3.  Run the following command to enable the FTP service to automatically start on system startup:

    ```
    systemctl enable vsftpd.service
    ```

4.  Run the following command to start the FTP service:

    ```
    systemctl start vsftpd.service
    ```

    **Note:** If the system returns the Job for vsftpd.service failed because the control process exited with error code error message when the preceding command is run, check whether the following problems exist and troubleshoot them. If the problems persist, submit a ticket.

    -   If the network environment does not support IPv6 addresses, run the vim /etc/vsftpd/vsftpd.conf command to change the value of listen\_ipv6 from `YES` to `NO`.
    -   If the MAC address that is specified in the /etc/sysconfig/network-scripts/ifcfg-xxx configuration file does not match the actual MAC address, run the ifconfig command to query the MAC address. Then, add `HWADDR=<The actual MAC address>` to the configuration file. You can also change HWADDR in the configuration file to the actual MAC address.
5.  Run the following command to query the listening port of the FTP service:

    ```
    netstat -antup | grep ftp
    ```

    If the following page appears, the FTP service is started and listens to port 21. By default, anonymous access is enabled in vsftpd. You can log on to the FTP server without a username or password. However, you do not have the permissions to modify or upload files.

    ![install_vsftpd_3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2529919951/p12600.png)


## Step 2: Configure vsftpd

In this example, vsftpd is configured in passive and local user mode to ensure data security.

1.  Run the following command to create a Linux user for the FTP service. In this example, the ftptest username is used.

    ```
    adduser ftptest
    ```

2.  Run the following command. Follow the instructions in the command line to modify the password of the ftptest user.

    ```
    passwd ftptest
    ```

3.  Run the following command to create a file directory for the FTP service:

    ```
    mkdir /var/ftp/test
    ```

4.  Run the following command to create a test file.

    This test file is used when the FTP client accesses the FTP server.

    ```
    touch /var/ftp/test/testfile.txt
    ```

5.  Run the following command to change the owner of the /var/ftp/test directory to ftptest:

    ```
    chown -R ftptest:ftptest /var/ftp/test
    ```

6.  Modify the vsftpd.conf configuration file.

    1.  Run the following command to open the configuration file of vsftpd.

        If you use the `apt install vsftpd` command to install vsftpd, the path of the configuration file is /etc/vsftpd.conf.

        ```
        vim /etc/vsftpd/vsftpd.conf
        ```

    2.  Press the I key to enter the edit mode.

    3.  Enable passive mode for the FTP server.

        Configure the following parameters:

        **Note:** When you modify or add information in the configuration file, take note of the format. For example, an extra space may cause the service to fail to restart.

        ```
        #Use the default values for all parameters except the following parameters: 
        
        #Modify the values of the following parameters:
        #Disallows anonymous users to log on to the FTP server. 
        anonymous_enable=NO
        #Allows local users to log on to the FTP server. 
        local_enable=YES
        #Listens to IPv4 sockets. 
        listen=YES
        
        #Add a number sign (#) to the beginning of the row to comment out the following parameter:
        #Disables listening to IPv6 sockets. 
        #listen_ipv6=YES
        
        #Add the following parameters at the end of the configuration file:
        #Specifies the directory to which local users are directed after they log on. 
        local_root=/var/ftp/test
        #Limits all users to their home directory after they log on. 
        chroot_local_user=YES
        #Uses a list to specify exception users. Exception users are not limited to the home directory after they log on. 
        chroot_list_enable=YES
        #Specifies a file to contain the list of exception users. 
        chroot_list_file=/etc/vsftpd/chroot_list
        #Enables passive mode. 
        pasv_enable=YES
        allow_writeable_chroot=YES
        #In this topic, the public IP address of the Linux instance is used. 
        pasv_address=<The public IP address of the FTP server>
        #Specifies the minimum port number of the port range that can be used to transmit data in passive mode. 
        We recommend that you use ports in a high number range, such as 50000 to 50010. These ports provide more secure access to the FTP server. 
        pasv_min_port=<port number>
        #Specifies the maximum port number of the port range that can be used to transmit data in passive mode. 
        pasv_max_port=<port number>
        ```

        For more information, see [vsftpd configuration file and parameters](/intl.en-US/Tutorials/Build an application/Build an FTP site on an ECS instance/Manually build an FTP site on a CentOS 7 instance.md).

    4.  Press the Esc key to exit the edit mode. Enter :wq and press the Enter key to save and close the file.

7.  Create the chroot\_list file, and write the list of exception users to the file.

    1.  Run the following command to create the chroot\_list file:

        ```
        vim /etc/vsftpd/chroot_list
        ```

    2.  Press the I key to enter the edit mode.

    3.  Enter the list of exception users. Exception users are not limited to the home directory and have access to other directories.

    4.  Press the Esc key to exit the edit mode. Enter :wq and press the Enter key to save and close the file.

    **Note:** If exception users do not exist, you must still create the chroot\_list file. The file can be empty.

8.  Run the following command to restart vsftpd:

    ```
    systemctl restart vsftpd.service
    ```


## Step 3: Configure security groups

After you build the FTP site, add inbound rules for security groups to allow traffic on the following FTP ports. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

**Note:** Most clients are located in LANs and can map their private IP addresses to public IP addresses to communicate with external resources. Therefore, the IP addresses returned by the ipconfig or ifconfig command may not be the actual public IP addresses of the clients. If you cannot log on to the FTP server from the client, check the public IP address of the client.

In passive mode, you must configure the security group rules to allow traffic on port 21 and on all ports in the port range specified by pasv\_min\_port and pasv\_max\_port in the /etc/vsftpd/vsftpd.conf configuration file. The following table describes the configuration details.

|Rule direction|Authorization policy|Protocol type|Port range|Authorized object|
|--------------|--------------------|-------------|----------|-----------------|
|Inbound|Allow|Custom TCP|21/21|The public IP addresses in CIDR block notation of all clients that need to access the FTP server. Separate the IP addresses with commas \(,\). To allow all clients to access the FTP server, specify 0.0.0.0/0 as an authorization object. |
|Inbound|Allow|Custom TCP|pasv\_min\_port/pasv\_max\_port. Example: 50000/50010.|The public IP addresses in CIDR block notation of all clients that need to access the FTP server. Separate the IP addresses with commas \(,\). To allow all clients to access the FTP server, specify 0.0.0.0/0 as an authorization object. |

## Step 4: Check whether you can access the FTP server from the client

To check whether FTP servers are accessible, you can use FTP clients, Windows command-line tools, or browsers. In this example, a host that runs Windows Server 2012 R2 64-bit operating system is used to describe how to access an FTP server.

1.  On the local host, open **This Computer**.

2.  In the address bar, enter `ftp://<The public IP address of the FTP server>:<The FTP port>`. In this example, the following public IP address of the Linux instance is used: `ftp:// 121.43.XX.XX:21`

3.  In the **Log on as** dialog box, enter the FTP username and password that you configured, and then click **Logon**.

    After you log on, you can view the files under the specified directory in the FTP server, for example, the test file named testfile.txt.


## vsftpd configuration file and parameters

The following section describes the files under the /etc/vsftpd directory:

-   /etc/vsftpd/vsftpd.conf is the core configuration file of vsftpd.
-   /etc/vsftpd/ftpusers is the blacklist file. Users specified in this file are not allowed to access the FTP server.
-   /etc/vsftpd/user\_list is the whitelist file. Users specified in this file are allowed to access the FTP server.

The following section describes the parameters in the vsftpd.conf configuration file.

-   The following table describes the parameters for logon control.

    |Parameter setting|Description|
    |:----------------|:----------|
    |anonymous\_enable=YES|Accepts anonymous users.|
    |no\_anon\_password=YES|Anonymous users do not need a password to log on to the FTP server.|
    |anon\_root= \(none\)|Specifies the home directory of anonymous users.|
    |local\_enable=YES|Accepts local users.|
    |local\_root= \(none\)|Specifies the home directory of local users.|

-   The following table describes the parameters that are used to manage the permissions of users.

    |Parameter setting|Description|
    |:----------------|:----------|
    |write\_enable=YES|Allows all users to upload files.|
    |local\_umask=022|Grants local users the permission to upload files.|
    |file\_open\_mode=0666|Uses umask for permissions to upload files.|
    |anon\_upload\_enable=NO|Allows anonymous users to upload files.|
    |anon\_mkdir\_write\_enable=NO|Allows anonymous users to create directories.|
    |anon\_other\_write\_enable=NO|Allows anonymous users to modify and delete files.|
    |chown\_username=lightwiter|Specifies the ownership of files that are uploaded by anonymous users.|


## FAQ

-   Question 1: What do I do if I am unable to download files from the FTP server when the local host runs a Windows operating system?

    Answer: You must perform the following operations to enable the download permission in Internet Explorer.

    1.  Open Internet Explorer in your local host.
    2.  Click the ![The Internet Explorer icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1272579161/p261673.png) icon in the upper-right corner of the browser, and then click **Internet Options**.
    3.  At the top of the **Internet Options** dialog box, click the **Security** tab.
    4.  In the **Select a zone to view or change security settings.** section, click **Internet**, and then click **Custom level...** in the **Security level for this zone** section.
    5.  Choose **Download** \> **File Download** \> **Enable**, and then click **OK**.
    6.  Click **Apply** and then click **OK**.
-   Question 2: What do I do if an error is reported when I use a command-line tool or a browser to connect to an FTP server on Windows?

    Answer: You can manually troubleshoot the problem based on the error message about the FTP server. If the problem is difficult to troubleshoot, we recommend that you use a third-party FTP client connection tool such as FileZilla. You can download FileZilla from [FileZilla](https://filezilla-project.org/download.php). In this example, FileZilla is used to connect to an FTP server in anonymous mode.

    **Note:** If the error reported persists when the FTP server is connected to, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

    1.  On the FTP server on Linux, install vsftpd.

        For more information, see [Step 1: Install vsftpd](#section_821_887_8np). If vsftpd is installed, skip this step.

    2.  Configure vsftpd as anonymous mode.
        1.  Run the following command to modify the /etc/vsftpd/vsftpd.conf configuration file.

            If you use the `apt install vsftpd` command to install vsftpd, the path of the configuration file is /etc/vsftpd.conf.

            ```
            vim /etc/vsftpd/vsftpd.conf
            ```

        2.  Press the I key to enter the edit mode.
        3.  Comment out the permissions and set `anon_upload_enable` to YES to allow anonymous users to upload files.
        4.  Press the Esc key to exit the edit mode. Enter :wq and press the Enter key to save and close the file.

            The following figure shows the modified configuration file.

            ![The configuration file of vsftpd](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9418773061/p102865.png)

        5.  Run the following command to change the permissions of the /var/ftp/pub directory and grant write permissions to FTP users:

            /var/ftp/pub is the default file directory of the FTP service.

            ```
            chmod o+w /var/ftp/pub/
            ```

        6.  Run the following command to reload the configuration file:

            ```
            systemctl restart vsftpd.service
            ```

    3.  Download and install FileZilla.
    4.  Use FileZilla to connect to the FTP server in anonymous mode.
        1.  Open the FileZilla client.
        2.  In the top navigation bar, choose **File** \> **Site Manager**.
        3.  In the lower-left corner of the **Site Manager** dialog box, click **New site**.
        4.  Enter a name for the new site and configure the new site.

            ![filezilla](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1272579161/p261708.png)

            The following list describes the parameters:

            -   Name: a custom site name. Example, `test-01`.
            -   Protocol: FTP.
            -   Host: the public IP address of the FTP server. In this topic, the value is the public IP address of the Linux instance. For example, `121.43.XX.XX`.
            -   Port: 21.
            -   Logon Type: Anonymous.

                In this example, an FTP client is used to connect to the FTP server in anonymous mode. If you want to manage access to the FTP server, set the logon type to normal and configure the username and password.

        5.  Click **Connect**.

            After the FTP server is connected to, you can upload, download, and delete files. The FileZilla interface is shown in the following figure.

            ![filezilla](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1272579161/p261717.png)

            The following table describes the sections in the preceding interface.

            |No.|Description|
            |---|-----------|
            |①|Commands, the connection status of the FTP server, and task execution results are shown.|
            |②|The section for the information about the local host, in which the directory information of the local host is shown.|
            |③|The section for the information about the remote server, in which the directory information of the FTP server is shown. In anonymous mode, the default directory is /pub.|
            |④|The section for records, in which the queues and logs of the FTP task is shown.|


Perform security hardening on the FTP service. For more information, see [FTP anonymous logon and weak password vulnerabilities](https://www.alibabacloud.com/help/zh/doc-detail/37452.htm).

