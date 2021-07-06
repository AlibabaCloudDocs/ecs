---
keyword: [上传公钥, 导入公钥]
---

# 导入SSH密钥对

除在ECS管理控制台新建密钥对外，如果您已经持有使用第三方工具生成的SSH密钥对，可以将公钥导入阿里云。

已获取待导入密钥对的公钥信息。若尚未获取，请参见[查看公钥信息](/intl.zh-CN/安全/SSH密钥对/使用SSH密钥对/查看公钥信息.md)。

**说明：**

-   不要导入私钥。请您妥善保存私钥。使用密钥对绑定ECS实例后，如果没有私钥，您将无法登录该ECS实例。
-   一台ECS实例只能导入一个公钥。

一个账号在一个地域最多可以拥有500个密钥对。更多详情，请参见[SSH密钥对使用限制](/intl.zh-CN/产品简介/使用限制.md)。

导入阿里云的公钥必须使用`Base64`编码，且必须支持下列加密方式中的一种：

-   rsa
-   dsa
-   ssh-rsa
-   ssh-dss
-   ecdsa
-   ssh-rsa-cert-v00@openssh.com
-   ssh-dss-cert-v00@openssh.com
-   ssh-rsa-cert-v01@openssh.com
-   ssh-dss-cert-v01@openssh.com
-   ecdsa-sha2-nistp256-cert-v01@openssh.com
-   ecdsa-sha2-nistp384-cert-v01@openssh.com
-   ecdsa-sha2-nistp521-cert-v01@openssh.com

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  在左侧导航栏，选择**网络与安全** \> **密钥对**。

3.  在顶部菜单栏左上角处，选择地域。

4.  单击**创建密钥对**。

5.  设置密钥对名称，并选择**导入已有密钥对**。

    **说明：** 密钥对名称不能重复。否则，控制台会提示密钥对已存在。

6.  在**公钥内容**文本框中，输入要导入的公钥。

7.  单击**确定**。


[绑定SSH密钥对](/intl.zh-CN/安全/SSH密钥对/使用SSH密钥对/绑定SSH密钥对.md)

**相关文档**  


[ImportKeyPair](/intl.zh-CN/API参考/SSH 密钥对/ImportKeyPair.md)

