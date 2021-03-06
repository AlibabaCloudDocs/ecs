---
keyword: [Workbench, 远程连接]
---

# 通过密码或密钥认证登录Linux实例

相比VNC，Workbench支持多用户远程连接同一台实例，并且支持可视化管理Linux实例中的文件，更加高效便捷。

-   实例已设置登录密码或者绑定密钥对。
-   实例处于**运行中**状态。
-   实例所在安全组已允许Workbench服务相关的IP访问实例，安全组规则详情和网络类型有关。更多信息，请参见[Workbench相关安全组规则详情](#section_bou_2ru_qr4)。

Workbench的远程连接会话默认维持6个小时，如果您超过6小时没有任何操作，连接会自动断开，您需要重新连接实例。

使用Workbench连接实例时，支持以下协议：

-   终端连接（SSH）协议：连接Linux实例时默认使用的协议，也支持连接安装了仿GNU系统（例如Cygwin）的Windows实例。关于如何连接Linux实例，请参见[基于终端连接（SSH）协议连接Linux实例](#section_cqq_y6e_42w)。
-   远程桌面（RDP）协议：连接Windows实例时默认使用的协议，也支持连接开启了远程桌面服务的Linux实例。关于如何连接Linux实例，请参见[基于远程桌面（RDP）协议连接Linux实例](#section_uda_fym_ovd)。

    **说明：** 如果通过远程桌面（RDP）协议连接实例，请保证公网带宽大于等于5 Mbit/s，否则远程桌面会卡顿。


Workbench还支持可视化管理Linux实例中的文件。具体操作，请参见[使用Workbench管理Linux实例文件]()。

## 基于终端连接（SSH）协议连接Linux实例

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  在左侧导航栏，选择**实例与镜像** \> **实例**。

3.  在顶部菜单栏左上角处，选择地域。

4.  在**实例列表**页面，找到需要连接的实例，单击该实例对应**操作**列下的**远程连接**。

5.  在弹出的**远程连接与命令**对话框中，单击**Workbench远程连接**对应的**立即登录**。

6.  在弹出的**登录实例**对话框中，输入信息。

    一般情况下按精简选项输入信息即可，如下表所示。

    |配置项|说明|
    |---|--|
    |**实例**|自动填充当前实例的信息，您也可以手动输入其他实例的IP或名称。|
    |**网络连接**|    -   专有网络实例支持选择公网IP或私网IP连接。
    -   经典网络实例支持选择公网IP或内网IP连接。 |
    |**用户名**、**密码**、**密钥**|输入用户名（例如root），并选择认证方式。支持的认证方式如下：    -   **密码认证**：需要继续输入登录密码。
    -   **证书认证**：需要继续输入或上传证书。如果证书已加密，还需要输入密钥口令。 |

    在对话框底部单击**完整选项**可以展开更多配置项，如下表所示。

    |配置项|说明|
    |---|--|
    |**资源组**|默认为**全部**，即可以手动选择任一资源组的资源。|
    |**区域**|默认为**全部**，即可以手动选择任一地域的资源。|
    |**连接协议**|默认为**终端连接（SSH）**。|
    |**端口**|连接协议为**终端连接（SSH）**时，默认端口为22。|
    |**语言环境**|偏好语言影响输出的内容，选择**默认**时，Workbench自动探测您远程主机的语言设置并进行合适的配置。|
    |**字符集**|偏好字符集影响输出内容的显示结果，选择**默认**时，Workbench自动探测您远程主机的字符集设置并进行合适的配置。|

7.  单击**确定**。


如果确定已满足本文的前提条件，连接实例时仍失败，请检查实例内部配置是否满足要求：

-   开启SSHD的远程服务，例如Linux系统中的SSHD服务。
-   开放终端连接端口，通常为22端口。
-   如果使用root用户登录Linux实例，需要保证在/etc/ssh/sshd\_config文件中配置`PermitRootLogin yes`，具体操作请参见[为Linux实例开启root用户远程登录](#section_m1n_unh_gr1)。

## 基于远程桌面（RDP）协议连接Linux实例

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  在左侧导航栏，选择**实例与镜像** \> **实例**。

3.  在顶部菜单栏左上角处，选择地域。

4.  在**实例列表**页面，找到需要连接的实例，单击该实例对应**操作**列下的**远程连接**。

5.  在弹出的**远程连接与命令**对话框中，单击**Workbench远程连接**对应的**立即登录**。

6.  在弹出的**登录实例**对话框，输入信息。

    1.  在对话框底部单击**完整选项**。

    2.  在**连接协议**区域，选择**远程桌面（RDP）**。

    3.  在弹出的对话框中，单击**确定**。

    4.  输入其他信息。

        |配置项|说明|
        |---|--|
        |**资源组**|默认为**全部**，即可以手动选择任一资源组的资源。|
        |**区域**|默认为**全部**，即可以手动选择任一地域的资源。|
        |**实例**|自动填充当前实例的信息，您也可以手动输入其他实例的IP或名称。|
        |**网络连接**|        -   专有网络实例支持选择公网IP或私网IP连接。
        -   经典网络实例支持选择公网IP或内网IP连接。 |
        |**端口**|连接协议为**远程桌面（RDP）**时，默认端口为3389。|
        |**用户名**、**密码**|输入用户名（例如Administrator）和密码。|

7.  单击**确定**。


如果确定已满足本文的前提条件，连接实例时仍失败，请检查实例内部配置是否满足要求：

-   开启远程桌面服务，例如Linux系统中自行安装的XFreeRDP服务。
-   开放远程桌面端口，通常为3389端口。
-   如果使用root用户登录Linux实例，需要保证在/etc/ssh/sshd\_config文件中配置`PermitRootLogin yes`，具体操作请参见[为Linux实例开启root用户远程登录](#section_m1n_unh_gr1)。

## 为Linux实例开启root用户远程登录

部分Linux系统中，SSHD服务默认禁用root用户远程登录，导致登录时提示用户名或密码错误。您可以按照以下步骤开启root用户远程登录。

1.  [通过密码认证登录Linux实例（VNC）](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过VNC远程连接登录Linux实例.md)。

2.  打开SSH配置文件。

    ```
    vi /etc/ssh/sshd_config
    ```

3.  将`PermitRootLogin no`修改为`PermitRootLogin yes`。

4.  按Esc键，输入:wq保存修改。

5.  重启SSHD服务。

    ```
    service sshd restart
    ```


## Workbench相关安全组规则详情

Workbench相关安全组规则详情和网络类型有关：

-   如需连接专有网络实例，请在**安全组规则**页面的**入方向**页签添加安全组规则，详情如下表所示。

    |授权策略|优先级|协议类型|端口范围|授权对象|
    |----|---|----|----|----|
    |**允许**|1|**自定义TCP**|    -   Linux实例默认开放22端口：选择**SSH\(22\)**。
    -   如果您手动开放了其他端口：手动输入端口范围。
|    -   如果通过实例的公网IP（包括固定公网IP和EIP）连接：添加47.96.60.0/24和118.31.243.0/24。
    -   如果通过实例的专有网络私网IP连接：添加100.104.0.0/16。
**说明：** 您也可以添加0.0.0.0/0，但存在安全风险，请谨慎使用。 |

-   如需通过公网连接经典网络实例，请在**安全组规则**页面的**公网入方向**页签添加安全组规则，详情如下表所示。

    |授权策略|优先级|协议类型|端口范围|授权对象|
    |----|---|----|----|----|
    |**允许**|1|**自定义TCP**|    -   Linux实例默认开放22端口：选择**SSH\(22\)**。
    -   如果您手动开放了其他端口：手动输入端口范围。
|通过实例的公网IP（包括固定公网IP和EIP）连接：添加47.96.60.0/24和118.31.243.0/24。 **说明：** 您也可以添加0.0.0.0/0，但存在安全风险，请谨慎使用。 |

-   如需通过内网连接经典网络实例，请在**安全组规则**页面的**入方向**页签添加安全组规则，详情如下表所示。

    |授权策略|优先级|协议类型|端口范围|授权对象|
    |----|---|----|----|----|
    |**允许**|1|**自定义TCP**|    -   Linux实例默认开放22端口：选择**SSH\(22\)**。
    -   如果您手动开放了其他端口：手动输入端口范围。
|通过实例的经典网络内网IP连接：添加11.195.184.0/24和11.246.55.0/24。 **说明：** 为内网入方向规则添加0.0.0.0/0存在高安全风险，不建议使用。 |


## 常见问题

无法连接实例时，您可以自行排查，详情请参见[远程连接FAQ]()和[GuestOS常见问题与修复方案](https://help.aliyun.com/document_detail/175789.html)。

