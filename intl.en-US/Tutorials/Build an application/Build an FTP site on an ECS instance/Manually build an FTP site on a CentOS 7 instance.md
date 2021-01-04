---
keyword: [build an FTP site, build an FTP site on a Linux ECS instance running CentOS 7.2, build an FTP site on a Linux ECS instance running CentOS 7]
---

# Manually build an FTP site on a CentOS 7 instance

Very secure FTPdaemon \(vsftpd\) is a lightweight, safe, and easy-to-use File Transfer Protocol \(FTP\) server software for Linux. This topic describes how to install vsftpd on a Linux ECS instance.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   An ECS instance is created and assigned a public IP address. If not, see [Creation method overview](/intl.en-US/Instance/Create an instance/Creation method overview.md).

FTP is a protocol used for transferring files. It is built on a client-server model architecture and supports the following working modes:

-   Active mode: The client sends port information to the FTP server, and the server establishes a connection to the port.
-   Passive mode: FTP server opens a port and sends the port information to the client. The client connects to the port, and the server accepts the connection.

**Note:** Most FTP clients are located in local area networks \(LANs\), have no independent public IP addresses, and are protected by firewalls. This causes problems for FTP servers in active mode to establish a connection to the client. Therefore, we recommend that you use the passive mode for the FTP server unless there are special requirements.

FTP supports the following three authentication modes:

-   Anonymous user mode: Anyone can log on to the FTP server without password verification. This is the least secure mode. We recommend that you use it to save only public files, but not files in a production environment.
-   Local user mode: This authentication mode requires users to have Linux local accounts. This mode is more secure compared with the anonymous user mode.
-   Virtual user mode: Virtual users are dedicated users of the FTP server. Virtual users can access only the FTP service provided by the Linux system and cannot access other resources of the system. This further enhances the security of the FTP server.

This topic describes how to configure vsftpd on a Linux instance in anonymous and local user authentication modes and in passive working mode of the FTP server.

The following resources are used in the procedure described in this topic:

-   Instance type: ecs.c6.large
-   Operating system: CentOS 7.2 64-bit
-   vsftpd: 3.0.2
-   Browser: Google Chrome

The commands and parameters used in this topic may vary based on your resources.

## Procedure

To build an FTP site on a Linux instance, perform the following steps:

-   [Step 1: install vsftpd](#section_821_887_8np)
-   [Step 2: Configure vsftpd](#section_7bm_08s_pts)
-   [Step 3: Set security groups](#section_cnf_mp9_o24)
-   [Step 4: Test the client](#section_zhf_ksd_coj)

## Step 1: install vsftpd

1.  Connect to the target Linux instance.

    For more information, see [Connection methods](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the following command to install vsftpd:

    ```
    yum install -y vsftpd
    ```

    If the following page appears, the installation succeeds.

    ![install_vsftp_successfully](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2529919951/p12598.png)

3.  Run the following command to enable the FTP service to run at boot time:

    ```
    systemctl enable vsftpd.service
    ```

4.  Run the following command to start the FTP service:

    ```
    systemctl start vsftpd.service
    ```

    **Note:** When you run the preceding command, if the system prompts you with the Job for vsftpd.service failed because the control process exited with error code error message, check whether the following problems exist and troubleshoot them. If the problems persist, submit a ticket.

    -   When the network environment does not support IPv6 addresses, run the vim /etc/vsftpd/vsftpd.conf command to change the value of listen\_ipv6 from `YES` to `NO`.
    -   When the MAC address set for the network interface controller in the /etc/sysconfig/network-scripts/ifcfg-xxx configuration file does not match the actual MAC address of the network interface controller, run the ifconfig command to query the MAC address and add `HWADDR=<The actual MAC address of the network interface controller>` to or change HWADDR into <The actual MAC address of the network interface controller\> in the /etc/sysconfig/network-scripts/ifcfg-xxx configuration file.
5.  Run the following command to query the listening port of the FTP service:

    ```
    netstat -antup | grep ftp
    ```

    The following page appears, which indicates that the FTP service is started and is listening to port 21. The anonymous access function is enabled by default. You can log on to the FTP server without entering your username and password, but you do not have the permissions to modify or upload files.

    ![install_vsftpd_3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2529919951/p12600.png)


## Step 2: Configure vsftpd

In this example, vsftpd is configured in anonymous user mode or local user mode. Select one of the modes.

Mode 1: Configure the permissions of anonymous users to upload files.

1.  Modify the /etc/vsftpd/vsftpd.conf configuration file.

    **Note:** If you are using the `apt install vsftpd` command to install vsftpd, the path of the configuration file is /etc/vsftpd.conf.

    1.  Run the vim /etc/vsftpd/vsftpd.conf command to open the configuration file.

    2.  Press I to enter the edit mode.

    3.  Comment out the permissions of anonymous users to upload files and set `anon_upload_enable` to YES.

    4.  Press Esc to exit the edit mode. Enter :wq and press Enter to save and close the file.

    The following figure shows the modified configuration file.

    ![The configuration file of vsftpd](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9418773061/p102865.png)

2.  Run the following command to change the permissions of the /var/ftp/pub directory and grant write permissions to FTP users:

    /var/ftp/pub is the default file directory of the FTP service.

    ```
    chmod o+w /var/ftp/pub/
    ```

3.  Run the following command to reload the configuration file:

    ```
    systemctl restart vsftpd.service
    ```

    ![Permission 2 of anonymous users](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3529919951/p12603.png)


Mode 2: Configure the permissions of local users to access the FTP server.

1.  Run the following command to create a Linux user for the FTP service. In this example, the username is ftptest.

    ```
    adduser ftptest
    ```

2.  Run the following command to modify the password of the ftptest user:

    ```
    passwd ftptest
    ```

3.  Run the following command to create a file directory for the FTP service:

    ```
    mkdir /var/ftp/test
    ```

4.  Run the following command to change the owner of the /var/ftp/test directory to ftptest:

    ```
    chown -R ftptest:ftptest /var/ftp/test
    ```

5.  Modify the vsftpd.conf configuration file.

    1.  Run the vim /etc/vsftpd/vsftpd.conf command to open the configuration file.

    2.  Press I to enter the edit mode.

    3.  Modify or add related configuration parameters based on the following content.

        **Note:** When you modify or add information in the configuration file, pay attention to the format. For example, an extra space may cause the service unable to be restarted.

        ```
        #Use the default values for all parameters except for the following parameters:
        
        #Modify the values of the following parameters:
        #Disallow anonymous users to log on to the FTP server.
        anonymous_enable=NO
        #Allow local users to log on to the FTP server.
        local_enable=YES
        #Listen to IPv4 sockets.
        listen=YES
        #Add # to the beginning of the line to comment out the following parameter and disable listening to IPv6 sockets.
        #listen_ipv6=YES
        
        #Add the following parameters:
        #Specify the directory where local users reside after they log on.
        local_root=/var/ftp/test
        #Specify all users who are restricted to the home directory after they log on.
        chroot_local_user=YES
        #Specify a list of users who are not restricted to the home directory after they log on.
        chroot_list_enable=YES
        #Specify a list file to contain users who are not restricted to the home directory after they log on.
        chroot_list_file=/etc/vsftpd/chroot_list
        #Enable the passive mode.
        pasv_enable=YES
        allow_writeable_chroot=YES
        #The public IP address of a Linux instance is used in this example.
        pasv_address=<The public IP address of the FTP server>
        #Set the minimum port number of the port range that can be used for data transmission in passive mode.
        pasv_min_port=<port number>
        #Set the maximum port number of the port range that can be used for data transmission in passive mode.
        pasv_max_port=<port number>
        ```

        **Note:** We recommend that you use ports in the high number range, such as 50000 to 50010. These ports provide more secure access to the FTP server.

        For more information about the parameters, see [vsftpd configuration file and parameters](#section_t9a_ors_44c).

    4.  Press Esc to exit the edit mode. Enter :wq and press Enter to save and close the file.

6.  Create the chroot\_list file, and write the exception user list to the file.

    1.  Run the vim /etc/vsftpd/chroot\_list command to create the chroot\_list file.

    2.  Press I to enter the edit mode.

    3.  Enter the names of exception users. These users are not limited to the home directory and can access other directories.

    4.  Press Esc to exit the edit mode. Enter :wq and press Enter to save and close the file.

    **Note:** Even if no exception users exist, you must also create the chroot\_list file. The file can be empty.

7.  Run the following command to restart vsftpd.

    ```
    systemctl restart vsftpd.service
    ```


## Step 3: Set security groups

After you build the FTP site, add inbound security group rules to allow traffic on the following FTP ports. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

**Note:** Most clients are located within LANs and have their private IP addresses converted into public IP addresses when the clients access or are accessed by external devices. Therefore, the IP addresses returned by the ipconfig or ifconfig command may not be the actual public IP addresses of the clients. If you cannot log on to the FTP server on the client, verify that the public IP address of your client is correct.

When the FTP server is in passive mode, you must configure the security group rules to allow traffic on port 21 and all the ports from pasv\_min\_port to pasv\_max\_port in the /etc/vsftpd/vsftpd.conf configuration file. The following table lists the configuration details:

|Rule direction|Authorization policy|Protocol type|Port range|Authorization object|
|--------------|--------------------|-------------|----------|--------------------|
|Inbound|Allow|Custom TCP|21|All the CIDR blocks that contain the public IP addresses of clients which need to access the FTP server. Separate multiple CIDR blocks with commas \(,\). To allow all clients to access the FTP server, authorize 0.0.0.0/0. |
|Inbound|Allow|Custom TCP|pasv\_min\_port to pasv\_max\_port|All the CIDR blocks that contain the public IP addresses of clients which need to access the FTP server. Separate multiple CIDR blocks with commas \(,\). To allow all clients to access the FTP server, authorize 0.0.0.0/0. |

## Step 4: Test the client

FTP clients, Windows command-line tools, or browsers can be used to test FTP servers. Google Chrome is used in this example to describe how to access an FTP server.

**Note:** If an error occurs when you use a browser to access the FTP server, clear the browser cache and try again.

1.  Open Google Chrome on the client.

2.  Enter `ftp://<The public IP address of the FTP server>:21` in the address bar.

    The public IP address of the Linux instance is used in this example.

3.  In the dialog box that appears, enter the ftptest username and corresponding password to access the FTP site and perform authorized operations on the FTP file.

    **Note:** This step applies only to local users. Anonymous users can log on to the FTP server without the username and password.


## vsftpd configuration file and parameters

The following section describes the files under the /etc/vsftpd directory:

-   /etc/vsftpd/vsftpd.conf is the core configuration file of vsftpd.
-   /etc/vsftpd/ftpusers is the blacklist file. Users in this file are not allowed to access the FTP server.
-   /etc/vsftpd/user\_list is the whitelist file. Users in this file are allowed to access the FTP server.

The following section describes the parameters in the vsftpd.conf configuration file:

-   The following table describes the working modes.

    |Parameter|Description|
    |---------|-----------|
    |pasv\_enable=YES|Enables the passive mode.|
    |pasv\_enable=NO|Enables the active mode.|
    |The pasv\_enable parameter is empty.|This parameter in the configuration file is empty by default, which indicates that the passive mode is used.|

    **Note:** To enable the active mode, you must configure the security group rules for the ECS instance to allow traffic on ports 20 and 21.

-   The following table describes the parameters used to control logons of users.

    |Parameter|Description|
    |:--------|:----------|
    |anonymous\_enable=YES|Accepts anonymous users.|
    |no\_anon\_password=YES|No password is required when anonymous users log on to the FTP server.|
    |anon\_root= \(none\)|The home directory for anonymous users.|
    |local\_enable=YES|Accepts local users.|
    |local\_root= \(none\)|The home directory for local users.|

-   The following table describes the parameters used to control the permissions of users.

    |Parameter|Description|
    |:--------|:----------|
    |write\_enable=YES|Allows users to upload files \(global control\).|
    |local\_umask=022|Grants local users the permission to upload files.|
    |file\_open\_mode=0666|Uses umask for file upload permissions.|
    |anon\_upload\_enable=NO|Allows anonymous users to upload files.|
    |anon\_mkdir\_write\_enable=NO|Allows anonymous users to create directories.|
    |anon\_other\_write\_enable=NO|Allows anonymous users to modify and delete files.|
    |chown\_username=lightwiter|Specifies the username of anonymously uploaded files.|


Perform security enhancement on the FTP service. For more information, see [FTP anonymous logon and weak password vulnerabilities](https://www.alibabacloud.com/help/zh/doc-detail/37452.htm).

