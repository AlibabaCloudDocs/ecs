# Alibaba Cloud Linux等保2.0三级版镜像FAQ

本文汇总Alibaba Cloud Linux等保2.0三级版镜像的常见问题及解决方案。

-   [使用Alibaba Cloud Linux等保2.0三级版镜像有什么优势？](#section_fee_2hq_37p)
-   [Alibaba Cloud Linux等保2.0三级版镜像有哪些加固项？加固的内容是什么？](#section_3r8_dqj_9d3)
-   [在实例内进行业务操作是否会影响Alibaba Cloud Linux等保2.0三级版镜像的等保加固配置？](#section_sgq_buv_2yf)
-   [Alibaba Cloud Linux等保2.0三级版镜像是否对系统的性能有影响？](#section_7w6_nwd_6w4)
-   [我为什么不能通过云安全中心进行Alibaba Cloud Linux等保2.0三级版镜像的基线检查？](#section_iga_afq_lpt)
-   [Alibaba Cloud Linux等保2.0三级版镜像为什么不支持SSH密钥对的方式登录？](#section_169_wbt_783)

## 使用Alibaba Cloud Linux等保2.0三级版镜像有什么优势？

-   节省成本：目前Alibaba Cloud Linux等保2.0三级版镜像是完全免费提供使用的。
-   节省人力：云安全中心提供基线检查策略，系统将自动判断实例是否达到了等保合规的要求。
-   节省时间：您可以通过已完成等保加固的自定义镜像，批量创建ECS实例。具体操作，请参见[使用等保镜像批量创建实例](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux等保2.0三级版镜像/使用等保镜像批量创建实例.md)。

## Alibaba Cloud Linux等保2.0三级版镜像有哪些加固项？加固的内容是什么？

系统从身份鉴别、访问控制、安全审计、入侵防范、恶意代码防范等5个方面，共计19个加固项进行加固。每一个加固项以及对应的具体说明，请参见[Alibaba Cloud Linux等保2.0三级版镜像检查规则说明](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux等保2.0三级版镜像/Alibaba Cloud Linux等保2.0三级版镜像使用说明.md)，其中，检查项即为对应的加固项。

## 在实例内进行业务操作是否会影响Alibaba Cloud Linux等保2.0三级版镜像的等保加固配置？

等保镜像只保证系统初始状态的安全，您后续使用时，在系统内的部分操作可能影响到等保加固的配置项。如果加固项出现问题，您可以通过云安全中心进行基线检查，然后根据检查结果自行修复问题。具体操作，请参见[Alibaba Cloud Linux等保2.0三级版镜像基线检查策略配置](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux等保2.0三级版镜像/Alibaba Cloud Linux等保2.0三级版镜像使用说明.md)。

## Alibaba Cloud Linux等保2.0三级版镜像是否对系统的性能有影响？

等保加固的配置项中，只有手动启动的`auditd`服务会对系统性能产生影响，其它配置项默认不会对系统性能造成影响。

## 我为什么不能通过云安全中心进行Alibaba Cloud Linux等保2.0三级版镜像的基线检查？

云安全中心仅企业版支持基线检查服务，如果您需要进行基线检查，请先将云安全中心的版本升级至企业版。具体操作，请参见[升级与降配](/cn.zh-CN/计费与开通服务/升级与降配.md)。

## Alibaba Cloud Linux等保2.0三级版镜像为什么不支持SSH密钥对的方式登录？

等保加固中的多数配置项均为对密码的检查（例如，对密码强度、密码重用次数、密码失效日期以及密码失败策略等配置项的扫描与加固），但没有对SSH密钥对进行检查与加固。为保证等保镜像的安全性，当您完成了等保加固配置后，系统将禁止`root`用户直接登录，其中包含`root`用户的密钥登录方式。

此外，阿里云目前不支持为实例内的非`root`用户创建SSH密钥对，因此您只能通过已创建的普通用户、审计员或安全员用户的用户密码方式登录实例。

