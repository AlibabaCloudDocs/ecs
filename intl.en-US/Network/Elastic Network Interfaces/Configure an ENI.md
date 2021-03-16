---
keyword: [multi-NIC driver, identify multiple NICs, automatically visible ENIs, ENI]
---

# Configure an ENI

You may need to manually configure elastic network interfaces \(ENIs\) for some images used by your instances so that the bound ENIs can be identified by the operating systems. This topic describes how to configure ENIs.

ENIs are bound to ECS instances. For more information about how to bind an ENI to an ECS instance, see [Bind an ENI](/intl.en-US/Network/Elastic Network Interfaces/Bind an ENI.md).

If your instances are running images of the following versions, you do not need to configure ENIs:

-   CentOS 8.0 64-bit, CentOS 8.1 64-bit, and CentOS 8.2 64-bit
-   CentOS 7.3 64-bit, CentOS 7.4 64-bit, and CentOS 7.5 64-bit
-   CentOS 6.8 64-bit and CentOS 6.9 64-bit
-   Debian 10.5 64-bit and Debian 10.6 64-bit
-   Windows Server 2008 R2 and later

If your instances are running images whose versions are not included in the preceding list, you must manually configure ENIs for the images.

## Procedure

1.  View and record information of ENIs. For more information, see the [Preparations](#section_n3y_n0g_l1c) section.
2.  Use one of the following methods to configure ENIs based on the operating systems of your instances:
    -   Alibaba Cloud Linux 2: [Configure ENIs for instances that run Alibaba Cloud Linux 2](#section_s2z_h1l_4wh)
    -   CentOS or Red Hat: [Configure ENIs for instances that run CentOS or Red Hat](#section_zx6_9u0_9b0)
    -   Ubuntu or Debian: [Configure ENIs for instances that run Ubuntu or Debian](#section_jiu_ahz_l3t)
    -   SUSE or openSUSE: [Configure ENIs for instances that run SUSE or openSUSE](#section_iae_16f_y2r)
3.  Configure routes for ENIs. For more information, see [Configure routes for ENIs](#section_5yp_ue4_rkv).

## Preparations

You must query the attributes of each ENI, including the primary private IP address, subnet mask, default route, and MAC address. You must also pay attention to the mapping between the ENI name and the MAC address in subsequent configurations.

1.  Remotely connect to an ECS instance. For more information, see [OverviewGuidelines on instance connection](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Query the attributes of each ENI, including the primary private IP address, subnet mask, default route, and MAC address.

    -   Method 1: Query the attributes in the ECS console.
        1.  Log on to the [ECS console](https://ecs.console.aliyun.com).
        2.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
        3.  In the left-side navigation pane, choose **Network & Security** \> **ENIs**.
        4.  On the **Network Interfaces** page, find the ENIs whose attributes you want to query and view their primary private IP addresses and MAC addresses in the **Private IP Address** and **Type/MAC Address\(All\)** columns.
    -   Method 2: Run the curl command to query the attributes from the instance metadata. For more information, see [Overview of instance metadata](/intl.en-US/Instance/Manage instances/Metadata/Overview of instance metadata.md).

        ```
        [root@LocalHost ~]# curl http://100.100.100.200/latest/meta-data/network/interfaces/macs/
        00:16:3e:12:e7:**/
        00:16:3e:12:16:**/
        [root@LocalHost ~]# curl http://100.100.100.200/latest/meta-data/network/interfaces/macs/00:16:3e:12:e7:**/netmask
        255.255.255.0
        [root@LocalHost ~]# curl http://100.100.100.200/latest/meta-data/network/interfaces/macs/00:16:3e:12:e7:**/primary-ip-address
        10.0.0.20
        [root@LocalHost ~]# curl http://100.100.100.200/latest/meta-data/network/interfaces/macs/00:16:3e:12:e7:**/gateway
        10.0.0.253
        ```

    -   Method 3: Call the DescribeNetworkInterfaces operation to query the attributes.
    In this example, the following ENI information is returned:

    ```
    eth1 10.0.0.20/24 10.0.0.253 00:16:3e:12:e7:**
    eth2 10.0.0.21/24 10.0.0.253 00:16:3e:12:16:**
    ```


## Configure ENIs for instances that run Alibaba Cloud Linux 2

eth1 is used in the following example. If you want to configure another ENI, modify the ENI ID.

1.  Open the configuration file of the ENI.

    ```
    vi /etc/systemd/network/60-eth1.network
    ```

2.  Press the I key to enter the edit mode and add the configuration information to the ENI configuration file.

    Choose one of the following configuration information sets based on your needs.

    -   Scenario 1: Assign a dynamic IP address for the ENI over DHCP.

        Sample code:

        ```
        [Match]
        Name=eth1 # Specify the ENI to be configured.
        
        [Network]
        DHCP=yes
        
        [DHCP]
        UseDNS=yes
        ```

    -   Scenario 2: Assign a static IP address for the ENI.

        Sample code:

        ```
        [Match]
        Name=eth1 # Specify the ENI to be configured.
        
        [Network]
        Address=192.168. **. **/24 # Specify the static IP address and subnet mask to be assigned.
        ```

    Press the Esc key, enter `:wq`, and then press the Enter key to save the file and exit the edit mode.

3.  Check the ENI configuration file and confirm the modification.

    ```
    cat /etc/systemd/network/60-eth1.network
    ```

4.  Restart the network service.

    ```
    systemctl restart systemd-networkd
    ```


## Configure ENIs for instances that run CentOS or Red Hat

eth1 is used in the following example. If you want to configure another ENI, modify the ENI ID.

Method 1: Use the multi-nic-util tool.

**Note:** You can download and install the multi-nic-util tool on some CentOS instances to automatically configure ENIs. multi-nic-util supports only images later than CentOS 6.8 or CentOS 7.3.

1.  Download the multi-nic-util tool.

    ```
    wget https://image-offline.oss-cn-hangzhou.aliyuncs.com/multi-nic-util/multi-nic-util-0.6.tgz
    ```

2.  Decompress the package and install the multi-nic-util tool.

    ```
    tar -zxvf multi-nic-util-0.6.tgz
    cd multi-nic-util-0.6
    bash install.sh
    ```

3.  Restart ENI.

    ```
    systemctl restart eni.service
    ```


Method 2: Manually configure the ENI.

1.  Open the configuration file of the ENI.

    ```
    vi /etc/sysconfig/network-scripts/ifcfg-eth1
    ```

2.  Press the I key to enter the edit mode and add the configuration information to the ENI configuration file.

    Sample code:

    ```
    DEVICE=eth1  # Specify the ENI to be configured.
    BOOTPROTO=dhcp
    ONBOOT=yes
    TYPE=Ethernet
    USERCTL=yes
    PEERDNS=no
    IPV6INIT=no
    PERSISTENT_DHCLIENT=yes
    HWADDR=00:16:3e:12:e7:**  # Specify this address as the queried MAC address of the ENI.
    DEFROUTE=no  # Specify that the ENI is not the default route. To prevent the active default route of the ECS instance from being changed when you start the ENI by running the ifup command, do not set eth1 to the default route.
    ```

    Press the Esc key, enter `:wq`, and then press the Enter key to save the file and exit the edit mode.

3.  Check the ENI configuration file and confirm the modification.

    ```
    cat /etc/sysconfig/network-scripts/ifcfg-eth1
    ```

4.  Run the `service network restart` or `systemctl restart network` command to restart the network service.


**Note:** If you want to create custom images after ENIs are configured in your instance, you must first run the /etc/eni\_utils/eni-cleanup command to remove network configurations under /etc/udev/rules.d/70-persistent-net.rules and /etc/sysconfig/network-scripts/.

## Configure ENIs for instances that run Ubuntu or Debian

You can perform the following operations on instances that run Ubuntu 14.04, Ubuntu 16.04, or Debian:

1.  Open the configuration file of an ENI.

    ```
    vi /etc/network/interfaces
    ```

2.  Press the I key to enter the edit mode and add the configuration information to the ENI configuration file.

    eth1 is used in this example:

    ```
    auto eth0
    iface eth0 inet dhcp
    
    auto eth1  # Specify the ENI to be configured.
    iface eth1 inet dhcp
    ```

    Press the Esc key, enter `:wq`, and then press the Enter key to save the file and exit the edit mode.

3.  Check the ENI configuration file and confirm the modification.

    ```
    cat /etc/network/interfaces
    ```

4.  Run the `service networking restart` or `systemctl restart networking` command to restart the network service.


You can perform the following operations on instances that run Ubuntu 18.04:

1.  Create and edit the configuration file of an ENI.

    eth1 is used in this example:

    ```
    vi /etc/netplan/eth1-netcfg.yaml
    ```

2.  Press the I key to enter the edit mode and add the configuration information to the ENI configuration file.

    eth1 is used in this example:

    ```
    network:
      version: 2
      renderer: networkd
      ethernets:
        eth1:
          dhcp4: yes
          dhcp6: no
    ```

    Press the Esc key, enter `:wq`, and then press the Enter key to save the file and exit the edit mode.

    **Note:** When you edit the configuration file, take note of the following items:

    -   The configuration file is in the `YAML` format. Therefore, you must follow the `YAML` syntax rules when you configure the file.
    -   You cannot use tabs for indentation in `YAML` files. Use the space instead.
    -   We recommend that you copy information in the default /etc/netplan/99-netcfg.yaml configuration file to avoid format issues.
3.  Check the ENI configuration file and confirm the modification.

    ```
    cat /etc/netplan/eth1-netcfg.yaml
    ```

4.  Run the `netplan apply` command to make the configuration take effect.


## Configure ENIs for instances that run SUSE or openSUSE

eth1 is used in the following example. If you want to configure another ENI, modify the ENI ID.

1.  Open the configuration file of the ENI.

    ```
    vi /etc/sysconfig/network/ifcfg-eth1
    ```

2.  Press the I key to enter the edit mode and add the configuration information to the ENI configuration file.

    ```
    BOOTPROTO='dhcp4'
    STARTMODE='auto'
    USERCONTROL='no'
    ```

    Press the Esc key, enter `:wq`, and then press the Enter key to save the file and exit the edit mode.

3.  Check the ENI configuration file and confirm the modification.

    ```
    cat /etc/sysconfig/network/ifcfg-eth1
    ```

4.  Run the `service network restart` or `systemctl restart network` command to restart the network service.


## Configure routes for ENIs

1.  Start ENIs.

    1.  Run the `ifup <ENI name>` command to start the dhclient process and initiate a DHCP request.

        ```
        ifup eth1
        ifup eth2
        ```

    2.  Check the allocation of IP addresses. The result must be the same as the ENI information that you queried in the "Preparations" section.

        ```
        [root@ecshost~ ]# ip a
        1: lo:  mtu 65536 qdisc noqueue state UNKNOWN qlen 1
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
        valid_lft forever preferred_lft forever
        2: eth0:  mtu 1500 qdisc pfifo_fast state UP qlen 1000
        link/ether 00:16:3e:0e:16:** brd ff:ff:ff:ff:ff:ff
        inet 10.0.0.19/24 brd 10.0.0.255 scope global dynamic eth0
        valid_lft 31506157sec preferred_lft 31506157sec
        3: eth1:  mtu 1500 qdisc pfifo_fast state UP qlen 1000
        link/ether 00:16:3e:12:e7:** brd ff:ff:ff:ff:ff:ff
        inet 10.0.0.20/24 brd 10.0.0.255 scope global dynamic eth1
        valid_lft 31525994sec preferred_lft 31525994sec
        4: eth2:  mtu 1500 qdisc pfifo_fast state UP qlen 1000
        link/ether 00:16:3e:12:16:** brd ff:ff:ff:ff:ff:ff
        inet 10.0.0.21/24 brd 10.0.0.255 scope global dynamic eth2
        valid_lft 31526009sec preferred_lft 31526009sec
        ```

2.  Set the metric parameter of the default route for each ENI in the route table.

    1.  Set the metric parameter.

        ```
        ip -4 route add default via 10.0.0.253 dev eth1 metric 1001
        ip -4 route add default via 10.0.0.253 dev eth2 metric 1002
        ```

        The preceding commands set the metric parameter of eth1 and eth2 to the following values:

        ```
        eth1: gw: 10.0.0.253 metric: 1001
        eth2: gw: 10.0.0.253 metric: 1002
        ```

    2.  Check whether the configuration succeeds. Pay attention to whether information of the Gateway and Metric columns is the same as the configured information.

        ```
        [root@ecshost~ ]# route -n
        Kernel IP routing table
        Destination Gateway Genmask Flags Metric Ref Use Iface
        0.0.0.0 10.0.0.253 0.0.0.0 UG 0 0 0 eth0
        0.0.0.0 10.0.0.253 0.0.0.0 UG 1001 0 0 eth1
        0.0.0.0 10.0.0.253 0.0.0.0 UG 1002 0 0 eth2
        10.0.0.0 0.0.0.0 255.255.255.0 U 0 0 0 eth0
        10.0.0.0 0.0.0.0 255.255.255.0 U 0 0 0 eth1
        10.0.0.0 0.0.0.0 255.255.255.0 U 0 0 0 eth2
        169.254.0.0 0.0.0.0 255.255.0.0 U 1002 0 0 eth0
        169.254.0.0 0.0.0.0 255.255.0.0 U 1003 0 0 eth1
        169.254.0.0 0.0.0.0 255.255.0.0 U 1004 0 0 eth2
        ```

3.  Create route tables.

    1.  Create the route tables.

        ```
        ip -4 route add default via 10.0.0.253 dev eth1 table 1001
        ip -4 route add default via 10.0.0.253 dev eth2 table 1002
        ```

        **Note:** We recommend that you keep the names of the route tables the same as the metric values of the default routes. 1001 and 1002 are used in this example.

    2.  Check whether the route tables are created.

        ```
        [root@ecshost~ ]# ip route list table 1001
        default via 10.0.0.253 dev eth1
        [root@ecshost~ ]# ip route list table 1002
        default via 10.0.0.253 dev eth2
        ```

4.  Configure policy-based routing.

    1.  Create policy-based routes.

        ```
        ip -4 rule add from 10.0.0.20 lookup 1001
        ip -4 rule add from 10.0.0.21 lookup 1002
        ```

    2.  View routing rules.

        ```
        [root@ecshost~ ]# ip rule list
        0: from all lookup local
        32764: from 10.0.0.21 lookup 1002
        32765: from 10.0.0.20 lookup 1001
        32766: from all lookup main
        32767: from all lookup default
        ```


After the ENIs are configured, you can perform the following operations:

-   [Assign secondary private IP addresses](/intl.en-US/Network/Elastic Network Interfaces/Assign secondary private IP addresses.md)
-   [Modify an ENI](/intl.en-US/Network/Elastic Network Interfaces/Modify an ENI.md)
-   [Unbind an ENI](/intl.en-US/Network/Elastic Network Interfaces/Unbind an ENI.md)
-   [Delete an ENI](/intl.en-US/Network/Elastic Network Interfaces/Delete an ENI.md)

**Related topics**  


[DescribeNetworkInterfaces](/intl.en-US/API Reference/Elastic network interfaces/DescribeNetworkInterfaces.md)

