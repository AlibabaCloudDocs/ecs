---
keyword: [cloud migration, impot image, ECS, Alibaba Cloud, import an image]
---

# Customize Linux images

If the selected OS is not supported by Alibaba Cloud and cloud-init cannot be installed, you can select Customized Linux when you import a custom image. Alibaba Cloud regards customized Linux images as an unrecognized OS type. You must add a parsing script to the custom image before the import to automatically configure the instance when the instance is first started.

## Limits

Customized Linux images have the following limits:

-   The first partition must be writable.
-   The type of the first partition must be FAT32, ext2, ext3, ext4, or UFS.
-   The size of the virtual file of the customized Linux image must be larger than 5 GiB.

Customized Linux images have the following security requirements:

-   No important vulnerabilities can be remotely exploited.
-   When you log on to an instance for the first time by using a VNC management terminal of the ECS console, you must change the initial password \(if there is one\) before you can perform any other actions. For more information, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).
-   Default SSH key pairs are not supported. The initial SSH key pair must be generated by Alibaba Cloud.

## Configuration method

Before you create and import a customized Linux image, you must perform the following operations:

1.  Create the aliyun\_custom\_image directory in the root directory of the first partition of the server from which the image is created.

    When the instance created from the customized Linux image is started for the first time, Alibaba Cloud writes instance configurations to the os.conf file in the aliyun\_custom\_image directory. If the os.conf file does not exist, Alibaba Cloud will create one.

2.  Create a parsing script in the image to parse the os.conf file to implement instance configurations.

    For more information about how to write a script, see [Considerations for the parsing script](#configureparsingscript) and [Example of the parsing script](#scriptdemo).


## Example of the os.conf file

-   os.conf file for instances in the classic network

    ```
    hostname=<yourHostName>
    password=<yourPassword>
    eth0_ip_addr=10.0.0.2
    eth0_mac_addr=00:xx:xx:xx:xx:23
    eth0_netmask=255.255.255.0
    eth0_gateway=10.0.0.1
    eth0_route="10.0.0.0/8 10.0.0.1;172.16.0.0/12 10.0.0.1"
    eth1_ip_addr=42.0.0.2
    eth1_mac_addr=00:xx:xx:xx:xx:24
    eth1_netmask=255.255.255.0
    eth1_gateway=42.0.0.1
    eth1_route="0.0.0.0/0 42.0.0.1"
    dns_nameserver="7.7.7.7 8.8.8.8"
    ```

    The following table describes the parameters in the preceding example.

    |Parameter|Description|
    |:--------|:----------|
    |hostname|The name of the host.|
    |password|The password. It must be a Base64-encoded string.|
    |eth0\_ip\_addr|The IP address of the eth0 NIC.|
    |eth0\_mac\_addr|The MAC address of the eth0 NIC.|
    |eth0\_netmask|The network mask of the eth0 NIC.|
    |eth0\_gateway|The default gateway of the eth0 NIC.|
    |eth0\_route|The eth0 internal routes. By default, routes are separated with semicolons \(;\).|
    |eth1\_ip\_addr|The IP address of the eth1 NIC.|
    |eth1\_mac\_addr|The MAC address of the eth1 NIC.|
    |eth1\_netmask|The network mask of the eth1 NIC.|
    |eth1\_gateway|The default gateway of the eth1 NIC.|
    |eth1\_route|The eth1 Internet routes. By default, routes are separated with semicolons \(;\).|
    |dns\_nameserver|The DNS address list. By default, addresses are separated with spaces.|

-   os.conf file for instances in VPCs

    ```
    hostname=<yourHostName>
    password=<yourPassword>
    eth0_ip_addr=10.0.0.2
    eth0_mac_addr=00:xx:xx:xx:xx:23
    eth0_netmask=255.255.255.0
    eth0_gateway=10.0.0.1
    eth0_route="0.0.0.0/0 10.0.0.1"
    dns_nameserver="7.7.7.7 8.8.8.8"
    ```

    The following table describes the parameters in the preceding example.

    |Parameter|Description|
    |:--------|:----------|
    |hostname|The name of the host.|
    |password|The password. It must be a Base64-encoded string.|
    |eth0\_ip\_addr|The IP address of the eth0 NIC.|
    |eth0\_mac\_addr|The MAC address of the eth0 NIC.|
    |eth0\_netmask|The network mask of the eth0 NIC.|
    |eth0\_gateway|The default gateway of the eth0 NIC.|
    |eth0\_route|The eth0 internal routes. By default, routes are separated with semicolons \(;\).|
    |dns\_nameserver|The DNS address list. By default, addresses are separated with spaces.|


## Considerations for the parsing script

Typically, when an instance is started for the first time, Alibaba Cloud writes instance configurations to the os.conf file. The os.conf file is in the aliyun\_custom\_image directory in the root directory of the partition. However, for a customized Linux image, you must create a predefined parsing script. The script reads the configurations from the os.conf file to configure the instance.

The parsing script must meet the conditions described in the following table.

|Condition|Description|
|:--------|:----------|
|Automatic start at system startup|Set the parsing script to run automatically at system startup by placing the script in the /etc/init.d/ directory.|
|Values for configuration items|As shown in the [Example of the os.conf](#configurationfiledemo) section, classic network-type and VPC-type instances differ in the number of configuration items and values of some configuration items.|
|Path for the configuration file|The device name allocated to the first partition for instances created from the customized Linux image varies depending on whether the instance is I/O optimized. We recommend that you use `uuid` or `label` in your parsing code to identify the device allocated for the first partition. The user password must be Base64-encoded in the parsing script.|
|Network type|The parsing script can determine the network type by checking whether eth1\_route or eth1-related configuration items exist. The script parses and processes the instance accordingly based on the network type. -   VPC-type instances are configured with the default Internet route specified by the eth0\_route parameter in the os.conf file.
-   Classic network-type instances are configured with the default Internet route specified by the eth1\_route parameter in the os.conf file, and with the default internal route specified by the eth0\_route parameter. |
|Configuration optimization|Configurations in the os.conf file are executed only once during the instance lifecycle. We recommend that you delete the os.conf file after the parsing script is executed. The parsing script will not execute the configurations in the os.conf file if the script does not read any configurations.|
|Customized image processing|When a custom image is created based on a customized Linux image, the automatic startup script is also included. Alibaba Cloud will write configurations to the os.conf file when the instance is started for the first time. Then, the parsing script will immediately execute the configurations upon detection.|
|Configuration change processing|When instance configurations are changed by using the Alibaba Cloud console or calling an API operation, Alibaba Cloud writes new configurations to the os.conf file. Then, the parsing script will run again to issue the changes.|

## Example of the parsing script

A parsing script for CentOS is used in this example. You must change the script content based on your operating system and debug the script before you execute it.

```
#! /bin/bash

### BEGIN INIT INFO
# Provides:          os-conf
# Required-Start:    $local_fs $network $named $remote_fs
# Required-Stop:
# Should-Stop:
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: The initial os-conf job, config the system.
### END INIT INFO

first_partition_dir='/boot/'
os_conf_dir=${first_partition_dir}/aliyun_custom_image
os_conf_file=${os_conf_dir}/os.conf

load_os_conf() {
    if [[ -f $os_conf_file ]]; then
        . $os_conf_file
        return 0
    else
        return 1
    fi
}

cleanup() {
    # ensure $os_conf_file is deleted, to avoid repeating config system
    rm $os_conf_file >& /dev/null
    # ensure $os_conf_dir exists
    mkdir -p $os_conf_dir
}

config_password() {
    if [[ -n $password ]]; then
        password=$(echo $password | base64 -d)
        if [[ $? == 0 && -n $password ]]; then
            echo "root:$password" | chpasswd
        fi
    fi
}

config_hostname() {
    if [[ -n $hostname ]]; then
        sed -i "s/^HOSTNAME=. */HOSTNAME=$hostname/" /etc/sysconfig/network
        hostname $hostname
    fi
}

config_dns() {
    if [[ -n $dns_nameserver ]]; then
        dns_conf=/etc/resolv.conf
        sed -i '/^nameserver.*/d' $dns_conf
        for i in $dns_nameserver; do
            echo "nameserver $i" >> $dns_conf
        done
    fi
}

is_classic_network() {
    # vpc: eth0
    # classic: eth0 eth1
    grep -q 'eth1' $os_conf_file
}

config_network() {
    /etc/init.d/network stop
    config_interface eth0 ${eth0_ip_addr} ${eth0_netmask} ${eth0_mac_addr}
    config_route eth0 "${eth0_route}"
    if is_classic_network ; then
        config_interface eth1 ${eth1_ip_addr} ${eth1_netmask} ${eth1_mac_addr}
        config_route eth1 "${eth1_route}"
    fi
    /etc/init.d/network start
}

config_interface() {
    local interface=$1
    local ip=$2
    local netmask=$3
    local mac=$4
    interface_cfg="/etc/sysconfig/network-scripts/ifcfg-${interface}"
    cat << EOF > $interface_cfg
DEVICE=$interface
IPADDR=$ip
NETMASK=$netmask
HWADDR=$mac
ONBOOT=yes
BOOTPROTO=static
EOF
}

config_default_gateway() {
    local gateway=$1
    sed -i "s/^GATEWAY=. */GATEWAY=$gateway/" /etc/sysconfig/network
}

config_route() {
    local interface=$1
    local route="$2"
    route_conf=/etc/sysconfig/network-scripts/route-${interface}
    > $route_conf
    echo $route | sed 's/;/\n/' | \
        while read line; do
            dst=$(echo $line | awk '{print $1}')
            gw=$(echo $line | awk '{print $2}')
            if ! grep -q "$dst" $route_conf 2> /dev/null; then
                echo "$dst via $gw dev $interface" >> $route_conf
            fi
            if [[ "$dst" == "0.0.0.0/0" ]]; then
                config_default_gateway $gw
            fi
        done
}

################## sysvinit service portal ####################

start() {
    if load_os_conf ; then
        config_password
        config_network
        config_hostname
        config_dns
        cleanup
        return 0
    else
        echo "not load $os_conf_file"
        return 0
    fi
}

RETVAL=0

case "$1" in
    start)
        start
        RETVAL=$?
    ;;
    *)
        echo "Usage: $0 {start}"
        RETVAL=3
    ;;
esac

exit $RETVAL
```

