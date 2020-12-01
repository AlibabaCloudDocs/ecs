# Connect to a Linux instance by using an SSH key pair

SSH key pairs are a secure and convenient method to authenticate logons. This topic describes how to use an SSH key pair to connect to a Linux instance from a Windows device or a device that supports SSH commands, such as a Linux client or MobaXterm for Windows.

-   An SSH key pair is created and the .pem private key file is downloaded. For more information, see [Create an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Create an SSH key pair.md).
-   An instance is in the Running state.
-   An SSH key pair is bound to the instance.
-   A public IP address or an elastic IP address \(EIP\) is associated with the instance.
-   A security group rule is added to the security group to which the instance belongs to allow traffic on the corresponding port, such as the default port 22 for SSH. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

    |Network type|NIC type|Rule direction|Action|Protocol type|Port|Priority|Authorization type|Authorization object|
    |------------|--------|--------------|------|-------------|----|--------|------------------|--------------------|
    |VPC|N/A|Inbound|Allow|SSH\(22\)|22/22|1|IPv4 CIDR block|0.0.0.0/0|
    |Classic network|Public|


## Use an SSH key pair to connect to a Linux instance from a Windows device

The following section describes how to convert the format of a private key file from .pem to .ppk and how to use an SSH key pair to connect to a Linux instance. PuTTYgen is used in this example.

1.  Download and install PuTTYgen and PuTTY.

    Download PuTTY and PuTTYgen from the following URLs:

    -   [PuTTYgen](https://the.earth.li/~sgtatham/putty/latest/w64/puttygen.exe)
    -   [PuTTY](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe)
2.  Convert the format of a private key file from .pem to .ppk.

    1.  Start PuTTYgen.

        In this example, PuTTYgen 0.71 is used.

    2.  Set **Type of key to generate** to **RSA** and click **Load**.

        ![windows_puttygen_1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6847597851/p51179.png)

    3.  Select **All Files**.

        ![windows_puttygen_2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6847597851/p5188.png)

    4.  Select the .pem private key file that you want to convert.

    5.  In the dialog box that appears, click **OK**.

    6.  Click **Save private key**.

    7.  In the dialog box that appears, click **Yes**.

    8.  Specify the name of the .ppk private key file and click **Save**.

3.  Start PuTTY.

4.  Configure the private key file used for authentication.

    1.  Choose **Connection** \> **SSH** \> **Auth**.

    2.  Click **Browse…**.

    3.  Select the resulting .ppk private key file.

    ![windows_putty_3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7847597851/p5191.png)

5.  Configure the required parameters to connect to the Linux instance.

    1.  Click **Session**.

    2.  In the **Host Name \(or IP address\)** field, enter the logon account and public IP address of the instance.

        The format is **account@IP address**. Example: root@10.10.xx.xxx.

    3.  In the **Port** field, enter the port number **22**.

    4.  Set **Connection type** to **SSH**.

    ![windows_putty_4](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7847597851/p5192.png)

6.  Click **Open**.

    If the following message appears, you have logged on to the instance by using the SSH key pair.

    ![windows_putty_5](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7847597851/p51203.png)


## Use an SSH key pair from a device that supports SSH commands \(configure the private key file by using commands\)

The following section describes how to use commands to configure the required parameters from a device that supports SSH commands, such as a Linux client or MobaXterm for Windows. The section also describes how to use SSH commands to log on to a Linux instance.

1.  Find the path where the .pem private key file is located. Example: ~/.ssh/ecs.pem.

    The path and file name are only for reference. You can modify the information in your subsequent commands based on your actual needs.

2.  Run the following command to modify the property of the private key file:

    ```
    chmod 400 [Path of the .pem private key file on your local PC]
    ```

    Example:

    ```
    chmod 400 ~/.ssh/ecs.pem
    ```

3.  Run the following command to connect to the instance:

    ```
    ssh -i [Path of the .pem private key file on your local PC] root@[Public IP address]
    ```

    Example:

    ```
    ssh -i ~/.ssh/ecs.pem root@10.10.xx.xxx
    ```


## Use an SSH key pair from a device that supports SSH commands \(configure the private key file by using the config file\)

The following section describes how to use commands to configure the required parameters from a device that supports SSH commands, such as a Linux client or MobaXterm for Windows. The section also describes how to use SSH commands to log on to a Linux instance.

1.  Find the path where the .pem private key file is located. Example: ~/.ssh/ecs.pem.

    The path and file name are only for reference. You can modify the information in your subsequent commands based on your actual needs.

2.  Run the following command to modify the property of the private key file:

    ```
    chmod 400 [Path of the .pem private key file on your local PC]
    ```

    Example:

    ```
    chmod 400 ~/.ssh/ecs.pem
    ```

3.  Run the following commands to go to the .ssh directory in the home directory and create a config file:

    ```
    cd ~/.ssh
    vim config
    ```

4.  In the `config` file, press the i key to enter the edit mode and add the following configuration items:

    ```
    # Enter the name of the ECS instance to connect to the instance by using an SSH key pair.
    Host ecs
    # Enter the public IP address of the ECS instance.
    HostName 121.196. **. **
    # Enter the port number. The default port number is 22.
    Port 22
    # Enter the logon account.
    User root
    # Enter the address of the .pem private key file on your local PC.
    IdentityFile ~/.ssh/ecs.pem
    ```

    If you have multiple ECS instances, you can use the `config` file to configure password-free logons in a centralized manner. The following example demonstrates how to configure password-free logons for two ECS instances:

    ```
    # Enter the name of one ECS instance to connect to the instance by using an SSH key pair.
    Host ecs1
    # Enter the public IP address of the ECS instance.
    HostName 121.196. **. **
    # Enter the port number. The default port number is 22.
    Port 22
    # Enter the logon account.
    User root
    # Enter the address of the .pem private key file on your local PC.
    IdentityFile ~/.ssh/ecs.pem
    
    # Enter the name of the other ECS instance to connect to the instance by using an SSH key pair.
    Host ecs2
    # Enter the public IP address of the ECS instance.
    HostName 121.196. **. **
    # Enter the port number. The default port number is 22.
    Port 22
    # Enter the logon account.
    User root
    # Enter the address of the .pem private key file on your local PC.
    IdentityFile ~/.ssh/ecs.pem
    ```

    After the configuration items are added, press the Ecs key and enter `:wq` to save the config file.

5.  Run the following command to restart the SSH service:

    ```
    service sshd restart
    ```

6.  Run the following command to connect to the instance:

    ```
    ssh [Name of the instance]
    ```

    Example:

    ```
    ssh ecs
    ```


