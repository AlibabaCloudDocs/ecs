# Set the MTU size of an NIC

A maximum transmission unit \(MTU\) is the largest size of a packet that can be transmitted without the need to fragment the packet. This topic describes how to set the MTU size of a network interface controller \(NIC\) on an ECS instance by using the ecs-utils-jumboframe script.

To limit the maximum sizes of transmitted packets and avoid excess latency resulted when large packets are fragmented, we recommend that you keep the local and network MTU sizes consistent.

**Note:** The ecs-utils-jumboframe script does not contain commands that can be used to restart NICs or network services. Different types of network services and NIC drivers may be used in different systems, and transient connections may occur. If your business does not allow transient connections, exercise caution when you perform this operation.

## Limits

-   You can run the ecs-utils-jumboframe script only on VPC-type ECS instances. The ecs-utils-jumboframe script uses instance metadata services to check whether instance types support the Jumbo Frame feature. Before you run the script on an ECS instance, access <IP address of the ECS instance\>: <Port number\> in your browser to check whether the port used to exchange data between networks and instance metadata services is enabled on the ECS instance. Example: 100.100.100.200:80. If the port is not enabled, enable it.
-   Only the seventh-generation hfg7, hfc7, and hfr7 instance families support the Jumbo Frame feature. A maximum MTU size of 8,500 is allowed for the instance types within these instance families. The ecs-utils-jumboframe script determines the maximum MTU size based on instance types. You can also use this script to set a maximum MTU size of 1,500 for NICs on ECS instances of other instance types.
-   The Jumbo Frame feature is applicable only to direct TCP communication between seventh-generation VPC-type ECS instances that have high clock speeds, and does not support the communication through intermediate nodes such as Server Load Balancer \(SLB\) instances.

## Set the MTU size of an NIC on a Linux instance

Use a Linux instance that uses one of the following images:

-   CentOS 6.x, CentOS 7.x, and CentOS 8.x
-   Debian 9.x and Debian 10.x
-   SUSE Linux Enterprise Server 15
-   Ubuntu 16.x, Ubuntu 18.x, and Ubuntu 20.x

1.  [Connect to the instance](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Download the ecs-utils-jumboframe-linux.sh script.

    ```
    wget https://ecs-image-tools.oss-cn-hangzhou.aliyuncs.com/jumboframe/ecs-utils-jumboframe-linux.sh
    ```

3.  Grant the execute permissions on the script.

    ```
    chmod +x ./ecs-utils-jumboframe-linux.sh
    ```

    You can run `./ecs-utils-jumboframe-linux.sh -h` to view the help.

    ![help](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7199545161/p225163.png)

4.  Query the list of NICs on the instance and the MTU sizes of the NICs.

    ```
    ip addr show
    ```

    ![origin-mtu](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7199545161/p225866.png)

5.  Set the MTU size of a NIC.

    -   Set a temporary MTU size for the NIC. To test the Jumbo Frame feature, you can use the following command to set a temporary MTU size for the NIC. The MTU is restored to the default size when the instance is restarted.

        ```
        ./ecs-utils-jumboframe-linux.sh <NIC name> <New MTU size>
        ```

        For example, you can run the following command to set a temporary MTU size of 8500 for the eth0 NIC:

        ```
        ./ecs-utils-jumboframe-linux.sh eth0 8500
        ```

    -   Set a permanent MTU size \(a MTU size that remains unchanged when the instance is restarted\) for the NIC. To enable the Jumbo Frame feature, you can use the following command to set a permanent MTU size and specify the -p mode. After the MTU size is set, it remains unchanged when the instance is restarted.

        ```
        ./ecs-utils-jumboframe-linux.sh -p <NIC name> <New MTU size>
        ```

        For example, you can run the following command to set a permanent MTU size of 8500 for the eth0 NIC:

        ```
        ./ecs-utils-jumboframe-linux.sh -p eth0 8500
        ```

    After the new MTU size is set for the eth0 NIC, you can run the `ip addr show` command to query information of the NIC. The MTU size of the NIC is 8500 in the command output.

    ![view-mtu-setting](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7199545161/p225168.png)


## Set the MTU size of an NIC on a Windows instance

Make sure that the Windows instance meets the following requirements:

-   The instance uses a Windows Server 2012 or later image.
-   The instance has PowerShell installed.

1.  [Connect to the instance](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Download the ecs-utils-jumboframe-windows.ps1 script.

    Visit [Download link](https://ecs-image-tools.oss-cn-hangzhou.aliyuncs.com/jumboframe/ecs-utils-jumboframe-windows.ps1) in your browser.

3.  Start PowerShell.

4.  Switch to the directory where the script is located.

    In this example, the script is placed on the desktop and located in the following directory:

    ```
    cd C:\Users\Administrator\Desktop
    ```

    You can run `Get-Help .\ecs-utils-jumboframe-windows.ps1` to view the help.

    ![get-help](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7199545161/p225498.png)

5.  Query the list of NICs.

    ```
    Get-NetAdapter
    ```

    ![get-netadapter](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7199545161/p225500.png)

6.  Set the MTU size of a NIC.

    **Note:** You can set only permanent MTU sizes on Windows instances. After a permanent MTU size is set for a NIC on a Windows instance, the MTU size remains unchanged when the instance is restarted.

    Run the following command:

    ```
    .\ecs-utils-jumboframe-windows.ps1 -NetworkAdapter <"NIC name"> -NewMTUValue <New MTU size>
    ```

    For example, you can run the following command to set a permanent MTU size of 8500 for an NIC named Ethernet:

    ```
    .\ecs-utils-jumboframe-windows.ps1 -NetworkAdapter "Ethernet" -NewMTUValue 8500
    ```

    After the new MTU size is set for the NIC, you can run the `Get-NetAdapterAdvancedProperty -Name "Ethernet" -RegistryKeyword "MTU"` command to query information of the NIC. The MTU size of the NIC is 8500 in the command output.

    ![view-mtu](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7199545161/p225503.png)


