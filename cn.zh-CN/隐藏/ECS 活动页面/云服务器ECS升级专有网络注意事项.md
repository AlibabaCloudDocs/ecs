# 云服务器ECS升级专有网络注意事项 {#concept_65497_zh .concept}

如果您的ECS实例的网络类型为经典网络（Classic），建议您升级为专有网络VPC，获取更卓越的网络安全防护效果。

## VPC网段规划 {#section_oty_zmg_jhb .section}

如果您的经典网络实例升级到VPC后需要和同一地域内其他经典网络实例通信，您可以使用ClassicLink功能搭建通信。可以与经典网络互通的VPC网段地址有10.111.0.0/16、172.16.0.0/12和192.168.0.0/16。更多关于ClassicLink功能的使用，请参见[ClassicLink迁移](../../../../intl.zh-CN/用户指南/网络连接/ClassicLink/ClassicLink概述.md#)。

## 升级后的IP { .section}

-   此次物理机网络类型升级将保持您的ECS实例公网IP地址不变，但公网网卡会被移除。

-   升级后的私有IP会从目标虚拟交换机（VSwitch）网段中随机选择。您可以自行创建[VPC](../../../../intl.zh-CN/用户指南/专有网络和子网/管理专有网络.md#)和[VSwitch](../../../../intl.zh-CN/用户指南/专有网络和子网/管理交换机.md#)，也可以使用系统默认选项。升级完成后，您可以自行[修改私有IP](../../../../intl.zh-CN/网络/修改IPv4地址/修改私有IP地址.md#)。


## 云数据库设置 { .section}

-   如果您使用了云数据库服务，您需要在升级之前将云数据库[设置为混访模式](../../../../intl.zh-CN/最佳实践/经典网络迁移到VPC/云数据库混访/云数据库混访概述.md#)。混访模式下，同时支持经典网络类型和VPC类型ECS实例访问云数据库。

-   ECS实例的私有IP地址会发生变化，请提前[更新云数据库白名单](../../../../intl.zh-CN/RDS for MySQL 快速入门/初始化配置/设置白名单.md#)，将虚拟交换机的网段加入到云数据库白名单中。


## 升级时长 { .section}

升级时长为15分钟左右。

## 其他注意事项 { .section}

-   升级前：建议您将应用服务设置为开机自启动，并做好可用性监控。
-   升级后：
    -   升级后软件授权码可能会发生变化。
    -   ECS实例的可用区会发生变化。受影响的关联服务有云数据库RDS、Redis或者MongoDB，请及时调整您的应用配置迁移可用区，确保您的业务能够持续提供服务。
    -   物理机升级的同时会升级底层虚拟化技术，您的ECS磁盘识别名称会发生变化。在Linux实例中，磁盘会被识别为vda、vdb和vdc等。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10947/155861069243662_zh-CN.png)

        阿里云会为Linux实例自动修复/etc/fstab文件，但您仍需关注其他应用是否对设备名有依赖。

    -   如果您长时间未重启或升级过内核，本次重启后可能会有文件系统检查（File System Check, fsck）、相关配置改动失效、启动失败等问题。
    -   磁盘在后台同步数据，时长视磁盘容量而定，通常同步100 GiB需要4小时。此时将暂停磁盘的相关操作，读写性能短暂下降。同步完成后相关操作及性能恢复正常。

一旦出现异常，请及时[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)或者拨打服务热线95187联系阿里云。

## 相关链接 { .section}

更多关于云服务器ECS升级步骤，请参阅[阿里云物理机升级通知](intl.zh-CN/隐藏/ECS 活动页面/阿里云物理机迁移升级通知.md#)。

