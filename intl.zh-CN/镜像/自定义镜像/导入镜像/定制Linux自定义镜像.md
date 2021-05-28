---
keyword: [上云, impotImage, ecs, 阿里云, 导入镜像]
---

# 定制Linux自定义镜像

当镜像的操作系统不在阿里云所支持的平台列表中，并且不能安装cloud-init时，您可以在导入自定义镜像时选择Customized Linux（定制版镜像）。阿里云将定制版Linux镜像当作无法识别的操作系统，您需要在导入镜像前，根据本文描述在镜像中添加解析脚本，便于初次启动时自动化配置实例。

## 限制要求

Customized Linux镜像具有如下限制条件：

-   第一个分区必须可以被写入。
-   第一个分区的文件类型只能是FAT32、EXT2、EXT3、EXT4或UFS。
-   虚拟文件的大小必须大于5GiB。

Customized Linux镜像具有如下安全要求：

-   不能存在可被远程利用的高危漏洞。
-   使用控制台的管理终端（VNC）登录实例时，如果存在初始默认密码，您必须在首次登录时修改，修改密码之前不允许进入实例做任何操作。详情请参见[通过密码认证登录Linux实例](/intl.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
-   不支持默认SSH密钥对，初始SSH密钥对必须由阿里云生成。

## 配置方法

制作并导入Customized Linux自定义镜像前，您需要进行如下配置。

1.  在镜像的第一个分区的根目录下新建目录aliyun\_custom\_image。

    使用该Customized Linux镜像所创建的实例初次启动时，阿里云会在aliyun\_custom\_image目录的os.conf文件中写入实例相关配置信息。如果不存在os.conf文件，则系统自动创建。

2.  在镜像中创建一份解析脚本，用以解析os.conf文件的系统配置。

    编写脚本，请参见[解析脚本注意事项](#configureparsingscript)和[解析脚本示例](#scriptdemo)。


## os.conf文件示例

-   经典网络类型实例os.conf文件示例。

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

    示例中各参数说明如下表所示。

    |参数名称|参数说明|
    |:---|:---|
    |hostname|主机名参数|
    |password|密码参数，Base64编码的字符串|
    |eth0\_ip\_addr|eth0网卡IP地址|
    |eth0\_mac\_addr|eth0网卡MAC地址|
    |eth0\_netmask|eth0网卡掩码|
    |eth0\_gateway|eth0网卡默认网关|
    |eth0\_route|eth0内网路由列表，默认用半角分号分隔|
    |eth1\_ip\_addr|eth1网卡IP地址|
    |eth1\_mac\_addr|eth1网卡MAC地址|
    |eth1\_netmask|eth1网卡掩码|
    |eth1\_gateway|eth1网卡默认网关|
    |eth1\_route|eth1公网路由列表，默认用半角分号分隔|
    |dns\_nameserver|DNS地址列表，默认用空格分隔|

-   专有网络VPC类型实例os.conf文件示例。

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

    示例中各参数说明如下表所示。

    |参数名称|参数说明|
    |:---|:---|
    |hostname|主机名参数|
    |password|密码参数，Base64编码的字符串|
    |eth0\_ip\_addr|eth0网卡IP地址|
    |eth0\_mac\_addr|eth0网卡MAC地址|
    |eth0\_netmask|eth0网卡掩码|
    |eth0\_gateway|eth0网卡默认网关|
    |eth0\_route|eth0内网路由列表，默认用半角分号分隔|
    |dns\_nameserver|DNS地址列表，默认用空格分隔|


## 解析脚本注意事项

实例初次启动时，正常情况下阿里云自动将配置项的相关信息写入第一个分区的根目录下aliyun\_custom\_image目录的os.conf文件中。配置Customized Linux镜像必须要在镜像中创建预定义解析脚本，用以从os.conf文件中读取实例配置信息并完成实例配置。

解析脚本需要满足的条件，如下表所示。

|需满足的条件|配置说明|
|:-----|:---|
|开机启动|解析脚本需要设置成开机自启动，例如，将解析脚本存放在/etc/init.d/目录下。|
|配置项取值规则|如[os.conf 文件示例](#configurationfiledemo)的配置项所述，VPC与经典网络类型实例的配置项数量和部分配置项的取值规则均有所不同。|
|配置文件读取路径|Customized Linux镜像在创建I/O优化实例或非I/O优化实例时，为第一个分区所分配的设备名默认不一样。所以在解析脚本中建议使用`uuid`或`label`识别第一个分区的设备。用户密码为Base64编码的字符串，设置密码时需要做相关处理。|
|判断VPC或经典网络|解析脚本判断该网络类型时，可以查看是否存在eth1\_route或其他eth1相关的配置项。判断出当前实例的网络类型后再有针对性地解析和处理。 -   VPC类型实例在os.conf文件的eth0\_route参数中配置默认公网路由。
-   经典网络类型实例在os.conf文件的eth1\_route参数中配置默认公网路由，内网路由配置在eth0\_route中。 |
|配置优化|os.conf文件中的配置在实例的整个生命周期中执行一次即可，解析脚本执行成功后建议删除os.conf文件。同时解析脚本如果没有读取到os.conf文件配置，则不执行文件中的配置。|
|自定义镜像处理|根据Customized Linux镜像创建的实例再制作自定义镜像时，镜像中也会包含这个开机启动脚本。阿里云会在实例第一次启动时写入os.conf配置，解析脚本在检测到该配置时即可执行相关配置。|
|修改相关配置时的处理|当实例的配置信息通过阿里云的控制台或API发生变更时，阿里云将相关信息写入到os.conf文件中，解析脚本将被再次执行从而下发这些更改。|

## 解析脚本示例

解析脚本以CentOS操作系统为例，仅供您参考。实际操作时，请根据操作系统类型调整脚本内容。使用脚本前，务必在镜像中调试脚本，并保证调试通过。

```
#!/bin/bash

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
        sed -i "s/^HOSTNAME=.*/HOSTNAME=$hostname/" /etc/sysconfig/network
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
    sed -i "s/^GATEWAY=.*/GATEWAY=$gateway/" /etc/sysconfig/network
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

