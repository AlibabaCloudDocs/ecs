# 通过PAM凭据认证登录实例

Workbench已接入特权访问管理中心（PAM），将实例的用户名、密码、密钥托管至PAM后，无需每次输入这些信息即可安全登录实例，且登录Linux实例和Windows实例的操作一致，更加方便快捷。

ECS实例处于**运行中**状态。

阿里云特权访问管理中心通过免密登录、RAM权限托管、RDP/SSH代理、安全审计和风控能力，提供有效的运维会话审计功能，实现事前和事中智能风控，有效规避因多次分享登录账号密码、权限管理不当等原因导致的数据泄露风险。更多信息，请参见[什么是特权访问管理中心]()。

## 操作步骤

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  在左侧导航栏，选择**实例与镜像** \> **实例**。

3.  在顶部菜单栏左上角处，选择地域。

4.  在**实例列表**页面，找到待连接的实例，在**操作**区域单击**远程连接**。

5.  在弹出的**远程连接与命令**对话框中，单击**Workbench远程连接**对应的**立即登录**。

6.  在**登录实例**对话框中，配置登录信息并登录实例。

    -   如果没有PAM凭据：
        1.  配置登录信息。

            |配置项|说明|
            |---|--|
            |**实例**|自动填充，您也可以手动选择其它实例。|
            |**网络连接**|选择**安全运维（PAM）**。**说明：** 如果尚未使用过特权访问管理中心，会弹出服务开通提醒，请按页面提示操作。 |
            |**PAM凭据**|选择**新增凭据**。|

        2.  在**将实例凭据存储到PAM**对话框中，输入新增PAM凭据的信息。

            |配置项|说明|
            |---|--|
            |**用户名**|输入用户名，例如root。|
            |**凭据类型**|支持以下类型：            -   **密码**：必须继续输入密码。
            -   **密钥**：必须继续输入或上传证书。如果证书已加密，还需要输入解密口令。 |
            |**凭证备注**|填写PAM凭据的描述信息，以便日后管理。|

        3.  选中**我确认将凭据存储到PAM托管的实例上**。
        4.  单击**确认**。
        5.  在**登录实例**对话框中，选择新增的PAM凭据，然后单击**确定**。
    -   如果已有PAM凭据：
        1.  配置登录信息。

            |配置项|说明|
            |---|--|
            |**实例**|自动填充，您也可以手动选择其它实例。|
            |**网络连接**|选择**安全运维（PAM）**。|
            |**PAM凭据**|选择已有的PAM凭据。|

        2.  单击**确定**。

## 常见问题

无法连接实例时，您可以自行排查，详情请参见[远程连接FAQ]()和[GuestOS常见问题与修复方案](https://help.aliyun.com/document_detail/175789.html)。

