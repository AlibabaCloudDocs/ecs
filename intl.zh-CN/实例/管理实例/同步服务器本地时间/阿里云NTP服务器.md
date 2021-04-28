---
keyword: [阿里云, ecs, 时间校对, 时区]
---

# 阿里云NTP服务器

阿里云提供了内网和公网NTP服务器，用于同步各网络中ECS实例的本地时间。

## 内网和公网NTP服务器

NTP是用于同步网络中计算机时间的协议，全称为网络时间协议（Network Time Protocol）。

时区和时间一致性对于云服务器ECS非常重要，有时会直接影响到任务执行的结果。例如，您在更新数据库或者分析日志时，时间顺序对结果有很大影响。为避免在ECS实例上运行业务时出现逻辑混乱和网络请求错误等问题，您需要统一相关ECS实例的时区设置。另外，您还可以通过NTP服务同步各网络中ECS实例的本地时间。

云服务器ECS为您提供了高精度的时间参考NTP服务器，其中`ntp.cloud.aliyuncs.com`服务器提供分布式的一级时钟源，适用于金融、通讯、科研和天文等以时间精度核心的生产行业。阿里云NTP服务也用于同步ECS实例和其它云产品的本地时间。各网络下的阿里云NTP服务器地址如下表所示。

|经典网络内网|专有网络VPC内网|公网|
|:-----|:--------|:-|
|-|ntp.cloud.aliyuncs.com|ntp.aliyun.com|
|ntp1.cloud.aliyuncs.com|ntp7.cloud.aliyuncs.com|ntp1.aliyun.com|
|ntp2.cloud.aliyuncs.com|ntp8.cloud.aliyuncs.com|ntp2.aliyun.com|
|ntp3.cloud.aliyuncs.com|ntp9.cloud.aliyuncs.com|ntp3.aliyun.com|
|ntp4.cloud.aliyuncs.com|ntp10.cloud.aliyuncs.com|ntp4.aliyun.com|
|ntp5.cloud.aliyuncs.com|ntp11.cloud.aliyuncs.com|ntp5.aliyun.com|
|ntp6.cloud.aliyuncs.com|ntp12.cloud.aliyuncs.com|ntp6.aliyun.com|
|-|-|ntp7.aliyun.com|

## 其他互联网基础服务

阿里云还提供了其他的互联网基础服务，如下表所示。

|公共服务|描述|
|----|--|
|公共DNS：223.5.5.5 / 223.6.6.6|域名：`http://www.alidns.com`|
|公共镜像站：`https://developer.aliyun.com/mirror`|镜像同步频率：每天凌晨2:00−4:00。覆盖了大多数开源软件及Linux发行版。**说明：** 公共镜像站升级维护中。部分镜像仓库功能可以正常使用，您可以手动添加软件源。具体操作，请参见[添加软件源](/intl.zh-CN/实例/管理实例/管理Linux实例软件/添加软件源.md)。 |

## 相关操作

-   [配置Windows实例NTP服务](/intl.zh-CN/实例/管理实例/同步服务器本地时间/配置Windows实例NTP服务.md)
-   [配置Linux实例NTP服务（CentOS 6）](/intl.zh-CN/实例/管理实例/同步服务器本地时间/配置Linux实例NTP服务（CentOS 6）.md)

