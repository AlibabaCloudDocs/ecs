---
keyword: [multiple private IP addresses, ENI, bind an ENI, ECS, Alibaba Cloud]
---

# Assign secondary private IP addresses

You can assign one or more secondary private IP addresses to a primary or secondary elastic network interface \(ENI\). This allows you to optimize the usage of VPC-type instances and divert traffic during a failover.

-   The instance type of your instance supports multiple secondary private IP addresses. The number of private IP addresses that can be assigned to a single ENI depends on the instance type of the instance to which the ENI is bound. For more information, see [Instance families](/intl.en-US/Instance/Instance families.md).
-   When you assign a secondary private IP address to a primary ENI, the instance to which the primary ENI is bound is in the **Running** or **Stopped** state.

Secondary private IP addresses are suitable for the following scenarios:

-   Multiple application usage

    If your ECS instance hosts multiple applications, you can assign multiple secondary private IP addresses to the corresponding ENIs. This way, each application uses a separate IP address for services, which optimizes the usage of the ECS instance.

-   Failover

    If an instance fails, you can unbind ENIs from the instance and bind the ENIs to another instance to divert traffic to that instance. This can ensure service continuity.


When you assign secondary private IP addresses, take note of the following limits:

-   Each security group of the VPC type can contain a maximum of 2,000 private IP addresses. This quota is shared among all primary and secondary ENIs in the security group.
-   You can assign a maximum of 20 private IP addresses to an ENI. The actual number depends on the status of the ENI and the instance type of the instance to which the ENI is bound.
    -   If the ENI is in the **Available** state, you can assign a maximum of 10 private IP addresses to the ENI.
    -   If the ENI is in the **Bound** state, the number of private IP addresses that can be assigned to the ENI is subject to the instance type of the instance.

## Description

This section applies to both primary and secondary ENIs.

1.  In the ECS console, assign secondary private IP addresses to an ENI. For more information, see the [Assign secondary private IP addresses](#section_bam_ihj_gsy) section in this topic.

2.  In the instance to which the ENI is bound, configure the assigned secondary private IP addresses.

    **Note:** If the ENI is a secondary ENI and is not bound to an instance, bind the ENI to an instance and configure the assigned secondary private IP addresses in the instance. For more information, see [Bind an ENI](/intl.en-US/Network/Elastic Network Interfaces/Bind an ENI.md).

    -   For Windows instances, see [Configure secondary private IP addresses in a Windows instance](#section_y4b_krk_ggb).
    -   For Linux instances, see [Configure secondary private IP addresses in a Linux instance](#section_b2x_hlb_3gb).

## Assign secondary private IP addresses

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Network & Security** \> **ENIs**.

3.  In the top navigation bar, select a region.

4.  On the Network Interfaces page, find the ENI to which you want to assign secondary private IP addresses, and then click **Manage Secondary Private IP Address** in the **Actions** column.

5.  In the Manage Secondary Private IP Address dialog box, click **Assign New IP**.

    -   Auto-assign: Keep the default setting. The system randomly assigns IPv4 addresses from the range of **IPv4 Private CIDR Block**.
    -   Manual-assign: Manually enter secondary private IP addresses within the range of **IPv4 Private CIDR Block**.
    **Note:** After an IP address is assigned, you can click **Assign New IP** again to assign another private IP address.

    ![Enter secondary private IP addresses](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6059039951/p47047.png)

6.  Click **OK**.


**Note:** After you complete automatic assignment of secondary private IP addresses, click **Manage Secondary Private IP Address** in the **Actions** column corresponding to the ENI to view the assigned secondary private IP addresses.

## Configure secondary private IP addresses in a Windows instance

1.  Remotely connect to an ECS instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Query the subnet mask and default gateway of the instance.

    1.  Open **Command Prompt** or **Windows PowerShell**.

    2.  Enter the `ipconfig` command to query the subnet mask and default gateway of the instance.

        ```
        PS C:\Users\Administrator> ipconfig
        Windows IP Configuration
        Ethernet adapter Ethernet:
           Connection-specific DNS Suffix . . . . . . . :
           Link-local IPv6 Address. . . . . . . . : fe80::6c64:1601:****:****
           IPv4 Address . . . . . . . . . . . . : 172. **. **.133
           Subnet Mask ..............: 255.255. **. **
           Default Gateway. . . . . . . . . . . . . : 172. **. **.253
        ```

3.  Open Network and Sharing Center.

4.  Click **Change adapter settings**.

5.  Double-click the current network connection name and click **Properties**.

6.  Double-click **Internet Protocol Version 4 \(TCP/IPv4\)**.

7.  Select **Use the following IP address** and click **Advanced**.

8.  In the **Advanced TCP/IP Settings** dialog box, set IP addresses.

    1.  In the **IP addresses** section, click **Add...** and enter one of the assigned IP addresses in the **IP address** field and the obtained subnet mask in the **Subnet mask** field.

        You can add multiple IP addresses to the same adapter.

        ![Add IP addresses](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9087467951/p47049.png)

    2.  In the **Default gateways** section, click **Add...** and enter the obtained subnet mask in the **Subnet mask** field.

9.  Click **OK**.


**Note:**

If a secondary private IP address is configured for a Windows instance and the instance cannot connect to the Internet, see [After I configure a secondary private IP address for a Windows instance, the instance cannot connect to the Internet. Why?](/intl.en-US/Network/Network FAQ.md).

## Configure secondary private IP addresses in a Linux instance

In the following example, the eth0 primary ENI is used. If you are using a secondary ENI, modify the ENI ID.

1.  Remotely connect to an ECS instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the `ipconfig` command to query the subnet mask and default gateway of the instance.

    ```
    [root@ecs ~]# ifconfig
    eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet 172.16. **.**  netmask 255.255. **.**  broadcast 172.16. **.**
            inet6 fe80::216:3eff:****:****  prefixlen 64  scopeid 0x20<link>
            ether 00:16:3e:0e:**:**  txqueuelen 1000  (Ethernet)
            RX packets 27146  bytes 39146111 (37.3 MiB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 6038  bytes 509398 (497.4 KiB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    ```

    **Note:** If some Linux distributions do not support the `ifconfig` command, you can run the `ip addr show` command.

3.  Configure secondary private IP addresses based on the operating system of your instance.

    -   RHEL series: CentOS 6, CentOS 7, Red Hat 6, Red Hat 7, or Alibaba Cloud Linux 2
        1.  Open the network configuration file.
            -   If you configure a single IP address, run the `vi /etc/sysconfig/network-scripts/ifcfg-eth0:0` command to add the following configuration items:

                ```
                DEVICE=eth0:0
                TYPE=Ethernet
                BOOTPROTO=static
                ONBOOT=yes
                IPADDR=<IPv4 address 1>
                NETMASK=<IPv4 mask>
                GATEWAY=<IPv4 gateway>
                ```

            -   If you configure multiple IP addresses, run the `vi /etc/sysconfig/network-scripts/ifcfg-eth0:1` command to add the following configuration items:

                ```
                DEVICE=eth0:1
                TYPE=Ethernet
                BOOTPROTO=static
                ONBOOT=yes
                IPADDR=<IPv4 address 2>
                NETMASK=<IPv4 mask>
                GATEWAY=<IPv4 gateway>
                ```

        2.  Run the `service network restart` or `systemctl restart network` command to restart the network service.
    -   Debian series: Ubuntu 14, Ubuntu 16, Debian 8, or Debian 9
        1.  Run the `vi /etc/network/interfaces` command to open the network configuration file and add the following configuration items:

            ```
            auto eth0:0
            iface eth0:0 inet static
            address <IPv4 address 1>
            netmask <IPv4 mask>
            gateway <IPv4 gateway>
            
            auto eth0:1
            iface eth0:1 inet static
            address <IPv4 address 2>
            netmask <IPv4 mask>
            gateway <IPv4 gateway>
            ```

        2.  Run the `service networking restart` or `systemctl restart networking` command to restart the network service.
    -   SLES series: SUSE 11, SUSE 12, or openSUSE 42
        1.  Run the `vi /etc/sysconfig/network/ifcfg-eth0` command to open the network configuration file and add the following configuration items:

            ```
            IPADDR_0=<IPv4 address 1>
            NETMASK_0=<Subnet prefix length>
            LABEL_0='0'
            
            IPADDR_1 = <IPv4 address 2>
            NETMASK_1 = <Subnet prefix length>
            LABEL_1='1'
            ```

        2.  Run the `service network restart` or `systemctl restart network` command to restart the network service.

**Related topics**  


[AssignPrivateIpAddresses](/intl.en-US/API Reference/Elastic network interfaces/AssignPrivateIpAddresses.md)

