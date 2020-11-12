---
keyword: [Alibaba Cloud Linux, Windows Server, CentOS, Ubuntu, Debian, CoreOS, Red Hat, OpenSUSE]
---

# Known issues

This topic describes known issues of Alibaba Cloud images for different operating systems, the scope of these issues, and their corresponding solutions.

## SUSE Linux Enterprise Server 12 SP5: Kernel updates may lead to startup hangs

-   Problem description: After an earlier kernel version is updated to SUSE Linux Enterprise Server \(SLES\) 12 SP5, or after an internal kernel version of SLES 12 SP5 is updated, instances may have the issue of startup hangs for some CPU types. These known CPU types are `Intel®Xeon®CPU E5-2682 v4 @ 2.50GHz` and `Intel®Xeon®CPU E7-8880 v4 @ 2.20GHz`. The following code describes the debugging result of the corresponding calltrace:

    ```
    [    0.901281] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
    [    0.901281] CR2: ffffc90000d68000 CR3: 000000000200a001 CR4: 00000000003606e0
    [    0.901281] DR0: 0000000000000000 DR1: 0000000000000000 DR2: 0000000000000000
    [    0.901281] DR3: 0000000000000000 DR6: 00000000fffe0ff0 DR7: 0000000000000400
    [    0.901281] Call Trace:
    [    0.901281]  cpuidle_enter_state+0x6f/0x2e0
    [    0.901281]  do_idle+0x183/0x1e0
    [    0.901281]  cpu_startup_entry+0x5d/0x60
    [    0.901281]  start_secondary+0x1b0/0x200
    [    0.901281]  secondary_startup_64+0xa5/0xb0
    [    0.901281] Code: 6c 01 00 0f ae 38 0f ae f0 0f 1f 84 00 00 00 00 00 0f 1f 84 00 00 00 00 00 90 31 d2 65 48 8b 34 25 40 6c 01 00 48 89 d1 48 89 f0 <0f> 01 c8 0f 1f 84 00 00 00 00 00 0f 1f 84 00 00 00 00 00 ** **
    ```

-   Cause: The new kernel version is incompatible with the CPU microcode.
-   Solution: In the `/boot/grub2/grub.cfg` file, add the `idle` kernel parameter to the row that begins with `linux` and set this parameter to nomwait. The following example shows how to modify the file:

    ```
    menuentry 'SLES 12-SP5'  --class sles --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-simple-fd7bda55-42d3-4fe9-a2b0-45efdced****' {
            load_video
            set gfxpayload=keep
            insmod gzio
            insmod part_msdos
            insmod ext2
            set root='hd0,msdos1'
            if [ x$feature_platform_search_hint = xy ]; then
              search --no-floppy --fs-uuid --set=root --hint='hd0,msdos1'  fd7bda55-42d3-4fe9-a2b0-45efdced****
            else
              search --no-floppy --fs-uuid --set=root fd7bda55-42d3-4fe9-a2b0-45efdced****
            fi
            echo    'Loading Linux 4.12.14-122.26-default ...'
            linux   /boot/vmlinuz-4.12.14-122.26-default root=UUID=fd7bda55-42d3-4fe9-a2b0-45efdced****  net.ifnames=0 console=tty0 console=ttyS0,115200n8 mitigations=auto splash=silent quiet showopts idle=nomwait
            echo    'Loading initial ramdisk ...'
            initrd  /boot/initrd-4.12.14-122.26-default
    }
    ```


## openSUSE 15: Kernel updates may lead to startup hangs

-   Problem description: After openSUSE kernel versions are updated to `4.12.14-lp151.28.52-default`, instances may have the issue of startup hangs for some CPU types. The known CPU type is `Intel®Xeon®CPU E5-2682 v4 @ 2.50GHz`. The following code describes the debugging result of the corresponding calltrace:

    ```
    [    0.901281] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
    [    0.901281] CR2: ffffc90000d68000 CR3: 000000000200a001 CR4: 00000000003606e0
    [    0.901281] DR0: 0000000000000000 DR1: 0000000000000000 DR2: 0000000000000000
    [    0.901281] DR3: 0000000000000000 DR6: 00000000fffe0ff0 DR7: 0000000000000400
    [    0.901281] Call Trace:
    [    0.901281]  cpuidle_enter_state+0x6f/0x2e0
    [    0.901281]  do_idle+0x183/0x1e0
    [    0.901281]  cpu_startup_entry+0x5d/0x60
    [    0.901281]  start_secondary+0x1b0/0x200
    [    0.901281]  secondary_startup_64+0xa5/0xb0
    [    0.901281] Code: 6c 01 00 0f ae 38 0f ae f0 0f 1f 84 00 00 00 00 00 0f 1f 84 00 00 00 00 00 90 31 d2 65 48 8b 34 25 40 6c 01 00 48 89 d1 48 89 f0 <0f> 01 c8 0f 1f 84 00 00 00 00 00 0f 1f 84 00 00 00 00 00 ** **
    ```

-   Cause: The new kernel version is incompatible with the CPU microcode. For more information, visit [Issues of startup hangs](https://bugzilla.opensuse.org/show_bug.cgi?id=1172886#c1).
-   Involved image: opensuse\_15\_1\_x64\_20G\_alibase\_20200520.vhd
-   Solution: In the /boot/grub2/grub.cfg file, add the `idle` kernel parameter to the row that begins with `linux` and set this parameter to nomwait. The following example shows how to modify the file:

    ```
    menuentry 'openSUSE Leap 15.1'  --class opensuse --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-simple-20f5f35a-fbab-4c9c-8532-bb6c66ce****' {
            load_video
            set gfxpayload=keep
            insmod gzio
            insmod part_msdos
            insmod ext2
            set root='hd0,msdos1'
            if [ x$feature_platform_search_hint = xy ]; then
              search --no-floppy --fs-uuid --set=root --hint='hd0,msdos1'  20f5f35a-fbab-4c9c-8532-bb6c66ce****
            else
              search --no-floppy --fs-uuid --set=root 20f5f35a-fbab-4c9c-8532-bb6c66ce****
            fi
            echo    'Loading Linux 4.12.14-lp151.28.52-default ...'
            linux   /boot/vmlinuz-4.12.14-lp151.28.52-default root=UUID=20f5f35a-fbab-4c9c-8532-bb6c66ce****  net.ifnames=0 console=tty0 console=ttyS0,115200n8 splash=silent mitigations=auto quiet idle=nomwait
            echo    'Loading initial ramdisk ...'
            initrd  /boot/initrd-4.12.14-lp151.28.52-default
    }
    ```


## CentOS 8.0: The version update of the public image leads to the change of image version number of created instances

-   Problem description: After you connect to an instance created from the centos\_8\_0\_x64\_20G\_alibase\_20200218.vhd public image, you find that the system version of the instance is CentOS 8.1.

    ```
    root@ecshost:~$ lsb\_release -a
    LSB Version:    :core-4.1-amd64:core-4.1-noarch
    Distributor ID:    CentOS
    Description:    CentOS Linux release 8.1.1911 (Core)
    Release:    8.1.1911
    Codename:    Core
    ```

-   Cause: The centos\_8\_0\_x64\_20G\_alibase\_20200218.vhd image is in the public image list and was updated by using the latest community update package. The image was upgraded and the actual system version is CentOS 8.1.

    ![centos_8_0_x64_20G_alibase_20200218.vhd](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5763559951/p94918.png)

-   Involved image: centos\_8\_0\_x64\_20G\_alibase\_20200218.vhd.
-   Solution: You can call operations such as [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md) and set `ImageId` to centos\_8\_0\_x64\_20G\_alibase\_20191225.vhd to create an instance whose system version is CentOS 8.0.

## Debian 9.6: Classic network-type instances have network configuration issues

-   Problem description: Classic network-type instances created from Debian 9 public images cannot be pinged.
-   Cause: Classic network-type instances created from Debian 9 public images cannot be automatically assigned IP addresses by using Dynamic Host Configuration Protocol \(DHCP\) because the systemd-networkd service is disabled by default in Debian 9.
-   Involved image: debian\_9\_06\_64\_20G\_alibase\_20181212.vhd.
-   Solution: Run the following commands in sequence:

    ```
    systemctl enable systemd-networkd 
    ```

    ```
    systemctl start systemd-networkd
    ```


## CentOS 6.8: An instance installed with the NFS client fails to respond

-   Problem description: A CentOS 6.8 instance installed with the NFS client fails to respond and must be restarted.
-   Cause: When you use the NFS service on instances whose operating system kernel versions are 2.6.32-696 to 2.6.32-696.10, the NFS client attempts to end a TCP connection if a glitch occurs due to communication latency. Specifically, if the NFS server is delayed in sending a response to the NFS client, the connection initiated by the NFS client may be stalled in the FIN\_WAIT2 state. Typically, the connection expires and closes one minute after the connection enters the FIN\_WAIT2 state and the NFS client can initiate another connection. However, kernel versions 2.6.32-696 to 2.6.32-696.10 have issues with establishing TCP connections. As a result, the connection remains in the FIN\_WAIT2 state, the NFS client is unable to recover the TCP connection, and a new TCP connection cannot be initiated. The requests hang, and the only way to fix the issue is to restart the instance.
-   Involved images: centos\_6\_08\_32\_40G\_alibase\_20170710.vhd and centos\_6\_08\_64\_20G\_alibase\_20170824.vhd.
-   Solution: Run the yum update command to update the kernel to 2.6.32-696.11 or later.

    **Note:** Before you perform operations on the instance, you must create a snapshot to back up your data. For more information, see [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).


## CentOS 7: The hostname changes from uppercase to lowercase letters after an instance restarts

-   Problem description: When ECS instances are restarted for the first time, the hostnames of some instances that run CentOS 7 change from uppercase to lowercase letters. The following table describes some examples.

    |Hostname|Hostname after the instance is restarted for the first time|Does the hostname remain in lowercase after the restart?|
    |:-------|:----------------------------------------------------------|:-------------------------------------------------------|
    |iZm5e1qe\*\*\*\*\*sxx1ps5zX|izm5e1qe\*\*\*\*\*sxx1ps5zx|Yes|
    |ZZHost|zzhost|Yes|
    |NetworkNode|networknode|Yes|

-   Involved images: the following CentOS public images and custom images derived from these public images:
    -   centos\_7\_2\_64\_40G\_base\_20170222.vhd
    -   centos\_7\_3\_64\_40G\_base\_20170322.vhd
    -   centos\_7\_03\_64\_40G\_alibase\_20170503.vhd
    -   centos\_7\_03\_64\_40G\_alibase\_20170523.vhd
    -   centos\_7\_03\_64\_40G\_alibase\_20170625.vhd
    -   centos\_7\_03\_64\_40G\_alibase\_20170710.vhd
    -   centos\_7\_02\_64\_20G\_alibase\_20170818.vhd
    -   centos\_7\_03\_64\_20G\_alibase\_20170818.vhd
    -   centos\_7\_04\_64\_20G\_alibase\_201701015.vhd
-   Involved hostnames: If the hostnames of your applications are case-sensitive, the availability of corresponding services may be affected when you restart such instances. The following table describes whether the hostname changes after an instance is restarted.

    |Current state of hostname|Does the hostname change after an instance restart?|When does the change occur?|Continue reading this section?|
    |:------------------------|:--------------------------------------------------|:--------------------------|:-----------------------------|
    |The hostname contains uppercase letters when you create the instance by using the ECS console or by calling ECS API operations.|Yes|When the instance is restarted for the first time|Yes|
    |The hostname contains only lowercase letters when you create the instance by using the ECS console or by calling ECS API operations.|No|N/A|No|
    |The hostname contains uppercase letters, and you modify the hostname after you log on to the instance.|No|N/A|Yes|

-   Solution: To retain uppercase letters in the hostname of an instance after you restart the instance, perform the following operations:
    1.  Connect to your instance. For more information, see [Connection methods](/intl.en-US/Instance/Connect to instances/Overview.md).
    2.  View the existing hostname.

        ```
        [root@izbp193*****3i161uynzzx ~]# hostname
        izbp193*****3i161uynzzx
        ```

    3.  Run the following command to staticize the hostname:

        ```
        hostnamectl set-hostname --static iZbp193*****3i161uynzzX
        ```

    4.  Run the following commands to view the updated hostname:

        ```
        [root@izbp193*****3i161uynzzx ~]# hostname
        iZbp193*****3i161uynzzX
        ```

-   Additional actions: If you are using a custom image, we recommend that you update cloud-init to the latest version and create a custom image again to prevent the previous issue from occurring to the custom image. For more information, see [Install cloud-init](/intl.en-US/Images/Custom image/Import images/Install cloud-init.md) and [Create a custom image from an instance](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from an instance.md).

## Linux: Pip requests time out

-   Problem description: Pip requests occasionally time out or fail.
-   Involved images: CentOS, Debian, Ubuntu, SUSE, openSUSE, and Alibaba Cloud Linux.
-   Cause: Alibaba Cloud provides three pip source addresses. The default address is mirrors.aliyun.com. To access this address, instances must be able to access the Internet. If your instance is not assigned with a public IP address, pip requests time out.
    -   The public source address \(default\): mirrors.aliyun.com
    -   The internal source address in VPCs: mirrors.cloud.aliyuncs.com
    -   The internal source address in the classic network: mirrors.aliyuncs.com
-   Solution: You can solve the problem by using one of the following methods:
    -   Method 1

        Assign a public IP address to your instance by associating an elastic IP address \(EIP\) with your instance. For more information, see [Overview](/intl.en-US/User Guide/Associate an EIP with a cloud instance/Bind an EIP to a secondary ENI/Overview.md).

        A subscription instance can also be reassigned with a public IP address by means of configuration upgrade or downgrade. For more information, see [Upgrade the instance types of subscription instances](/intl.en-US/Instance/Change configurations/Change instance types/Upgrade the instance types of subscription instances.md).

    -   Method 2

        If a pip request fails, you can run the fix\_pypi.sh script in your ECS instance and retry the pip operation. Specifically, perform the following operations:

        1.  Connect to your instance. For more information, see [Connect to a Linux instance by using VNC](/intl.en-US/Instance/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using VNC.md).
        2.  Run the following command to obtain the script file:

            ```
            wget http://image-offline.oss-cn-hangzhou.aliyuncs.com/fix/fix_pypi.sh
            ```

        3.  Run one of the following scripts based on the network type of the instance:
            -   For instances in VPCs, run the `bash fix_pypi.sh "mirrors.cloud.aliyuncs.com"` script.
            -   For instances in the classic network, run the `bash fix_pypi.sh "mirrors.aliyuncs.com"` script.
        4.  Retry the pip operation.
        The following section describes the fix\_pypi.sh script:

        ```
        #! /bin/bash
        
        function config_pip() {
            pypi_source=$1
        
            if [[ ! -f ~/.pydistutils.cfg ]]; then
        cat > ~/.pydistutils.cfg << EOF
        [easy_install]
        index-url=http://$pypi_source/pypi/simple/
        EOF
            else
                sed -i "s#index-url.*#index-url=http://$pypi_source/pypi/simple/#" ~/.pydistutils.cfg
            fi
        
            if [[ ! -f ~/.pip/pip.conf ]]; then
            mkdir -p ~/.pip
        cat > ~/.pip/pip.conf << EOF
        [global]
        index-url=http://$pypi_source/pypi/simple/
        [install]
        trusted-host=$pypi_source
        EOF
            else
                sed -i "s#index-url.*#index-url=http://$pypi_source/pypi/simple/#" ~/.pip/pip.conf
                sed -i "s#trusted-host.*#trusted-host=$pypi_source#" ~/.pip/pip.conf
            fi
        }
        
        config_pip $1
        ```


