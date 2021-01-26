---
keyword: [阿里云, ecs, 服务器, 弹性计算]
---

# 在移动设备上连接Linux实例

在iOS、Android等移动设备环境中，您可以使用用户名密码验证的方式远程连接Linux实例。

-   已创建实例。
-   已为实例设置登录密码。
-   已为实例分配固定公网IP或绑定EIP。
-   实例处于运行中状态。
-   为实例所在的安全组添加安全组规则，放行对相应端口的访问，具体操作请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。

    |网络类型|规则方向|授权策略|端口范围|优先级|授权对象|
    |----|----|----|----|---|----|
    |专有网络VPC|入方向|允许|SSH（22）|1|0.0.0.0/0|
    |经典网络|公网入方向|

    |网络类型|网卡类型|规则方向|授权策略|协议类型|端口范围|优先级|授权类型|授权对象|
    |----|----|----|----|----|----|---|----|----|
    |专有网络VPC|无需配置|入方向|允许|SSH（22）|22/22|1|IPv4地址段访问|0.0.0.0/0|
    |经典网络|公网|


根据移动设备的操作系统，您可以使用不同的工具远程连接Linux实例：

-   [在iOS环境中使用SSH Control Lite连接Linux实例](#section_1k4_15a_pb8)
-   [在Android环境中使用JuiceSSH连接Linux实例](#section_euu_1ti_i0n)

## 在iOS环境中使用SSH Control Lite连接Linux实例

本示例中使用用户名和密码验证。

1.  下载SSH Control Lite。

2.  启动SSH Control Lite。

3.  在页面底部，单击**Hosts**。

4.  在页面左上角，单击**+**图标。

    ![iOS环境中连接Linux实例-001](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5904359951/p77178.png)

5.  单击**Connection**。

    ![iOS环境中连接Linux实例-002](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5904359951/p77179.png)

6.  输入连接信息，然后单击**Save**。

    -   **Name**：输入Host名称。本示例中为**DocTest**。
    -   **Protocol**：使用默认值**SSH**。
    -   **Host**：输入待连接Linux实例的固定公网IP或EIP。
    -   **Port**：输入端口号**22**。
    -   **Username**：输入用户名**root**。
    -   **Password**：输入实例登录密码。
    ![iOS环境中连接Linux实例-003](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5904359951/p77180.png)

7.  在页面底部，单击**Remote Controls**。

    ![iOS环境中连接Linux实例-004](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5904359951/p77181.png)

8.  在页面左上角，单击**+**图标。

    创建一个新的远程连接会话，本示例中会话命名为**New remote**。

    ![iOS环境中连接Linux实例-005](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5904359951/p77187.png)

9.  单击**Host1**。

    ![iOS环境中连接Linux实例-006](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5904359951/p77190.png)

10. 单击**Bind**。

    ![iOS环境中连接Linux实例-007](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5904359951/p77193.png)

11. 选择刚添加的Linux实例。

    本示例中为**DocTest**。

    ![iOS环境中连接Linux实例-008](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5904359951/p77196.png)

12. 在页面的右上角单击**Done**。进入**Edit**状态后，单击**DocTest**。

    ![iOS环境中连接Linux实例-009](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6904359951/p77198.png)

13. 单击**Connect**。

    ![iOS环境中连接Linux实例-010](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6904359951/p77199.png)

14. 选择**Yes, Once**或**Yes, Permanently**。

    连接成功后，**DocTest**前的指示图标会变为绿色。

    ![iOS环境中连接Linux实例-011](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6904359951/p77204.png)

15. 单击**DocTest**。

    ![iOS环境中连接Linux实例-012](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6904359951/p77205.png)

16. 单击**Console**，进入Linux实例的管理界面。

    ![iOS环境中连接Linux实例-013](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6904359951/p77206.png)


至此，您已经成功地连接了Linux实例。

![iOS环境中连接Linux实例-014](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6904359951/p77214.png)

## 在Android环境中使用JuiceSSH连接Linux实例

本示例中使用用户名和密码进行认证。

1.  安装JuiceSSH。

2.  启动JuiceSSH。

3.  单击**Connections**。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6904359951/p5320.png)

4.  单击**+**图标。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6904359951/p5321.png)

5.  输入连接信息，然后单击![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/58642/cn_zh/1503983576102/check%20icon.png)图标。

    -   **Nickname**：输入连接会话的名称。本示例中为**DocTest**。
    -   **Type**：使用默认值**SSH**。
    -   **Address**：输入需待连接Linux实例的固定公网IP或EIP。
    -   设置**Identity**：
        1.  单击**Identity**，在下拉列表里选择**New**。
        2.  输入如下信息，然后单击![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/58642/cn_zh/1503983576102/check%20icon.png)图标。
            -   **NickName**：可选项，您可以根据管理需要设置一个身份名称，方便后续管理。本示例中为**DocTest**。
            -   **Username**：输入用户名**root**。
            -   **Password**：单击**SET\(OPTIONAL\)**，然后输入实例登录密码。

                ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6904359951/p5322.png)

    -   **Port**：输入端口号**22**。

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6904359951/p5323.png)

6.  确认提示信息，然后单击**ACCEPT**。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6904359951/p5324.png)

7.  首次连接时，会出现设置字体等提示信息。确认信息，然后单击**OK - I’VE GOT IT!**。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6904359951/p5325.png)


至此，您已经成功连接了Linux实例。

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7904359951/p5326.png)

**相关文档**  


[连接方式概述ECS远程连接操作指南](/intl.zh-CN/实例/连接实例/连接方式概述.md)

