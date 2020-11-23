# 授予实例RAM角色

本文介绍了如何在控制台创建、授权实例RAM角色，并将其授予ECS实例。

-   您已经开通RAM服务。参见RAM文档[开通方法](/cn.zh-CN/产品定价/计费方法.md)。
-   待授予实例RAM角色的ECS实例网络类型必须是专有网络VPC。
-   如果您是通过RAM用户操作本文示例，您需要通过云账号授权RAM用户允许使用实例RAM角色。详细步骤请参见[授权RAM用户使用实例RAM角色](/cn.zh-CN/安全/实例RAM角色/管理实例RAM角色/授权RAM用户使用实例RAM角色.md)。

-   一台ECS实例一次只能授予一个实例RAM角色。
-   当您给ECS实例授予了实例RAM角色后，并希望在ECS实例内部部署的应用程序中访问云产品的API时，您需要通过实例元数据获取实例RAM角色的临时授权Token。详细步骤请参见[获取临时授权Token](/cn.zh-CN/安全/实例RAM角色/管理实例RAM角色/获取临时授权Token.md)。

## 操作步骤

本文示例使用云账号在RAM控制台创建一个实例RAM角色，并将其授予ECS实例：

1.  [步骤一：创建实例RAM角色](#section_s9s_ayg_45l)
2.  [步骤二：为RAM角色授予权限](#section_dpz_sjj_rbj)
3.  [步骤三：为实例授予RAM角色](#section_xb2_v3o_mtj)

## 步骤一：创建实例RAM角色

按以下步骤在访问控制RAM控制台创建一个实例RAM角色：

1.  云账号登录[RAM控制台](https://ram.console.aliyun.com/)。

2.  在左侧导航栏，单击**RAM角色管理**。

3.  单击**创建RAM角色**。

4.  当前可信实体类型选择为**阿里云服务**，单击**下一步**。

    **阿里云服务**用于授权ECS实例访问或管理您的云资源。RAM角色选择**阿里云服务**类型后，支持授予给ECS实例。

    ![选择云服务](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6756775061/p183974.png)

    **说明：**

    如果您的RAM角色选择**阿里云账号**等类型，创建结束后需要在RAM角色的**信任策略管理**页签，单击**修改信任策略**手动添加以下ECS服务授权策略。

    ```
    "Service": [
    	"ecs.aliyuncs.com"
    ]
    ```

5.  选择角色类型为**普通服务角色**。

6.  输入**角色名称**和**备注**。

7.  选择受信服务为**云服务器**。

8.  单击**完成**。


配置完成后，在RAM角色的**信任策略管理**页签中，确认是否包含以下ECS服务授权策略。

![ecs服务](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8575775061/p183955.png)

## 步骤二：为RAM角色授予权限

按以下步骤在访问控制RAM控制台授权实例RAM角色一个系统权限或者自定义权限：

1.  云账号登录[RAM控制台](https://ram.console.aliyun.com/)。

2.  （可选）如果您不使用系统权限，可以参见[账号访问控制](/cn.zh-CN/安全/账号访问控制.md)创建自定义权限策略章节创建一个自定义策略。

3.  在左侧导航栏，单击**RAM角色管理**。

4.  在**RAM角色名称**列表下，单击目标RAM角色名称。

5.  在**权限管理**页签下，单击**精确授权**。

6.  选择权限类型为**系统策略**或**自定义策略**。

7.  输入策略名称。

8.  单击**确定**。

9.  单击**关闭**。


## 步骤三：为实例授予RAM角色

按以下步骤在ECS控制台为一台ECS实例授予实例RAM角色：

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  在左侧导航栏，单击**实例与镜像** \> **实例**。

3.  在顶部菜单栏左上角处，选择地域。

4.  找到要操作的ECS实例，选择**更多** \> **实例设置** \> **授予/收回RAM角色**。

5.  在弹窗中，选择创建好的实例RAM角色，单击**确定**完成授予。


以下示例演示了如何授予实例RAM角色。

![授予实例RAM角色](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5834129951/p128555.gif)

您也可以在创建ECS实例时，并在**系统配置**页面的**RAM角色**属性中为实例选择已创建好的实例RAM角色。更多详情请参见[使用向导创建实例](/cn.zh-CN/实例/创建实例/使用向导创建实例.md)。

**相关文档**  


[CreateRole](/cn.zh-CN/API参考/API参考（RAM）/角色管理接口/CreateRole.md)

[CreatePolicy](/cn.zh-CN/API参考/API参考（RAM）/权限策略管理接口/CreatePolicy.md)

[AttachPolicyToRole](/cn.zh-CN/API参考/API参考（RAM）/权限策略管理接口/AttachPolicyToRole.md)

[AttachInstanceRamRole](/cn.zh-CN/API参考/实例/AttachInstanceRamRole.md)

