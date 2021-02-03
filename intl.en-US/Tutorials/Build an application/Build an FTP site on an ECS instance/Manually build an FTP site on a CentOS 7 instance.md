---
keyword: [build an FTP site, build an FTP site on CentOS 7.2, build an FTP site on CentOS 7]
---

# Manually build an FTP site on a CentOS 7 instance

Very secure FTPdaemon \(vsftpd\) is a lightweight, safe, and easy-to-use File Transfer Protocol \(FTP\) server software for Linux. This topic describes how to install and configure vsftpd on a Linux ECS instance.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   An ECS instance is created and assigned a public IP address. For more information about how to create an ECS instance, see [Creation method overview](/intl.en-US/Instance/Create an instance/Creation method overview.md).

FTP is a protocol used for transferring files. It is built on a client-server model architecture and supports the following working modes:

-   Active mode: The client sends port information to the FTP server, and the server establishes a connection to the port.
-   Passive mode: The server opens a port and sends the port information to the client. The client initiates a connection to the port, and the server accepts the connection.

**Note:** Most FTP clients are located in local area networks \(LANs\), have no independent public IP addresses, and are protected by firewalls. This causes problems for FTP servers in active mode to establish connections to the clients. We recommend that you use passive mode for the FTP server unless you have special requirements.

FTP supports the following authentication modes:

-   Anonymous user mode: In this mode, anyone can to log on to the FTP server without a username or password. This is the least secure authentication mode. We recommend that you use it to save only unimportant public files, but not files in a production environment.
-   Local user mode: This authentication mode requires users to have local Linux accounts. This mode is more secure than the anonymous user mode.
-   Virtual user mode: Virtual users are dedicated users of the FTP server. Virtual users can access only the FTP service provided by the Linux system and cannot access other resources of the system. This way, the security of the FTP server is further enhanced.

The following table lists the methods of configuring the FTP server.

|Working mode|Anonymous user|Local user|
|------------|--------------|----------|
|Active mode|Allow anonymous users to upload files to the FTP server in active mode.|Allow local users to access to the FTP server in active mode.|
|Passive mode|N/A.|Allow local users to access to the FTP server in passive mode.|

The following resources are used in the procedure described in this topic:

-   Instance type: ecs.c6.large
-   Operating system: CentOS 7.2 64-bit
-   vsftpd: 3.0.2
-   Browser: Internet Explorer 11

If you use software versions different from the preceding ones, you may need to adjust commands and parameter settings described in the following sections.

## Step 1: install vsftpd

1.  Connect to the Linux instance.

    For more information about how to connect to a Linux instance, see [Connection methods](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the following command to install vsftpd:

    ```
    yum install -y vsftpd
    ```

    If the following page appears, vsftpd is installed.

    ![install_vsftp_successfully](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2529919951/p12598.png)

3.  Run the following command to enable the FTP service to automatically start on system startup:

    ```
    systemctl enable vsftpd.service
    ```

4.  Run the following command to start the FTP service:

    ```
    systemctl start vsftpd.service
    ```

    **Note:** When you run the preceding command, if the system prompts you with the Job for vsftpd.service failed because the control process exited with error code error message, check whether the following problems exist and troubleshoot them. If the problems persist, submit a ticket.

    -   When the network environment does not support IPv6 addresses, run the vim /etc/vsftpd/vsftpd.conf command to change the value of listen\_ipv6 from `YES` to `NO`.
    -   When the MAC address set in the /etc/sysconfig/network-scripts/ifcfg-xxx configuration file does not match the actual MAC address, run the ifconfig command to query the MAC address. Then, add `HWADDR=<The actual MAC address>` to the file or change HWADDR to the actual MAC address in the file.
5.  Run the following command to query the listening port of the FTP service:

    ```
    netstat -antup | grep ftp
    ```

    If the following page appears, the FTP service is started and listens to port 21. By default, anonymous access is enabled in vsftpd. You can log on to the FTP server without a username or password, but you do not have the permissions to modify or upload files.

    ![install_vsftpd_3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2529919951/p12600.png)


## Step 2: Configure vsftpd

In this example, vsftpd is configured in anonymous and local user modes. Select one of the modes.

Mode 1: Configure the permissions of anonymous users to upload files in active mode.

1.  Modify the /etc/vsftpd/vsftpd.conf configuration file.

    **Note:** If you are using the `apt install vsftpd` command to install vsftpd, the path of the configuration file is /etc/vsftpd.conf.

    1.  Run the vim /etc/vsftpd/vsftpd.conf command to open the configuration file.

    2.  Press the I key to enter the edit mode.

    3.  Comment out the permissions of anonymous users to upload files and set `anon_upload_enable` to YES.

    4.  Press the Esc key to exit the edit mode. Enter :wq and press the Enter key to save and close the file.

    The following figure shows the modified configuration file.

    ![The configuration file of vsftpd](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9418773061/p102865.png)

2.  Run the following command to change the permissions on the /var/ftp/pub directory and grant write permissions to FTP users:

    ```
    chmod o+w /var/ftp/pub/
    ```

3.  Run the following command to reload the configuration file:

    ```
    systemctl restart vsftpd.service
    ```

    ![Permission 2 of anonymous users](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3529919951/p12603.png)


Mode 2: Configure the permissions of local users to access the FTP server.

1.  Run the following command to create a Linux user for the FTP service. In this example, the ftptest username is used.

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

    2.  Press the I key to enter the edit mode.

    3.  Enable active or passive mode for the FTP server.

        **Note:** When you modify or add information in the configuration file, pay attention to the format. For example, an extra space may cause the failure to restart the service.

        -   To enable active mode for the FTP server, configure the following parameters:

            ```
            #Use the default values for all parameters except the following parameters:
            
            #Modify the values of the following parameters:
            anonymous_enable=NO      #Disallows anonymous users to log on to the FTP server.
            local_enable=YES         #Allows local users to log on to the FTP server.
            listen=YES               #Listens to IPv4 sockets.
            
            #Add a number sign (#) to the beginning of the row to comment out the following parameter:
            #listen_ipv6=YES          #Disables listening to IPv6 sockets.
            
            #Add the following parameters:
            chroot_local_user=YES    #Limits all users to their home directory after they log on.
            chroot_list_enable=YES   #Uses a list to specify exception users. Exception users are not limited to their home directory after they log on.
            chroot_list_file=/etc/vsftpd/chroot_list  #Specifies a file to contain the list of exception users.
            allow_writeable_chroot=YES  
            local_root=/var/ftp/test #Specifies the directory where local users reside after they log on.
            ```

        -   To enable passive mode for the FTP server, configure the following parameters:

            ```
            #Use the default values for all parameters except the following parameters:
            
            #Modify the values of the following parameters:
            anonymous_enable=NO          #Disallows anonymous users to log on to the FTP server.
            local_enable=YES             #Allows local users to log on to the FTP server.
            listen=YES                   #Listens to IPv4 sockets.
            #Add a number sign (#) to the beginning of the row to comment out the following parameter:
            #listen_ipv6=YES             #Disables listening to IPv6 sockets.
            
            #Add the following parameters:
            local_root=/var/ftp/test     #Specifies the directory where local users reside after they log on.
            chroot_local_user=YES        #Limits all users to their home directory after they log on.
            chroot_list_enable=YES       #Uses a list to specify exception users. Exception users are not limited to their home directory after they log on.
            chroot_list_file=/etc/vsftpd/chroot_list  #Specifies a file to contain the list of exception users.
            allow_writeable_chroot=YES
            pasv_enable=YES                    #Enables passive mode.
            pasv_address=<The public IP address of the FTP server>  #In this topic, the public IP address of the Linux instance is used.
            pasv_min_port=<port number>          #Specifies the minimum port number of the port range that can be used for data transmission in passive mode.
            pasv_max_port=<port number>          #Specifies the maximum port number of the port range that can be used for data transmission in passive mode.
            ```

            **Note:** We recommend that you use ports in a high number range, such as 50000 to 50010. These ports provide more secure access to the FTP server.

        For more information, see [vsftpd configuration file and parameters](#section_t9a_ors_44c).

    4.  Press the Esc key to exit the edit mode. Enter :wq and press the Enter key to save and close the file.

6.  Create the chroot\_list file and write the list of exception users to the file.

    1.  Run the vim /etc/vsftpd/chroot\_list command to create the chroot\_list file.

    2.  Press the I key to enter the edit mode.

    3.  Enter the list of exception users. Exception users are not limited to their home directory and have access to other directories.

    4.  Press the Esc key to exit the edit mode. Enter :wq and press the Enter key to save and close the file.

    **Note:** Even if no exception users exist, you must still create the chroot\_list file. The file can be empty.

7.  Run the following command to restart vsftpd:

    ```
    systemctl restart vsftpd.service
    ```


## Step 3: Set security groups

After you build the FTP site, add inbound security group rules to allow traffic on the following FTP ports. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

**Note:** Most clients are located in LANs and can have their private IP addresses mapped to public IP addresses for communication with external resources. Therefore, the IP addresses returned by the ipconfig or ifconfig command may not be the actual public IP addresses of the clients. If you cannot log on to the FTP server from the client, check the public IP address of the client.

-   If the FTP server is in passive mode, configure the security group rules to allow traffic on port 21. The following table lists the configuration details.

    |Rule direction|Action|Protocol type|Port range|Authorization object|
    |--------------|------|-------------|----------|--------------------|
    |Inbound|Allow|Custom TCP|21/21|The public IP addresses in CIDR block notation of all clients that need to access the FTP server. Separate the IP addresses with commas \(,\). To allow all clients to access the FTP server, specify 0.0.0.0/0 as an authorization object. |

-   If the FTP server is in passive mode, configure the security group rules to allow traffic on port 21 and all ports in the range specified by the pasv\_min\_port and pasv\_max\_port parameters in the /etc/vsftpd/vsftpd.conf configuration file. The following table lists the configuration details.

    |Rule direction|Action|Protocol type|Port range|Authorization object|
    |--------------|------|-------------|----------|--------------------|
    |Inbound|Allow|Custom TCP|21/21|The public IP addresses in CIDR block notation of all clients that need to access the FTP server. Separate the IP addresses with commas \(,\). To allow all clients to access the FTP server, specify 0.0.0.0/0 as an authorization object. |
    |Inbound|Allow|Custom TCP|pasv\_min\_port/pasv\_max\_port|The public IP addresses in CIDR block notation of all clients that need to access the FTP server. Separate the IP addresses with commas \(,\). To allow all clients to access the FTP server, specify 0.0.0.0/0 as an authorization object. |


## Step 4: Test the client

You can use FTP clients, Windows command-line tools, or browsers to test FTP servers. Google Chrome is used in this example to describe how to access an FTP server.

**Note:** If an error occurs when you use a browser to access the FTP server, clear the browser cache and try again.

1.  Open Google Chrome on the client.

2.  In the address bar, enter `ftp://<The public IP address of the FTP server>:FTP port`. The public IP address of the Linux instance is used in this example. Example: `ftp://39.0. **. **:21`

3.  In the dialog box that appears, enter the username and password to access the FTP site and perform operations on the FTP file.

    **Note:** This step applies only to local users. Anonymous users can log on to the FTP server without usernames or passwords.


## vsftpd configuration file and parameters

The following section describes the files under the /etc/vsftpd directory:

-   /etc/vsftpd/vsftpd.conf is the core configuration file of vsftpd.
-   /etc/vsftpd/ftpusers is the blacklist file. Users in this file are not allowed to access the FTP server.
-   /etc/vsftpd/user\_list is the whitelist file. Users in this file are allowed to access the FTP server.

The following section describes the parameters in vsftpd.conf configuration file.

-   The following table describes the parameters for logon control.

    |Parameter setting|Description|
    |:----------------|:----------|
    |anonymous\_enable=YES|Accepts anonymous users.|
    |no\_anon\_password=YES|No password is required when anonymous users log on to the FTP server.|
    |anon\_root= \(none\)|Specifies the home directory of anonymous users.|
    |local\_enable=YES|Accepts local users.|
    |local\_root= \(none\)|Specifies the home directory of local users.|

-   The following table describes the parameters used to control the permissions of users.

    |Parameter setting|Description|
    |:----------------|:----------|
    |write\_enable=YES|Allows users to upload files \(global control\).|
    |local\_umask=022|Grants local users the permission to upload files.|
    |file\_open\_mode=0666|Uses umask for permissions to upload files.|
    |anon\_upload\_enable=NO|Allows anonymous users to upload files.|
    |anon\_mkdir\_write\_enable=NO|Allows anonymous users to create directories.|
    |anon\_other\_write\_enable=NO|Allows anonymous users to modify and delete files.|
    |chown\_username=lightwiter|Specifies the ownership of anonymously uploaded files.|


Perform security hardening on the FTP service. For more information, see [FTP anonymous logon and weak password vulnerabilities](https://www.alibabacloud.com/help/zh/doc-detail/37452.htm).

