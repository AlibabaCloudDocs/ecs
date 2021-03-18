---
keyword: 私有IP地址
---

# 修改私有IP地址

您可以直接修改专有网络中ECS实例的私有IP，也可以通过更改ECS实例所属的交换机来更改ECS实例的私有IP。

-   实例的弹性网卡未设置辅助私网IP地址。
-   实例处于已停止状态。

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  在左侧导航栏，选择**实例与镜像** \> **实例**。

3.  在顶部菜单栏左上角处，选择地域。

4.  找到目标实例，在**操作**区域选择**更多** \> **网络和安全组** \> **修改私有IP**。

5.  在**修改私有IP**对话框，完成配置，然后单击**修改**。

    -   如果您要更换交换机，请确保所选交换机的可用区和实例的可用区相同。
    -   如果您不需要更换交换机，则直接修改私有IP即可。
    ![修改私网IP](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2876649951/p5483.png)

6.  在**操作**区域选择**更多** \> **实例状态** \> **启动**。

    **说明：** ECS实例重新启动后，修改的私有IP生效。


**相关文档**  


[ModifyInstanceVpcAttribute](/intl.zh-CN/API参考/网络/ModifyInstanceVpcAttribute.md)

