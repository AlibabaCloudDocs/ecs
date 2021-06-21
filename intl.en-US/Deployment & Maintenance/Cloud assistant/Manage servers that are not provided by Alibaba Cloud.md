---
keyword: [install the Cloud Assistant client on servers that are not provided by Alibaba Cloud, managed instance, manage a server that is not provided by Alibaba Cloud]
---

# Manage servers that are not provided by Alibaba Cloud

This topic describes how to register a server that is not provided by Alibaba Cloud as an instance managed by Alibaba Cloud. After a server is registered as a managed instance, the server can use various online services provided by Alibaba Cloud such as Cloud Assistant, Operation Orchestration Service \(OOS\), and Alibaba Cloud DevOps.

-   The server runs an operating system of one of the following versions:
    -   Alibaba Cloud Linux
    -   CentOS 6, CentOS 7, CentOS 8, and later
    -   CoreOS
    -   Debian 8, Debian 9, Debian 10, and later
    -   OpenSUSE
    -   RedHat 5, RedHat 6, RedHat 7, and later
    -   SUSE Linux Enterprise Server \(SLES\) 11, SLES 12, SLES 15, and later
    -   Ubuntu 12, Ubuntu 14, Ubuntu 16, Ubuntu 18, and later
    -   Windows Server 2012, Windows Server 2016, Windows Server 2019, and later
-   The server can access the Internet.

## Preparations

Managed instances are supported in the China \(Beijing\), China \(Zhangjiakou\), China \(Hangzhou\), China \(Shanghai\), China \(Shenzhen\), and China \(Hong Kong\) regions. You can select a region based on your server.

For example, you can run the Ping command to test the connection speed and select a region where you are fastest connected to the server.

-   Test the connection between the server and the China \(Beijing\) region:

    ```
    ping -c 4 cn-beijing.axt.aliyuncs.com
    ```

-   Test the connection between the server and the China \(Hangzhou\) region:

    ```
    ping -c 4 cn-hangzhou.axt.aliyuncs.com
    ```

-   Test the connection between the server and the China \(Shanghai\) region:

    ```
    ping -c 4 cn-shanghai.axt.aliyuncs.com
    ```


## Procedure

Perform the following steps to manage instances based on whether your server can directly access the Internet.

-   Perform the following steps if your server can directly access the Internet:
    1.  [Step 1: Create an activation code for managed instances](#section_fhj_e5i_yr4)
    2.  [Step 2: Install the Cloud Assistant client on the server and register the server as an instance \(common method\)](#section_6z6_wsc_i0n)
    3.  [Step 3: View the managed instance in the ECS console](#section_por_q2b_931)
-   Perform the following steps if you need to configure a proxy server for your server to access the Internet:
    1.  [Step 1: Create an activation code for managed instances](#section_fhj_e5i_yr4)
    2.  [Step 2: Install the Cloud Assistant client on the server and register the server as an instance \(proxy method\)](#section_2pm_7s2_v2r)
    3.  [Step 3: View the managed instance in the ECS console](#section_por_q2b_931)

## Step 1: Create an activation code for managed instances

This section describes how to create an activation code for managed instances in the Elastic Compute Service \(ECS\) console and generate an installation script.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **ECS Cloud Assistant**.

3.  In the top navigation bar, select a region.

4.  Click the **Manage Instances** tab.

    ![Create an activation code](../images/p225649.png)

5.  Click **Create Activation Code**.

6.  In the **Create Activation Code** panel, configure the parameters listed in the following table.

    |Parameter|Description|
    |---------|-----------|
    |**Instance Name Prefix**|Specifies the prefix of the names of instances to be managed to facilitate subsequent management.|
    |**Source IP Address**|Specifies the IP addresses or CIDR blocks of managed instances.     -   If you enter the public IP addresses or CIDR blocks of servers, only the servers whose IP addresses are within the configured range can be managed.
    -   If you do not specify this parameter, all servers can be managed. |
    |**Instance Quota**|Specifies the number of managed instances. Valid values: 1 to 1000. Default value: 10. |
    |**Validity Period**|The validity period of the activation code. If the activation code is not used until the validity period ends, you must create a new one. Valid values: 1 to 24. Default value: 4. Unit: hours. |
    |**Description**|The description of the activation code. Specify information such as the purpose of the code in the description to facilitate subsequent management.|

7.  Click **Create**.

    After the activation code is generated, the installation scripts are generated.

    ![Generate scripts](../images/p225668.png)

8.  Select an installation script suitable for the operating system type of your server and click **Download** or **Copy** to save the script to your computer.

    **Note:**

    -   After the activation code is generated, the installation scripts are displayed once. You must save the appropriate installation scripts to your computer.
    -   If your servers runs different operating systems, you must download the corresponding installation scripts in sequence.

## Step 2: Install the Cloud Assistant client on the server and register the server as an instance \(common method\)

After you obtain the installation script, you must install the Cloud Assistant client on your server and register the server as an instance. If your server can access the Internet, perform the following steps. If your server must use a proxy server to access the Internet, see [Step 2: Install the Cloud Assistant client on the server and register the server as an instance \(proxy method\)](#section_2pm_7s2_v2r).

**Install the Cloud Assistant client on a Linux server and register the server as an instance**

1.  Log on to the server by using Secure Shell \(SSH\).

2.  Create an installation script in the server.

    1.  Run the following command to create a script by using the VIM editor:

        ```
        vim installAssistant.sh
        ```

    2.  Press the `I` key to enter the edit mode.

    3.  Paste the content of the script created in the ECS console. For more information, see [Step 1: Create an activation code for managed instances](#section_fhj_e5i_yr4).

    4.  Press the `Esc` key to exit the edit mode.

    5.  Enter `:wq` and press the `Enter` key to save and exit the file.

3.  Run the following command to set execution permissions on the installation script:

    ```
    sudo chmod 755 installAssistant.sh
    ```

4.  Run the following command to install the Cloud Assistant client on the server:

    ```
    sudo ./installAssistant.sh
    ```

    After the operation is complete, the client is installed if information shown in the following figure is returned.

    ![Return results in Linux](../images/p227024.png)


**Install the Cloud Assistant client on a Windows server and register the server as an instance**

1.  Log on to the server by using **Remote Desktop Connection**.

2.  Upload the installation script to the server.

    For information about how to obtain the installation script, see the [Step 1: Create an activation code for instances to be managed](#section_fhj_e5i_yr4) section in this topic.

    **Note:** **Remote Desktop Connection** allows you to directly copy and paste the script file to the server. If your network environment has limits that prevent direct copying, you can upload scripts by using FTP and other software.

3.  Right-click the installation script and select **Run with PowerShell** to install the Cloud Assistant client.

    ![Windows installation script](../images/p227027.png)


## Step 2: Install the Cloud Assistant client on the server and register the server as an instance \(proxy method\)

After you obtain the installation script, you must install the Cloud Assistant client on your server and register the server as an instance. If your server can access the Internet, perform the following steps. If your server must use a proxy server to access the Internet, see [Step 2: Install the Cloud Assistant client on the server and register the server as an instance \(common method\)](#section_6z6_wsc_i0n).

**Install a Cloud Assistant client on a Linux server and register the server as an instance**

This section describes how to configure a proxy server. Cent OS 7.8 is used in this example. If your server runs an operating system such as Debian, you must modify the commands shown in the following figure based on the installation script generated in the ECS console.

![centos](../images/p268369.png)

-   ①: Download the Cloud Assistant client installation package
-   ②: Install the Cloud Assistant client
-   ③: Register the server as an instance managed by Cloud Assistant

If your server must use a proxy server to access the Internet, you must configure the corresponding proxy server information based on these commands.

1.  Log on to the server by using SSH.

2.  Run the following command to download the Cloud Assistant client by using the proxy server:

    ```
    sudo https_proxy=<http://your_proxy_address> && wget https://aliyun-client-assist.oss-accelerate.aliyuncs.com/linux/aliyun_assist_latest.rpm
    ```

    **Note:** You must replace `<http://your_proxy_address>` with your proxy server address.

3.  Run the following command to install the Cloud Assistant client:

    ```
    sudo rpm -ivh aliyun_assist_latest.rpm --force
    ```

4.  Configure a proxy server for Cloud Assistant.

    1.  Modify the Cloud Assistant configuration file.

        Modify the Cloud Assistant configuration file and configure the ALIYUN\_ASSIST\_PROXY environment variable. Perform the following steps:

        1.  Create the vim /etc/sysconfig/aliyun file by using the VIM editor.

            ```
            sudo vim /etc/sysconfig/aliyun
            ```

        2.  Enter and save the following content and then exit.

            ```
            ALIYUN_ASSIST_PROXY=<http://your_proxy_address>
            ```

            **Note:** You must replace `<http://your_proxy_address>` with your proxy server address.

        3.  Modify the aliyun.service file by using the VIM editor.

            ```
            sudo vim /etc/systemd/system/aliyun.service
            ```

        4.  Modify and save the EnvironmentFile value and then exit.

            ```
            EnvironmentFile=/etc/sysconfig/aliyun
            ```

    2.  Run the following command to reload the systemd configuration:

        ```
        sudo systemctl daemon-reload
        ```

    3.  Run the following command to restart the Cloud Assistant client:

        ```
         sudo systemctl restart aliyun.service
        ```

        After the Cloud Assistant client is started, if `Detected environment variable ALIYUN_ASSIST_PROXY for proxy setting` related information exists in the logs of Cloud Assistant, a proxy server is created for Cloud Assistant. The default log path is /usr/local/share/aliyun-assist/\{version\}/log/aliyun\_assist\_main.log.

5.  Run the following commands to register the server as an instance managed by Cloud Assistant by using the proxy server.

    1.  Run the following command to configure the proxy server:

        ```
        sudo export ALIYUN_ASSIST_PROXY=<http://your_proxy_address>
        ```

        **Note:** You must replace `<http://your_proxy_address>` with your proxy server address.

    2.  Run the following commands to register the server as an instance managed by Cloud Assistant:

        ```
        sudo aliyun-service --register --RegionId "cn-hangzhou" \
           --ActivationCode "a-hz0f5KlGmF/TsM5uBuq7Eqor+****" \
           --ActivationId "045CE381-0404-4F42-A44B-CC232B3E****"
        ```

        **Note:** The preceding code is for reference only. You must copy and paste the code generated in the ECS console. For more information, see [Step 1: Create an activation code for managed instances](#section_fhj_e5i_yr4).


**Install the Cloud Assistant client on a Windows server and register the server as an instance**

This section describes how to configure a proxy server. Windows Server 2016 Datacenter is used in the example. The installation script of the Cloud Assistant client for Windows is shown in the following figure. When you configure a proxy server, you must use the `RegionId`, `ActivationCode`, `ActivationId` parameter values.

![Windows script](../images/p268965.png)

1.  Log on to the server by using **Remote Desktop Connection**.

2.  Configure the proxy server for the browser.

    1.  Choose **Start** \> **Control Panel**.

    2.  Click **Network and Internet**.

    3.  Click **Network and Sharing Center**.

    4.  In the lower-left corner, click **Internet Options**.

        ![Proxy](../images/p268412.png)

    5.  Click the **Connections** tab and click **LAN settings**.

    6.  In the **Proxy server** section, configure the proxy server address and port and click **OK**.

3.  Download the installation package of the Cloud Assistant client.

    1.  Click Start and choose **Windows PowerShell** \> **Windows PowerShell**.

    2.  Right-click **Windows PowerShell** and select **Run as administrator**.

    3.  In the **Windows PowerShell** dialog box, run the following command to download the installation package of the Cloud Assistant client:

        ```
        Invoke-WebRequest -Uri 'https://aliyun-client-assist.oss-accelerate.aliyuncs.com/windows/aliyun_agent_latest_setup.exe' -OutFile 'C:\\aliyun_agent_latest_setup.exe'
        ```

4.  After you download the installation package, install the Cloud Assistant client.

    1.  Open the C:\\ drive.

    2.  Double -click aliyun\_agent\_latest\_setup.exe and follow the installation wizard to install the Cloud Assistant client.

5.  Configure a proxy server for Cloud Assistant.

    1.  Choose **Start** \> **Control Panel**.

    2.  Click **System and Security**.

    3.  Click **System**.

    4.  In the left-side navigation pane, click **Advanced system settings**.

        ![Configure proxy](../images/p267862.png)

    5.  Click the **Advanced** tab and click **Environment Variables**.

    6.  In the **System variables** section, click **New**.

    7.  Configure **Variable name** and **Variable value** and click **OK**.

        -   **Variable name**: Set this parameter to ALIYUN\_ASSIST\_PROXY.
        -   **Variable value**: Set this parameter to your proxy server address.
    8.  Run the following commands in **Windows PowerShell** to restart the Cloud Assistant client.

        Run the following command to disable the Cloud Assistant client:

        ```
        net stop AliyunService
        ```

        Run the following command to restart the Cloud Assistant client:

        ```
        net start AliyunService
        ```

6.  Use the proxy server to register an instance managed by Cloud Assistant in **Windows PowerShell**.

    Run the following command to go to the directory where the Cloud Assistant client is installed:

    ```
    cd C:\ProgramData\aliyun\assist\{version}
    ```

    **Note:** `{version}` specifies the version of the Cloud Assistant client. You must set this value to a specific version number.

    Run the following commands to register the server as an instance managed by Cloud Assistant:

    ```
     .\aliyun_assist_service.exe  --register  --RegionId="cn-hangzhou" --ActivationCode="a-hz0f6dB8Fg6hhtK0A5n9xqqdH****" --ActivationId="0A2E5ECE-5C71-4FA3-807B-05962C25****"
    ```

    **Note:** The preceding code is used for reference only. Change the values of `RegionId`, `ActivationCode`, and `ActivationCode` to those in the script that is automatically generated in the console. For information about how to obtain the script, see the [Step 1: Create an activation code for managed instances](#section_fhj_e5i_yr4) section in this topic.


## Step 3: View the managed instance in the ECS console

After you install the Cloud Assistant client, you must go back to the ECS console to check whether the managed instance is connected.

1.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **ECS Cloud Assistant**.

2.  In the top navigation bar, select a region.

3.  Click the **Manage Instances** tab to view the list of managed instances.

    ![Managed instance list](../images/p227029.png)

    As shown in the preceding figure, if **Connection Status** corresponding to the managed instance is **Running**, the managed instance is registered.


You can then use Cloud Assistant to manage the server without logging on to the server. For how to use Cloud Assistant, see [Immediate execution](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Immediate execution.md) and [Send files to ECS instances](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Send files to ECS instances.md).

## Optional. Unregister managed instances and uninstall the Cloud Assistant client

If you do not want to use Cloud Assistant any longer, you can unregister the managed instances and disable and uninstall the Cloud Assistant client.

If your server runs a Linux operating system, perform the following steps:

1.  Log on to the server by using SSH.
2.  Run the following command to unregister the managed instances:

    ```
    sudo aliyun-service --deregister
    ```

3.  Disable and uninstall the Cloud Assistant daemon process.

    Run the following command to disable the Cloud Assistant daemon process:

    ```
    sudo /usr/local/share/assist-daemon/assist_daemon --stop
    ```

    **Note:** /usr/local/share/assist-daemon/assist\_daemon is the default path of the Cloud Assistant daemon process.

    Run the following command to uninstall the Cloud Assistant daemon process:

    ```
    sudo /usr/local/share/assist-daemon/assist_daemon --delete
    ```

4.  Run the following command to disable the Cloud Assistant client:

    **Note:** Linux has different kernel versions and uses different initialization process services. Linux that uses a later kernel version such as Ubuntu 18.04 generally uses the systemd initialization process service. The systemd initialization process is used in this example. For more information about how to use other initialization process services, see [Uninstall the Cloud Assistant daemon process from a Linux instance](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Start or stop the Cloud Assistant client.md).

    ```
    sudo systemctl stop aliyun.service
    ```

5.  Run the following command to uninstall the Cloud Assistant client.
    -   RPM package:

        ```
        sudo rpm -qa | grep aliyun_assist | xargs sudo rpm -e
        ```

    -   DEB package:

        ```
        sudo dpkg -r aliyun_assist_latest.deb
        ```

6.  Delete the Cloud Assistant daemon process and the Cloud Assistant client.

    Run the following command to delete the directory where the Cloud Assistant daemon process is stored:

    ```
    sudo rm -rf /usr/local/share/assist-daemon
    ```

    Run the following command to delete the directory where the Cloud Assistant client is stored:

    ```
    sudo rm -rf /usr/local/share/aliyun-assist
    ```


If your server runs a Windows operating system, perform the following steps:

**Note:** Windows Service 2019 is used in this example. The paths for Windows PowerShell and services in other Windows versions may be different.

1.  Log on to the server with the administrator account.
2.  Start Windows PowerShell as an administrator.

    ![Start Powershell](../images/p227208.png)

    1.  Click Start.
    2.  Choose **Windows PowerShell** \> **Windows PowerShell**.
    3.  Right-click **Windows PowerShell** and select **Run as administrator**.
3.  Run the following command in **Windows PowerShell** to unregister the managed instances:

    ```
    aliyun-service --deregister
    ```

4.  Open the service management window.

    ![Service](../images/p227260.png)

    1.  Click Start.
    2.  Choose **Administrative Tools** \> **Service**.
5.  Find **Aliyun Assist Service** and click **Stop the service**.

    ![Stop Service](../images/p227406.png)


## References

-   [CreateActivation]()
-   [DisableActivation]()
-   [DeregisterManagedInstance]()
-   [DescribeActivations]()
-   [DescribeManagedInstances]()
-   [DeleteActivation]()

